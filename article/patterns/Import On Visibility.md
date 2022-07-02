# Import On Visibility

- https://www.patterns.dev/posts/import-on-visibility/

- 중요하지 않은 컴포넌트 로드하기

유저 상호작용에 있어 우리는 자주 보이지 않는 페이지까지 로드합니다.
이 방법의 좋은 예시로 보이지 않는 부분을 이미지 lazy loading을 하는것입니다. 유저가 스크롤을 내릴때 오직 한번 로드됩니다.
모든 이미지가 즉시 요청되지 않을때, 초기 로딩시간을 줄일 수 있습니다.
현재 뷰포트를 어디인지 알기 위해서 IntersectionObserver API 를 사용하며 라이브러리를 사용할 수 도 있습니다. (react-lazyload, react-loadable-visibility)

fallback 컴포넌트는 앱내 멈춰져있는 현상을 방지해줍니다.
단순하게 짧은 시간동안 module이 loaded, parsed, compiled, executed까지 기다리게 해주는데 필요합니다.
