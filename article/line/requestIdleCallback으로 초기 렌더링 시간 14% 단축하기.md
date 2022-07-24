# requestIdleCallback으로 초기 렌더링 시간 14% 단축하기

- https://engineering.linecorp.com/ko/blog/line-securities-frontend-4

## 작업 환경

- 성능 개선은 프런트 엔드 성능의 전형적인 지표인 Core Web Vitals 개선을 목표로 삼았고 결과 측정 수단으로는 Google Chrome 확장 프로그램인 Lighthouse를 사용했습니다.

## 성능 개선 1

- LCP의 개선을 기대하며 레이지 로딩을 이용한 번들 분할을 아래의 코드와 비슷하게 진행하였습니다.

```ts
import { lazy, Suspense } from "react";
import MainContents from "./mainContents";

const OtherContents = lazy(() => import("./otherContents"));

const Home: React.VFC = () => {
  return (
    <div>
      <MainContents />
      <Suspense fallback={<p>Loading...</p>}>
        <OtherContents />
      </Suspense>
    </div>
  );
};
```

## 수상한 appendChild

- 성능을 측정해보니 렌더링을 처리하는 중에 왠지 모르게 시간이 걸리는 appendChild가 나열된 것을 발견했습니다.
- appendChild를 실행하는 것은 React가 아니라 webpack의 런타임이었습니다.
- 초기 렌더링에 appendChild가 나타나는 현상을 설명할 수 있는 요인은 두 가지입니다.
  - import()에 해당하는 코드를 실행할 때 webpack 런타임이 그 자리에서 동기적으로 스크립트 요소를 생성하고 임베딩을 실시한다는 점
  - React의 lazy()로 생성한 컴포넌트를 렌더링한 시점에서 역시 동기적으로 콜백 함수를 호출한다는 점
- 이 두 가지 처리가 모두 동기적으로 실행된 결과, appendChild가 초기 렌더링 처리에 섞이게 되었습니다.

## requestIdleCallback 함수 도입

### Background

- 초기 렌더링하는 동안에는 메인 스레드가 콘텐츠를 최대한 빨리 표시하는 것에 집중하기를 바라기 때문에 레이지 로딩 관련 작업은 뒤로 미루고 싶습니다.

### Description

- requestIdleCallback은 브라우저의 메인 스레드(JavaScript 실행 등을 담당하는 스레드)가 비어 있으면 지정한 콜백 함수를 실행하도록 지시할 수 있는 함수입니다.

```ts
import { lazy } from "react";

export const lazyIdle: typeof lazy = (factory) => {
  return lazy(
    () =>
      new Promise((resolve) => {
        window.requestIdleCallback(() => resolve(factory()), {
          timeout: 3000,
        });
      })
  );
};

const OtherContents = lazyIdle(() => import("./otherContents"));
```

- 위와 같이 lazyIdle()에 전달된 팩토리 함수(() => import(‘./otherContents’)와 같은 함수)의 실행을 requestIdleCallback으로 지연시킵니다.
- 결과적으로 스크립트 요소 삽입을 초기 렌더링 완료 후로 지연시킵니다. 앞서 소개한 Google에서 작성한 글에서 requestIdleCallback의 콜백 내에서 DOM을 조작하는 것을 권장하지 않고 있는데요. 스크립트 요소?이므로(레이아웃 등에 영향을 주지 않음) 문제없습니다.
- IOS는 requestIdleCallback를 지원하지 않기에 polyfill을 이용했습니다.

## 성능 개선 결과

- 다섯 군데 정도 lazy()를 lazyIdle()로 교체를 하고 14%정도 개선되는 결과를 얻어내었습니다.
  - 대략 700ms => 600ms 감소

## My Opinion

- nextjs에서 이용하려면 dynamic noSSR 설정을 하여 CSR 측면에서 최적화하는 방법으론 충분할듯 싶습니다.
