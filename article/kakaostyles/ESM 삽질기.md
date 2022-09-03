# ESM 삽질기

- https://devblog.kakaostyle.com/ko/2022-04-09-1-esm-problem/

## 발생하는 문제

- chalk 란 모듈이 5.0으로 가면서 Pure ESM 모듈이 됐습니다. 이를 가져다 쓰면 다음과 같은 에러가 발생합니다.

## ESM이란 무엇인가?

ESM 이전엔 CommonJS를 이용해왔었습니다.
다만 CommonJS의 가장 큰 문제는 런타임에 모듈을 읽는 다는 것입니다.
런타임으로 모듈을 읽기에 순환 참조가 발생하는 경우, 해당 모듈을 다시 읽으려할떄 읽혀지지 않아 undefined와 같은 비어있는 값을 반환하게 됩니다.
그리고 또 async/await 문법이 나온 이후에 가장 아쉬운 점 중 하나가 최상위 단계에서 await가 불가능하다는 것입니다.
IIFE를 사용해야했었고 CommonJS의 한계로 인한 것이고 ESM에서는 가능해졌습니다.
따라서 CommonJS의 단점을 보완하여 나온 부분이 ESM
문제는 CommonJS 프로젝트에서는 ESM 모듈을 불러오는 것이 불가능하다는 것에 있습니다. 따라서 프로젝트가 ESM으로 전환해야지만 Pure ESM 모듈을 사용할 수 있습니다.

## JS JavaScript에서 Pure ESM 모듈을 읽기 위한 방법

- .mjs 확장자 사용
- 전체 프로젝트를 ESM으로 전환
- dynamic import 사용
