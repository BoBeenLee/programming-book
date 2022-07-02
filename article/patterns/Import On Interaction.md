# Import On Interaction

- https://www.patterns.dev/posts/import-on-interaction/

- 중요하지 않은 자원을 로드하는 방법

- 페이지 내에 필요하지 않은 자원, 컴포넌트를 위하여 코드, 데이터가 포함되어있을지도 모릅니다.

  - ex) 페이지 부분에서 스크롤하여 보이지 않는 영역의 데이터, 3rd party위젯 (비디오 플레이어, chat)

- 일찍이 자원을 로드하는것은 main thread가 블락당할 수 있습니다. 이같은 결과 인터렉션 메트릭스에 영향을 주게 됩니다. (ex) First Input Delay, Total Blokcin Time, Time To Interactive)
- 자원을 즉시 로딩하는 대신에 너는 해당 순간에 로드할 수 있습니다.
  - 처음 그 컴포넌트에 반응했을떄
  - 화면 스크롤을 내리는 순간
  - 컴포넌트의 지연로딩으로 브라우저가 놀고 있는 순간에 (requestIdleCallback)
- 추상화 레벨에 자원을 로드하는 다른 방법도 있습니다.

  - Eager - 바로 로드하는 방법
  - Lazy (Route-based) - route or (step by step)컴포넌트 기반으로 유저가 이동을 할때
  - Lazy (On interaction) - 유저가 UI 클릭할 때 (ex) 컬러 피커, 챗 보기 ... )
  - Lazy (In viewport) - 스크롤하여 해당 컴포넌트쪽으로 이동할때
  - Prefetch - 필요하기 전에 로드하지만 중요한 리소스가 로드된 후에
  - Preload - 일찍이 로드

- lazily importing을 한 성공?적인 케이스로는 Google Docs의 Share 버튼을 하나의 예로 보면 될듯 싶습니다.

## 3rd 파티 UI를 위한 Fake 로딩

렌더링 할때 or 코드 로드 중일때 3rd 스크립트가 임포팅 되고 있는 중일 수도 있고 제어하기 힘들 수 있습니다.
상호작용 로드 구현하기 위해 하나의 옵션으론 facade를 이용하는 것입니다.
facade란 이미지나 스크린샷과 같은 기본 경험을 시뮬레이션하는 더 많은 비용이 드는 구성 요소에 대한 간단한 "미리 보기" 또는 "자리 표시자"입니다. 경우에 따라서 마찬가지로, 파사드는 호버에서 필요한 리소스에 미리 연결할 수 있습니다.

ex) Video Player Embeds, Authentication (OAuth), Chat widgets

## 어떻게 반응형 임포트를 구현할 수 있는가?

### React

- React.lazy를 통한 code-splitting으로 쉽게 구현할 수 있습니다.

```
import React, { lazy, Suspense } from 'react';
import MessageList from './MessageList';
import MessageInput from './MessageInput';

const EmojiPicker = lazy(
  () => import('./EmojiPicker')
);

const Channel = () => {
  ...
  return (
    <div>
      <MessageList />
      <MessageInput />
      {emojiPickerOpen && (
        <Suspense fallback={<div>Loading...</div>}>
          <EmojiPicker />
        </Suspense>
      )}
    </div>
  );
};
```

## progressive loading의 부분을 통한 반응형 임포트

- 상호 작용 기반 지연 로딩에는 여러 가지 중요한 측면이 있습니다. (Google 필터 예시)
  - 먼저, 페이지가 시각적으로 빠르게 완성되도록 초기에 최소한의 코드를 다운로드합니다.
  - 다음으로, 사용자가 페이지와 상호 작용하기 시작하면 이러한 상호 작용을 사용하여 로드할 다른 코드를 결정합니다. 예를 들어 "추가 필터" 구성 요소에 대한 코드를 로드합니다.
  - 즉, 사용자가 사용할 필요가 없기 때문에 페이지의 많은 기능에 대한 코드가 브라우저로 전송되지 않습니다.

## 일찍이 클릭했을때 이벤트를 잃음을 피하는 방법

- 구글팀에선 JSAction을 통해 일찍이 프레임워크가 부트스트랩 되기전에 감지하여 완료된 후 재실행?(replaying)합니다.

## 데이터 호출은 어떤가?

- CSS, JS 호출과 유사하며 컴포넌트는 데이터가 필요할떄 인지하여 실행합니다.

## Trade-offs

### 만일 유저 클릭 후에 스크립트 로드가 오래걸린다면?

- 이러한 일이 일어나는 경우를 줄이는 방법은 더 잘 분해하는것과 페이지 내 중요한 컨텐츠 로딩이 완료된 후 자원을 prefetch하는 것입니다.

### 유저 반응 전에 기능성이 부족하다면?

- 예를 들면 임페디드된 비디오 플레이어가 자동 플레이를 할 수 없다거나
- 이러한 기능성이 핵심이라면 로딩 자원 접근 방식을 고려해야할지 모른다.
  - 예를 들면 유저가 반응할때까지 지연로딩하는것보다 화면 내 스크롤할때 3rd 파티 iframe를 lazy-loading한다거나

## 정적 변수를 통해 embeds 상호작용을 대체할 수도 있다.

- 성능을 최적화하는 경우 임베드를 비슷해 보이는 정적 변형으로 완전히 대체하여 보다 양방향 버전(예: 원본 소셜 미디어 게시물)에 연결하는 것이 가능합니다. 빌드 시 포함 데이터를 가져와 정적 HTML 버전으로 변환할 수 있습니다.
- ex) 블로그의 Social media embede를 삽입하는 경우

## 결론

- 3rd 파티 JS, 중요하지 않은 JS 요청 딜레이 일 경우에 유용할 수 있습니다.
- 보통은 3rd 파티에서 동기적인 부분을 비하기 위해 non-blocking 3rd 파티 스크립트 초점으로 사용합니다.
- 상호 작용 시 가져오기와 같은 패턴을 사용하면 중요하지 않은 리소스의 로드를 사용자가 해당 UI를 필요로 할 가능성이 훨씬 더 높은 시점으로 연기할 수 있습니다.
