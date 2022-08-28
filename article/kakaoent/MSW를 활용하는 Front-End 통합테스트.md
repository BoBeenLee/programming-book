# MSW를 활용하는 Front-End 통합테스트

- https://fe-developers.kakaoent.com/2022/220825-msw-integration-testing/?fbclid=IwAR2O6m0mJpLc8K243FmQEaIrnzKM6iOt2JmrYzqj0i_azWcJcCKiZ_NiYiU

## MSW의 도입

- 작은 단위테스트는 복잡도가 낮아 정상적으로 테스트 가능하지만 통합 테스트를 넘어가면서 문제가 발생하기 시작합니다. 여러 컴포넌트가 모여 하나의 기능을 수행하려면 서버와 통신해야 하는 경우가 많기 때문에 MSW필요성이 대두되게 되었습니다.

- 입력후 검색 결과를 보여주는 통합테스트의 예시로 MSW가 필요성에 대해 얘기
  - 서버 개발자와 협의가 이뤄진 API 스펙만 있다면 미리 목업을 만들어, 실제 데이터를 호출하듯이 테스트를 해볼 수 있게 되는 것

## MSW

- MSW는 API 요청을 가로채서 사전에 설정해둔 목업 데이터를 넘겨주도록 설정해 주는 도구입니다.

## 기본 세팅

## 통합 테스트 작성

1. 서버에서 데이터를 정상적으로 잘 가져와서 렌더링 하는가
2. 서로 다른 데이터에 따라 조건부 렌더링이 잘 되는가
3. 엣지 케이스 데이터들에 대해 처리가 잘 되어있는가
4. 네트워크 에러가 발생했을 때도 처리가 잘 되는가

### 목업을 통해 데이터 가져오기

- 기본적인 msw mock 설정 방법

### 동적으로 데이터 변경하기

```ts
/**
 * 타입을 변경해서 응답 데이터를 등록합니다
 * 혹은 목업 데이터 파일을 미리 만들어 두고 해당 데이터를 등록하는 것도 좋은 방법입니다.
 */
const result = searchResultData;
result.data = result.data.map((item) => ({ ...item, type: "rounded" }));
server.use(rest.get("/search", (_, res, ctx) => res(ctx.json(result))));
```

### 엣지케이스 테스트하기

- 동적 데이터 변경을 통해 빈 데이터 값을 전달하여 엣지 케이스 테스팅

```
/**
* 위에서와 동일한 방법으로 Empty 데이터를 처리해 줍니다.
*/
overrideSearchResultWithEmptyData();
```

### 에러 발생 상황 테스트하기

- 동적 데이터 변경을 통해 400, 500에러를 반환하여 에러 발생 케이스 테스팅

```
function overrideSearchResultWithErrorData() {
  server.use(
    rest.get('/search', (_, res, ctx) =>
      res(ctx.status(404), ctx.json({ errorMessage: 'Not Found' })),
    ),
  );
}
...
overrideSearchResultWithErrorData();
```

## 그 외 MSW 활용 방법

- 스토리북을 통해 시각적으로 테스트를 진행하는 경우
  - 모킹을 활용한 Storybook Interaction Testing
- 로컬 개발 서버 연동

## 맺음말

- 통합 테스트를 진행하면서 발생하는 API와 관련된 이슈는 애자일과 같은 빠른 개발 방법론을 추구하는 오늘날의 많은 프로젝트에서 마주하는 문제이기에 정해진 시점까지 프로덕트를 출시하기 위해 API개발이 끝나지 않아도 FE개발을 시작하는 병렬적인 작업을 하게 되는 경우가 발생하기에 MSW를 활용한다면 실제 유사 환경에서 통합 테스트를 효율적으로 진행할 수 있습니다.
- 테스트를 통과한다면 현실에서도 동일한 상황에 알맞게 대처하는 것을 보장하게 됩니다. 또 다음 스프린트가 진행됨에 따라 변경된 API 스펙을 미리 적용하여 기존 코드와의 정합성을 빠르게 체크할 수도 있어 유지 보수성도 훨씬 증진됨을 경험하게 될 것입니다.

## My Opinion

- 보통 컴포넌트 화면 개발 후 API 연동을 진행하기에 API개발이 지연되거나 기다려야하는 상황이 생길경우, 1) Mock API를 받는 형식으로 처리를 할 수 있을 것이고 2) MSW와 같이 API 요청을 가로채서 사전에 설정해둔 목업 데이터를 넘겨주도록 설정해주는 방법으로 처리할 수 있을것으로 보입니다.
- 통합 테스트 관점으로 보았을땐 2)번 선택지가 동적으로 데이터 변경을 할 수 있는 측면에서 큰 이점을 가질 수 있고 스토리북과의 연계성을 생각해본다면 Mock API보다 더 나은 방법이라 생각합니다.
- 다만 MSW Response와 실제 API Response의 sync유지를 된다는 가정하에기에 API Codegenerator를 활용하여 sync여부를 CI시점에 체킹을 꼭 해줘야한다는 점이 있어보입니다.
