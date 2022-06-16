## Prototype Pattern
- https://www.patterns.dev/posts/prototype-pattern/

- Prototype Pattern은 같은 타입 객체들사이에 속성들을 공유하기 위한 방법입니다.
- 객체에 직접 존재하지 않는 객체의 속성에 액세스하려고 할 때마다 JavaScript는 프로토타입 체인 내에서 해당 속성을 사용할 수 있는지 확인하기 위해 프로토타입 체인으로 이동합니다.
	- 객체에서 직접 사용할 수 없는 속성에 액세스하려고 할 때 JavaScript는 속성을 찾을 때까지 __proto__가 가리키는 모든 객체를 재귀적으로 안내합니다

- 자바스크립트 관련 프로토타입 패턴 상세 내용은 아래 부분을 보는것이 좋을듯하다.
	- 클래스 상속, 프로토타입 상속
	    - literal prototype inheritance: [https://ko.javascript.info/prototype-inheritance](https://ko.javascript.info/prototype-inheritance)
	    - function prototype inheritance: [https://ko.javascript.info/function-prototype](https://ko.javascript.info/function-prototype)
