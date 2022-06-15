# patterns
- https://www.patterns.dev/posts/introduction/

## Singleton Pattern
- Share a single global instance throughout our application
    - Singletons are classes which can be instantiated once, and can be accessed globally.

- 하나의 객체로 글로벌로 접근할 수 있다.
- **오직 한번**만 생성되어야한다.

- Object.freeze를 통해 싱글톤 객체의 추가, 수정하여 overwritinge되는 리스크를 줄인다.

### 장점
- 메모리 절약
  - 싱글톤으로 하나의 객체만 생성하므로
- javascript에서는 object로 간단하게 singleton을 정확히 구사할수 있다.
- 테스팅면에선 각 테스트마다 객체를 생서할 필요가 없다.
  - 테스트 시간 절약
- 전체 앱에 접근이 가능하다.

### 단점
- Singletons are actually considered an anti-pattern, and can (or.. should) be avoided in JavaScript.
- 다양한 언어에선 javascript 구현방법대로 직접적으로 구현이 어려움
- Dependency hiding
  - 싱글톤을 임포팅함이 분명하지 않아 예기치 않은 행동으로 다른 값을 변경할 수 있다.
- 글로벌에 접근할 수 있어서 object수정이 예기치 않은 행동으로 이끌수 있음.

### State management in React
- Redux, React Context 사용하라
- 해당 툴들은 싱글톤과 유사하게 행동하며 read only state로 제공한다.
  - 다만 redux는 action through a dispatcher 보낸 후 reducers를 통해서 state를 업데이트할 수 있다.

### Usecase
- Firebase Event, remoteConfig 호출 등등
  - firebase 객체 config 설정은 객체가 호출될때 한번 설정(initialize) 하고 설정된 객체를 전달해주면 되므로 singleton으로 적합하다.
- google-cloud/storage 설정
  - 파일 업로드, 다운로드 설정도 한번 설정하고 해당 설정이 도중에 바뀌는 경우가 없기에

### My Opinion
- 싱글톤 객체에 수정이 필요 없고 event, logging, notify과 상호작용이 필요없는 객체에 유용할듯 싶다.

