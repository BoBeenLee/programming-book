
# Render Props Pattern
- https://www.patterns.dev/posts/render-props-pattern/

- HOC섹션에서 재사용성에 대해서 알아보았었다.
- render props패턴을 사용한 재사용성 높은 컴포넌트를 만드는 또다른 방법이다.
- render prop는 컴포넌트 속성에 함수 값 엘레멘트를 전달하는 방법이다.
	- 자신이 구현한 렌더로직 대신에 render 속성을 호출합니다.
```
<Title render={() => <h1>I am a render prop!</h1>} />
```

- 왜사용하는것일까?
- 단순히 render prop를 호출하는것 이상의 일을 합니다. 대신, 우리는 일반적으로 render prop을 받는 컴포넌트에서 render prop으로 전달하는 요소로 데이터를 전달하기를 원합니다

### Lifting state

- 온도 변환기 예시 Fahrenheit and Kelvin 컴포넌트는 유저 입력을 받기 위해선 lift the state를 해야합니다.
- Input 컴포넌트가 상태를 가지고 있는 대신에 공통 조상인 App 컴포넌트로 상태를 올리고 state value를 연동합니다.
- 규모가 큰앱 내에 lift state는 tricky한 요소이며 상태값이 변할때마다 모든 자식들이 리렌더링 될것입니다. (state를 이용하지 않는 상태조차도)

### Render props

- render props를 받는 Input 컴포넌트로 변경하였습니다.
- Kelvin, Fahrenheit 컴포넌트는 유저 입력값을 접근할 수 있습니다.
- lift state로 발생한 모든 자식들에 리렌더링 되지 않고 Input, Input render props로 전달된 Kelvin, Fahrenheit 컴포넌트만 렌더링되여 불필요한 렌더링을 줄여줍니다.

### Children as a function

- render props형태로 children props에 함수를 전달할 수 있습니다.

```
<Title>{() => <h1>I am a render prop!</h1>}</Title>
```

### Hooks
- 몇몇 경우에는 render props는 훅으로 대체됩니다.
	- ex) Apollo Client

- HOC graphql() 대신에 Mutation 컴포넌트로 render prop를 받습니다.
- 훅의 사용 예시는 HOC 섹션과 동일합니다.


### 장점
- 재사용성이 높으며, HOC가 같은 이슈를 해결하지만 재사용성 및 데이터 공유인 render props 패턴은 HOC 패턴을 사용하여 발생할 수 있는 몇 가지 문제를 해결합니다.
	- 이름 충돌 이슈는 render props 패턴으로 해결할 수 있습니다.
	- 명확한 props를 child 컴포넌트에 전달합니다. (HOC props 전달시 불명확한 props 전달이슈를 해결해줍니다.)
- render props를 통해 앱로직을 분리합니다.
	- render prop을 받은 상태 컴포넌트는 데이터를 stateless 컴포넌트로 전달합니다.
### 단점
- 대부분 React Hooks로 대체되었습니다.
- Hooks가 컴포넌트에 재사용성과 데이터 공유를 추가하는 방식을 변경함에 따라 Hooks는 많은 경우에 render props 패턴을 대체할 수 있습니다.
- render prop를 라이프 사이클 메소드에 추가할 수 없기에 받은 데이터가 바뀔 필요가 없는 컴포넌트에서만 사용합니다.
	- 다만 다시 리렌더링하라라는 어떠한 다른 props를 전달하는 방법으로 리렌더링할 수 있습니다.

