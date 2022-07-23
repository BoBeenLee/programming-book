# JavaScript Bundle Diet

- https://www.youtube.com/watch?v=EP7g5R-7zwM&list=WL&index=11

## 왜 번들사이즈가 중요한가?

    - 2초 이내 로드시 이탈율 9%
    - 5초 초과시 이탈율 38%

## Website Speed

- 바이트별로 보면, 자바스크립트는 같은 크기의 이미지나 웹폰트보다 브라우저가 처리하는 비용이 많이 듭니다.
  - API 콜이 너무 많거나, critical rendering path에 해당하는 리소스가 큰것처럼 다양한 원인으로 느려질 수있다.
  - 그중에 bundle size에 집중할것이다.
- 자바스크립트는 파싱, 컴파일, 실행까지 여러단계를 거치기때문에 자바스크립트가 더 비용이 높다.

## 원인 찾기

- Tooling
  - Webpack Analyse
    - 가장 다양한 정보를 주지만 사용이 복잡하고 느림
  - Webpack Visualizer
    - 깔끔한 시각화, 기능이 부족
  - Webpack Bundle Analyzer
    - 빠르게 찾기 위해선 해당 라이브러리를 추천

## 원인 분석 후

- 용량이 큰 라이브러리는 작은 라이브러리로 교체
- 용도가 겹치는 라이브러리는 하나의 라이브러리로 통일
- 종종 같은 라이브러리지만 버젼이 다른 경우를 발견할 수 있다.
  - why? 이유는 npm 특성

## 라이브러리 중복 줄이기

- 같은 라이브러리가 서로 다른 버젼을 참조하는 경우가 가끔 있음 (Dependency conflict)
- npm의 경우 nested dependencies
  - 그러나 중복된 라이브러리가 쌓이게 되면 과도하게 큰 용량을 차지하게 됩니다.
  - semver를 지킨다는 가정하에는 중복라이브러리 문제가 제거된다. 다만 항상 지켜지지 않기떄문에
- npm dedupe - 중복된 모듈을 줄일 수 있는 명령어

- yarn도 완벽하지 않음 ex) query-string이 중복해서 들어감

  - yarn deduplicate 한 라이브러리로 만들어준다.
  - yarn 2 - yarn dedupe

- 중복현상에는 lodash에서 발견할 수 있다.
  - lodash가 번들에 포함된 경우가 많아 lodash최적화는 의미가 있다.
  - 다양한 라이브러리에 있다. cjs, esm버젼, 각기능별로 존재함.
    - Webpack의 alias기능을 활용하면 웹팩에 있는 lodash기능만 이용하게 할 수 있다.
  - `babel-plugin-transform-imports`, `babel-plugin-lodash`를 이용하여 결과물을 최적화한다.

## 더 가벼운 라이브러리 사용하기

lodash

- lodash는 생각보다 용량이 크다. groupBy: 6kb
- shorthands표현, 개싱등을 지원하기 때문 sumBy(data, 'value')
- 토스에선 가능한 native를 사용하거나 더 가벼운 함수를 구현하여 사용중입니다.

## 더 가벼운 라이브러리 사용하기

- node.js와 브라우저 환경을 통일하기 위해 polyfill을 추가할 수 있습니다.
  - polyfill 추가될 경우 더 느려지는 경우도 있음.
- 토스의 경우 node-rsa란 라이브러리를 사용했는데요 (Node.js지원만 생각하고 만들어진거라 크립토 등등 다양한 라이브러리들이 포함되어있다.)
  - 폴리필이 들어갈 수 있기에 명시적으로 끄거나 browser에서 잘판단해주는 라이브러리 사용을 권합니다.
    - ex) create-react-app 명시적으로 끄는 node polyfill 설정을 가지고 있다.

## 더 가벼운 라이브러리 사용하기

- Bundle Phobia
  - gzip으로 압축되었을 때 용량과 다은로드 속도, 각버젼별 용량을 쉽게 확인할 수 있습니다.
  - 디펜던시를 미리 확인할 수 있습니다.(분석)
  - 추가적으로 비슷한 기능의 라이브러리들의 용량을 비교해주기도 합니다.
  - Exports Analysis tree shaking이 되었을때 함수별로 얼마나 용량을 차지할지 미리 확인해볼 수 있습니다.

## 라이브러리를 만드는 관점 중요한 포인트

- tree-shaking
  - 정적 분석을 통한 필요한 코드만 가져오는 기술
  - tree-shaking 지원된다면 정말로 사용 중인 코드만 번들에 포함되기 떄문에 더 가벼운 번들을 만들 수 있다.
- tree shaking의 어려움

```
export const a = foo();
export const b = bar();

import { b } from "./boo";
``
	- a는 뺄수 있을까?
		- 정답은 경우에 따라 다르다.


- 제거하여도 동작에 이상이 없음
```

function foo() {
return "Hello World!";
}
export const a = foo();
export const b = bar();

```

- 제거하면 동작이 달라질 수 있다. 왜냐하면 `let count = 0;`선언에 의해 b export 코드 동작에 영향을 줄 수 있기 때문에

```

let count = 0;
function foo() {
count ++;
return count;
}
export const a = foo();
export const b = bar();

