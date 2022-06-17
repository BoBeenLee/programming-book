
## Module Pattern

- https://www.patterns.dev/posts/module-pattern/
- https://betterprogramming.pub/understanding-the-difference-between-named-and-default-exports-in-react-2d253ca9fc22#:~:text=Combining,both%20default%20and%20named%20components.


- named exports
	- Opt-in Aliasing
	- Multiple Exports Per File
	- Typescript Benefits
		- index.ts로 통합하여 named exports를 내보낼 수 있습니다.
```ts
import { multiply, subtract, square } from "./math.js";

```
	- Inside index.ts, export everything from each file in the directory.
	```ts
		export * from "./buttons";
		export * from "./inputs";
	```


- default exports
```ts
import addValues from "./math.js";

```
- Default Aliasing
	- default export를 한다면 어떤 이름이든지 네이밍 가능하다.
- Single Export
	- 오직 하나만 default export가능하다.

- all exports from a module, meaning all named exports and the default export
	- 불필요한 임포트까지 하기에 주의해야한다.
```ts
import * as math from "./math.js";

math.default(7, 8);
math.multiply(8, 9);
math.subtract(10, 3);
math.square(3);
```

### Dynamic import
- 파일 상단에 모든 모듈을 임포트할때, 먼저 로드됩니다. 몇몇 경우에는 조건에 따라 오직 임포트되기를 원할 수 있습니다.(on-demand)
- 동적 임포트를 해당 요구에 맞게 임포트할 수 있습니다.
- 동적 임포트 모듈에 의해 페이지 로드타임을 줄일수 있습니다.
- 유저가 필요할때, 유저가 필요한 코드를 load, parse, compile 할 수 있습니다.
ex) 유저가 클릭 후 각각의 이미지는 num 기반으로 로드됩니다. 
```
const res = await import(`../assets/dog${num}.png`);
```
해당 방법은 모듈 패스에 의존적이지 않고 유연성을 부가합니다. 
유저 입력 기반으로 외부에서 소스를 받고 모듈을 임포트할 수 있습니다.

### Result
- 모듈 패턴으로 우리의 코드를 공개적으로 노출되지 않는 부분을 **캡슐화**할 수 있습니다.
- 우발적인 이름 충돌과 전역 범위 오염?을 방지하여 여러 종속성 및 네임스페이스 작업을 덜 위험하게 만듭니다.
- 모든 JavaScript 런타임에서 ES2015 모듈을 사용하려면 Babel과 같은 변환기가 필요합니다.

### Usecase
- 도메인 기반으로 컴포넌트 분류, 유틸 기능별로 js파일 분리하여 임포트 등등
- Dynamic Import 예시 
	- 컴포넌트 단위로 Lazy Loading
	- 해당 화면 접근했을시 외부 js 라이브러리, 이미지 로딩

### My Opinion
- 가급적이면 Named Exports를 하는것을 선호하는 편입니다.
	- https://www.bundleapps.io/blog/use-named-exports-over-default-exports-in-javascript
	- Explicit over implicit
		- 명시적인 임포트 선언
	- Refactoring actually works
		- rename 리팩토링할 경우 유용하다.
	- Codebase look-up
		- 가져온 특정 함수 또는 변수를 검색하는 것이 간단해집니다. 네임 기반으로 찾으면 되므로
	- Better Tree Shaking 
		- 빌드 프로세스 동안 번들에서 사용하지 않는 코드를 제외하고 모듈에서 각 개별적으로 임포트 할 수 있습니다.
