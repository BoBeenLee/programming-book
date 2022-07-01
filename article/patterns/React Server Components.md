# React Server Components

- https://www.patterns.dev/posts/react-server-components/

- 서버 구성 요소는 SSR을 보완하여 JavaScript 번들에 추가할 필요 없이 중간 추상화로 렌더링합니다.

- zero 번들 사이즈 RSC는 서버 기잔 멘탈 모델과 함께 현대 UX에 초점을 두었습니다.
- SSR컴포넌트와 차이점이 있고 핵심적인 Client Side JS 번들들만 전달하는 결과를 가질 수 있습니다.

prod 레벨단에선 아직 준비가 되어있지 않고 계속 관심을 가지며 주시할 가치가 있습니다.

- https://www.youtube.com/watch?v=TQQPAU21ZUw 를 시청을 통해 RFC(https://github.com/reactjs/rfcs/blob/bf51f8755ddb38d92e23ad415fc4e3c02b95b331/text/0000-server-components.md)를 읽기

## Server-side rendering limitations

- 오늘날엔 클라이언트 JS 서버사이드 렌더링은 차선책일 수 있습니다.
- JS는 HTML string내에 렌더링됩니다. HTML은 브라우저에 전달되며 빠른 First Contentful Paint, Largest Contentful Paint 결과물로 나타날 수 있습니다.

- 그러나 JS는 상호작용을 위해 fetch가 여전히 필요하며 자주 hydration 단계를 통하여 진행하게 됩니다.
- SSR은 초기 페이지 로드를 위해 사용되고 그러기에 hydration 후 그것을 다시 사용하는 것을 볼 수 없을 것입니다.

Note: 오직 서버에서 SSR App을 빌드할 수 있고 클라이언트에서 hydrating하는것을 피하는것이 사실?이지만, 과도한 상호작용 모델의 과도한 상호 작용에는 종종 React 외부로 나가는 것이 포함됩니다.
서버 구성 요소가 활성화하는 하이브리드 모델을 사용하면 구성 요소별로 이를 결정할 수 있습니다.

RSC와 함께라면 refetch를 할 수가 있습니다. 새로운 데이터를 서버에서 받아야할때 컴포넌트 앱내에 리렌더링됩니다. 클라이언트에서 보내야하는 코드의 양을 제한할 수 있습니다.

## Server Components

- React의 새로운 서버 구성 요소는 서버 측 렌더링을 보완하므로 JavaScript 번들에 추가할 필요 없이 중간 추상화 형식으로 렌더링할 수 있습니다.
- 이를 통해 상태 손실 없이 서버 트리를 클라이언트 쪽 트리와 병합할 수 있으며 더 많은 구성 요소로 확장할 수 있습니다.
- 서버 컴포넌트는 SSR을 위해 대체하지는 않습니다. When paired together, they support quickly rendering in an intermediate format, then having Server-side rendering infrastructure rendering this into HTML enabling early paints to still be fast. We SSR the Client components which the Server components emit, similar to how SSR is used with other data-fetching mechanisms.
- 이 순간 JS 번들은 줄어들 것이고 초기 탐색은 18~19% 작은 번들 사이즈를 보여줄 것입니다.

## Automatic Code-Splitting

- 코드 분할하여 필요한 사용자에게 전달하는것이 best practice로 고려됩니다.
- 이는 당신의 앱을 작은 반들 적은 코드들로 client에 전달되게 합니다.
- 서버 구성 요소 이전에는 수동으로 React.lazy()를 사용하여 "분할 지점"을 정의하거나 경로/페이지와 같은 메타 프레임워크에 의해 설정되어 새로운 청크를 생성했습니다.

## 코드 스프리팅의 챌린지

- meta 프레임워크 외, 수동으로 최적화하여 import 문을 동적 가져오기로 교체해야 합니다.
- 애플리케이션이 사용자 경험에 영향을 미치는 구성 요소를 로드하기 시작할 때 지연될 수 있습니다.

서버 컴포넌트는 클라이언트 컴포넌트 내 모든 normal import들을 자동으로 코드 스프리팅해줍니다.
또한 개발자는 훨씬 더 일찍(서버에서) 사용할 구성 요소를 선택할 수 있으므로 클라이언트가 렌더링 프로세스에서 더 일찍 가져올 수 있습니다.

## 서버 컴포넌트는 Next.js SSR을 대체할 수 있는가?

- No. 그들은 차이점이 있습니다. 서버 컴포넌트 초기 채택은 연구와 실험이 계속됨에 따라 Next.js와 같은 메타 프레임워크를 통해 실제로 실험될 것입니다.

To summarize a good explanation of the differences between Next.js SSR and Server Components from Dan Abramov:

- 서버 컴포넌트를 위한 코드는 클라이언트로 전달되지 않습니다.
  - React를 사용한 SSR 구현 코드는 클라이언트로 JS bundle로 언제든 보낼 수 있습니다.
  - 이는 상호작용에 딜레이를 줄 수 있습니다.
- 서버 컴포넌트는 트리 내에서 언제든지 백엔드로 접근을 허용합니다.
  - Next.js를 이용할때 getServerSideProps를 통하여 백엔드에 접근할 수 있습니다. 그것은 탑 레벨 페이지에 동작하는 제한적인 접근입니다. 임의의 npm 구성 요소는 이를 수행할 수 없습니다.
- 트리 내에 클라이언트 측 유지하는 동안 서버 컴포넌트는 refetch가 할 수 있습니다.
  - 이는 중요 전송 메커니즘이고 HTML 보다 더 나은, 내부 상태를 날리지 않고 서버 렌더링 부분에서 refetching을 허용가능합니다. (ex) 검색 입력 포커싱, 입력 상태 유지된 상태에서 검색 결과를 볼 수 있습니다.)

서버 구성 요소에 대한 초기 통합 작업 중 일부는 다음과 같은 webpack 플러그인을 통해 수행됩니다.

## My Opinion

- SSR를 보완한다라는 것이 키포인트인거같고 전에 읽은 Islands 아키텍쳐와 비교했을땐 smaller, focused 상호작용하는 서버렌더링 페이지를 hydration한다는 점에선 접점이 있어보이는듯 싶습니다.
  - 서버 컴포넌트 또한 작은 상호작용 컴포넌트 단위로 refetching하기에 rehydration한다는 것과 유사하다고 판단됩니다.
- Next.js를 대체하진 않지만 SSR을 보완한다는 점에서 Next.js SSR을 보완하는 feature라 생각하면 될듯하다.