```
- 오른쪽 코드처럼 순서, 호출위치에 따라서 동작이 달라지는 경우를 side effect가 있다한다.
- 이처럼 tree-shaking을 하려면 side effect가 없을때만 가능합니다.

- 번들러는 이런 side effect를 얼마나 잘판단하냐에 따라 tree shaking을 할 수도 안할 수 있다.

## Preserve Modules
- 라이브러리를 만들때에는 웹팩에게 사이드 이펙트 여부를 알려줘야한다.
```

preserveModules: false | true

```

- preserveModules 옵션을 키면 원본 소스 코드와 유사한 구조의 output이 나옵니다.
- preserveModules false일 경우, 원본 소스에 tree shaking이 불가능한 코드가 섞여있다면 최종 output은 한 파일이므로 파일 전체가 tree-shaking이 실패할 수 있다.
- preserveModules true를 킨다면 일부만 실패하여 진행합니다.


## 컴파일툴 잘고르기
- webpack에선 직접 dead코드를 제거하기도 하지만 프로덕션 빌드에선 다른 라이브러리의 도움을 받습니다.
	- ex) tenser
		- tenser도 마찬가지로 side effect유무를 판단하여 코드를 지우는데 이때 터서의 판단을 돕는데 pure annotation입니다.
		- /*#__PURE__*/ pure annotation 주석을 확인하면 그 코드는 side effect가 없다고 판단합니다.
	- babel은 pure annotation을 붙여주지만 아직 typescript는 붙여주지 않는다. 따라서 가급적이면 babel을 이용해 컴파일하시는것을 권장한다.
	- react사용하면 babel-plugin-transform-react-pure-annnotation덕분에 pure annotation이 자동으로 삽입되므로 react component를 라이브러리로 만들었다면 특히나 유용합니다.
	- tree shaking을 잘지원하기 위해선 이처럼 툴설정도 유의해야합니다.

## Webpack stats
- 문제원인 찾기
	- 의도와 다르게 side effect가 발생한다면 이를 찾는건 까다로움
		- 현재 가장 좋은 방법은 webpack의 stats기능을 이용하는것입니다.
	- webpack-cli를 쓴다면 stats옵션을 이용하면 되고 nextjs이용하면 아래와 같은 플러그인을 추가하면 웹팩이 번들링 도중에 분석한 다양한 정보를 json포맷으로 저장할 수 있습니다.
		- json파일을 webpack analyse에 올리면 모듈과 모듈의관계를 분석할 수 잇습니다.
			ex) big.js가 모든 번들에 포함되어있었는데 webpack stats로 찾아 side effect가 발생한 곳을 수정
## 라이브러리 영향 줄이기
- 라이브러리 용량을 더이상 줄이기 어렵다면
- Single Common Chunk
- 단일 청크나 vendor/유저청크 두가지의 output으로 웹페이지를 운용하시는 분들도 계실겁니다.
	- ex) @nivo/pie를 한두페이지에서만 사용하나 모든 페이지에서 증가하는 현상이 있었음
- 이런 문제를 해결하기 위해 nextjs는 구글의 제안에 따라 Framework(React, React Dom, ...), Commons(모든 코드를 사용하는 모든 페이지에 받아짐), Shared AB(2페이지 이상 이용하는 shared 청크), Page A, B, C(특정 페이지만 사용하는 청크)로 나누고 있습니다.
	- 이렇게 나누면 영향을 최소화할 수 있습니다.

## Chunks
- Dynamic Import
	- 필요할때만 받는 dynamic import입니다.
```

import dynamic from 'next/dynamic';
const PageA = dynamic(() => import("./PageA"));
const PageB = dynamic(() => /_ webpackPrefetch: true _/ import("./PageB"));

```
- 용량이 큰 라이브러리의 영향을 줄이는 또다른 방법 중 필요할때만 받는 dynamic import입니다. webpackPrefetch 기능을 이용하면 prefetch기능을 이용할 수 있다.
	- ex) 토스팀에서는 최대 1/3의 용량을 가진 번들을 만들고 적절한 DI와 Prefetch를 이용해 초기 로딩 속도를 절반 가까이 줄일 수 있었습니다.

## PPT Link
- https://static.toss.im/slash21/pdf/[%ED%86%A0%EC%8A%A4_SLASH%2021]%20JavaScript%20Bundle%20Diet_%EC%9D%B4%ED%95%9C.pdf

## My Opinion
- 번들 사이즈 최적화에 관한 유용한 정보(툴, tree-shaking를 잘하는 방법)가 많다.
- 일단 프로젝트 내 분석하는게 첫번째이고 줄일 수 있는 포인트를 탐색하는 시간이 필요할 듯 보인다.
- typescript에선 현재도 pure annotation을 지원하지 않는가?
	- 따로 나와있는 정보가 없는것보니 babel을 이용해야할듯 싶기도하다.
- babel을 사용한다면 nextjs swc기능에 제한이 있기에 라이브러리 만드는 용도에서만 사용해야할듯 싶기도하다.
- 번들 최적화는 프로젝트 규모따라 최적화 작업이 여러가지 발생할테지만 결국 라이브러리 의존도가 얼마나 있으냐에 따라 번들 사이즈 작업량이 달라지는 듯하다.
```
