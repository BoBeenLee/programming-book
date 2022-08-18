# 돔하디의 Virtual DOM

- https://www.youtube.com/watch?v=6rDBqVHSbgM&list=WL&index=7

- Virtual DOM 배경
  - SPA가 등장하면서 클라이언트 사이드 렌더링 방식이 많이 사용되면서 현재는 DOM업데이트가 상당히 복잡하게 발생하는 애플리케이션들이 많아졌습니다.
  - DOM 정적인 페이지였을떄에는 크게 문제가 되지 않았지만 클라이언트 사이드 렌더링이 많이 사용되면서 DOM의 동적인 변화가 많이 발생하였고 화면 렌더링 하는 과정의 비효율성을 해결하고 최적화를 할 필요성이 대두되었습니다. 이러한 과정에서 등장한것이 Virtual DOM이 등장하게 되었습니다.
  - DOM조작에 화면을 비효율적으로 렌더링하는 과정을 해결, 최적화하는 과정에서 나온 것인 Virtual DOM
- Virtual DOM
- 실제 DOM의 가벼운 버젼
- 실제 DOM 노드 트리를 복제한 자바스크립트 객체
- Virtual DOM은 실제 DOM과 같은 class, style속성을 갖고 있지만 화면에 변화를 직접 줄수 있는 기능인 getElementById과같은 DOM api들은 갖고 있지 않기 때문이다.
- Virtual DOM의 동작
  - DOM노드에 변화가 생기면 Virtual DOM은 다시 새로운 가상의 DOM트리를 처음부터 다시 만들게됩니다. 이 과정에서 변화가 생길때마다 가상의 DOM트리를 만드는것이 비효율적으로 생각할 수 있다.
    - 하지만 DOM노드를 조작하는 것의 비효율성은 DOM트리를 업데이트하는 과정에서 발생하는 것이 아니라 _렌더링 과정에서 비싼 비용이 드는 것입니다._
      - Virtual DOM은 렌더링하지않고 메모리상에서 트리를 변경하는 일이기에 상당히 빠르게 작업을 진행할 수 있습니다.
  - diff(previous: VTree, current: VTree) => PatchObject
    - Virtual DOM의 내부 구현체를 살펴보면 diff함수에서 매개변수로 이전 상태의 DOM트리와 새롭게 만들어진 DOM트리로 받아오고 변경전,후 DOM트리의 변화된 부분만 확인.
      - 확인 후 실제 DOM에 변경된 부분을 적용.
  - patch(rootNode: DOMNode, patches: PatchObject) => DOMNode newRootNode
    - rootNode, patches를 받아 변경된 사항만을 실제 DOM노드에 적용하여 렌더링과정을 수행합니다.
  - 이와 같은 일련의 과정을 보면 버퍼링, 캐싱의 역할을 한다고 볼 수 있습니다.
  - 브라우저 렌더링 과정을 반복하는 것이 아닌 변화들을 Virtual DOM반영 후 변경된 부분들만 모아서 실제 DOM에 적용하여 한번만 렌더링함으로써 성능 최적화
- React에서의 Virtual DOM
- jsx 자바스크립트를 확장한 문법 따라서 babel과 같은 툴로 js로 변환하여 진행한다.
- jsx html문법을 babel로 변환한후 js객체로 만든후 ReactDOM.render를 통해 DOM에 적용.
- 재조정: 상태가 변화했을때 화면에 Virtual DOM을 활용하여 DOM을 업데이트하는 과정
- 리액트에선 "Virtual DOM은 UI의 이상적인 또는 가상적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 실제 DOM과 동기화하는 프로그래밍 개념"
  - 이 과정을 재조정이라한다.
- 따라서 재조정이란 Virtual DOM과 실제 DOM을 비교하고 일치시키는 과정
- 리액트는 변경전 Virtual DOM과 변경 이후 Virtual DOM 두 트리를 유지하고 있다가 두 트리의 스냅샷을 비교하여 변화된 부분만 감지한 후 변경된 부분만을 실제 DOM에 적용합니다.
- 이 과정중 diffing 알고리즘을 사용하게 됩니다.
  - jsx가 js객체로 변화된 결과값중 type(h1, h2, div)이 변경전 리액트 엘리먼트 타입과 변경 후 리액트 엘리먼트 타입을 비교하여 두가지 다른 유형의 행동을 하게됩니다.
    - type === type? 속성만 변경
    - type !== type? 트리 재생성
- key prop
- key prop은 재조정과 깊은 연관이 있다.
- ex) li태그가 첫번째 위치에 삽입되었을 경우, 재조정에 의해 모든 요소가 제자리에 위치하지 않았다 판단하여 li전부 다시 그리게 된다.
  - 성능 이슈 유발
- 이를 위해서 식별자로 key prop을 제공한다.
- key값으로 이전, 변경 후 트리를 비교하고 재조정하기에 문제없이 첫번째에 li가 추가되어도 문제없이 추가된 노드가 그리게된다.
  - key값은 변경되지 않은 유일한값으로
  - 다만 array index를 주면 새로운 아이템이 맨앞에 추가될때, key값이 0인 새로 추가된 value에 기존 트리에 키값 0인 value값을 그대로 유지하게된다.

## My Opinion

- 재조정 부분을 간단하게 설명하여 React 문서와 곁들어서 보면 딱 좋을듯싶다.
  - https://ko.reactjs.org/docs/reconciliation.html
