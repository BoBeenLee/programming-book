# Islands Architecture

- https://www.patterns.dev/posts/islands-architecture/#:~:text=The%20term%20Islands%20architecture%20was,top%20of%20otherwise%20static%20HTML.

- 서버렌더링 페이지내에 작고 집중적인 상호작용하는 것을 선호합니다.
- 향상이 나아지는 방향보단 명시적으로? islands 결과물은 점진적인 나아지는 HTML입니다.
- 모든 페이지 렌더링을 통제되는것보단 다수의 entrypoint를 이용합니다.
  상호작용의 islands를 위한 스크립트는 독립적으로 전달되고 hydared됩니다. 정적인 HTML되는 나머지 페이지를 할 수 있습니다.

- 과도한 js 로딩, 프로세싱은 퍼포먼스를 저해합니다. 그러나 몇몇 상호작용, js는 필수적으로 요구됩니다.
- variants of SRR에 대해 논하고자합니다. 균형을 찾아서 app을 빌드할수 있게 해줍니다.

1. CSR(클라이언트 측 렌더링) 애플리케이션과 유사한 상호 작용
2. SSR 애플리케이션에 필적하는 SEO 이점.

- SSR 위한 core 원칙은 HTML을 서버에 렌더링하고 필요한 JS를 client로 hydrate합니다.
  Rehydration은 Server에서 렌러딩 후 Client측 UI 컴포넌트 상태 재생성 프로세스입니다.
  rehydartion이 비용으로 온다면 SSR의 변형은 재수화 프로세스를 최적화하려고 시도합니다.
  이는 중요한 컴포넌트, 스트리밍 컴포넌트의 부분 hydration에 의해 달성하게 됩니다.
  그러나 위의 기술에서 최종적으로 제공되는 순수 JavaScript는 동일하게 유지됩니다.

- islands 아키텍처라는 용어는 Katie Sylor-Miller와 Jason Miller에 의해 대중화되어 정적 HTML 위에 독립적으로 제공될 수 있는 상호 작용의 "islands"을 통해 전달되는 JavaScript의 양을 줄이는 것을 목표로 하는 패러다임을 설명합니다.

- islands는 정적인 부분과 동적인 islands와 함께 구획화된 페이지 뷰를 제안하는 컴포넌트 기반 아키텍져입니다.
- 페이지 내 statis regions은 순수하고 상호작용 HTML이 없으며 hydration이 필요없습니다.
- 동적 regions는 HTML과 결합하여 렌더링 후 그들 자신이 rehydratiing 수용하는 스크립트합니다.

## 동적 컴포넌트의 islands

- 대부분의 페이지는 정적 콘텐츠와 동적 콘텐츠의 조합입니다. 일반적으로 페이지는 격리될 수 있는 대화형 영역이 포함된 정적 콘텐츠로 구성됩니다.
  ex) 블로그 포스트, e-commerce 프로덕트 페이지,
- 렌더링 후 동적 콘텐츠(버튼, 필터, 검색 표시줄)를 이벤트에 다시 연결해야 합니다

- 점진적 hydration에선, 페이지의 hydration 아키텍쳐는 탑 다운 방식입니다.
  페이지는 각 컴포넌트를 hydration, 스케쥴링을 통제합니다.
  각 컴포넌트는 islands 아키텍쳐 내 비동기적으로 실행하는 hydration script를 가집니다.
  한 구성 요소의 성능 문제가 다른 구성 요소에 영향을 주지 않아야 합니다.

## islands 구현

- islands 아키텍처는 다양한 소스에서 개념을 차용하여 최적으로 결합하는 것을 목표로 합니다.
- Jekyll 및 Hugo와 같은 템플릿 기반 정적 사이트 생성기는 페이지에 대한 정적 구성 요소의 렌더링을 지원합니다. 대부분의 최신 JavaScript 프레임워크는 동형 렌더링도 지원하므로 동일한 코드를 사용하여 서버와 클라이언트에서 요소를 렌더링할 수 있습니다.

## Frameworks

- ex) Marko, Astro, Eleventy + Preact

## 장단점

- islands 아키텍처는 static, 부분적인 hydration, ssr과 같은 서로 다른 렌더링으로부터 아이디어들을 결합합니다.
- 구현하는 islands 잠재적 이득은 아래 부분을 따릅니다.

- Performance: 클라이언트로부터 js 코드를 전달하는 양을 줄일 수 있습니다. 전송된 코드는 대화형 구성 요소에 필요한 스크립트로만 구성되며, 이는 전체 페이지에 대한 가상 DOM을 다시 만들고 페이지의 모든 요소를 재수화하는 데 필요한 스크립트보다 훨씬 적습니다. JavaScript의 작은 크기는 자동으로 더 빠른 페이지 로드 및 TTI(Time to Interactive)에 해당합니다.
- SEO: 모든 정적 콘텐츠가 서버에서 렌더링되기 때문에; 페이지는 SEO 친화적입니다.
- Prioritizes important content: 주요 콘텐츠(특히 블로그, 뉴스 기사 및 제품 페이지의 경우)는 사용자가 거의 즉시 사용할 수 있습니다. 상호 작용을 위한 보조 기능은 일반적으로 키 콘텐츠를 사용한 후 점차적으로 사용할 수 있게 된 후에 필요합니다.
- Accessibility: 표준 정적 HTML 링크를 사용하여 다른 페이지에 액세스하면 웹사이트의 접근성을 개선하는 데 도움이 됩니다.
- Component-based: 아키텍처는 재사용성 및 유지 보수성과 같은 구성 요소 기반 아키텍처의 모든 이점을 제공합니다.

### 장점에도 불구하고 개념은 아직 초기 단계에 있습니다. 제한된 지원으로 인해 몇 가지 단점이 있습니다.

- 몇몇 프레임워크에만 이용가능하며 직접 아키텍터를 개발해야합니다. or Astro, Marko로 migration 작업을 해야하는 추가적인 노력이 필요합니다.
- Jason의 초기 게시물 외에 아이디어에 대한 논의가 거의 없습니다.
- 이 아키텍처는 수천 개의 섬이 필요할 수 있는 소셜 미디어 앱과 같은 대화형 페이지에는 적합하지 않습니다.
- 페이지 성능에 미치는 영향을 최소화하면서 동적 구성 요소를 통해 상호 작용을 지원하면서 정적 콘텐츠를 렌더링하기 위한 SSR의 사용을 강조합니다. 앞으로 이 분야에서 더 많은 플레이어를 만나고 사용 가능한 구현 옵션의 폭이 넓어지기를 바랍니다.

## My Opinion

- React Server Component와 아키텍처가 유사한 느낌을 받았으며 해당 차이를 https://www.patterns.dev/posts/react-server-components/ 읽어봐야할듯하다.
  - 차이점이라면 각 컴포넌트 끼리 region을 나누는것은 동일한거같지만 React Server Component로 인해 client에서 js라이브러리를 로드하여 렌더링하는 것이 아닌 서버에서 렌더링된 데이터를 전달해주는 방식으로 client에서 js 라이브러리를 로드할 필요가 없기에 가지는 이점이 있는듯하다.
