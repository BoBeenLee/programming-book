
# React
- https://ko.reactjs.org/docs

## Portals
- https://ko.reactjs.org/docs/portals.html
- Portal은 부모 컴포넌트의 DOM 계층 구조 바깥에 있는 DOM 노드로 자식을 렌더링하는 방법을 제공합니다.
- portal이 DOM 트리의 어디에도 존재할 수 있다 하더라도 모든 다른 면에서 일반적인 React 자식처럼 동작합니다.
  - Portal을 통한 이벤트 버블링이 가능합니다.

### Usecase
- 유스케이스는 부모 컴포넌트에 overflow: hidden이나 z-index가 있는 경우이지만, 시각적으로 자식을 “튀어나오도록” 보여야 하는 경우, 모달, 다이얼로그, 호버카드, 툴팁, 스낵 메시지바가 해당 부분을 의미합니다.


## 웹 컴포넌트와 리액트의 차이점
- 웹 컴포넌트는 재사용할 수 있는 컴포넌트에 강한 캡슐화를 제공
- React는 데이터와 DOM을 **동기화**하는 선언적 라이브러리를 제공