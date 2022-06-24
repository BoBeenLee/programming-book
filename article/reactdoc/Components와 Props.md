

# Components와 Props
- https://ko.reactjs.org/docs/components-and-props.html

## State and Lifecycle
- props는 읽기 전용입니다.
- 데이터는 아래로 흐릅니다

QA
- state batch 영역에 대해서
	react17에선 browser events and Hooks 만 가능했었음.

	react18 이후부턴 아래 부분까지 automatic batching 기능을 사용할 수 있다.
	- Event Handlers
	- Hooks
	- Asynchronous Operations
	- Timeouts

## 이벤트 처리하기

## State 끌어올리기
- 하위 두컴포넌트 입력값이 서로 동기화된 상태를 원할때가 있음 ex) 화씨, 섭씨 입력 컴포넌트
- 가장 가까운 공통 조상으로 state를 두어 끌어올림을 이뤄낼 수 있습니다.
- 변경이 일어나는 데이터에 대해서는 source of truth를 하나만 두어야한다.
- 작업순서는 그값이 필요한 컴포넌트 state에 작성하고 다른컴포넌트도 역시 필요할 경우 가장 가까운 공통 조상으로 끌어올리는 식으로 작업하면된다.

QA
- props drilling이 발생할 수도 있는데 어떻게 해결가능할것인가?
	- context, state management

## 합성 (Composition) vs 상속 (Inheritance)

- React는 강력한 합성 모델을 가지고 있으며, 상속 대신 합성을 사용하여 컴포넌트 간에 코드를 재사용하는 것이 좋습니다.
- 범용적인 ‘박스’ 역할을 하는 Sidebar 혹은 Dialog와 같은 컴포넌트에서 특히 자주 볼 수 있습니다.

- 특수화: 더 “구체적인” 컴포넌트가 “일반적인” 컴포넌트를 렌더링하고 props를 통해 내용을 구성




## React로 사고하기

- 목업으로 시작하기
1. 1단계: UI를 컴포넌트 계층 구조로 나누기
어떤것이 컴포넌트가 되어야하나요? 
새로운 함수, 객체 만들때처럼 만들면되지만 한 가지 테크닉은 단일 책임 원칙입니다.

2. 2단계: React로 정적인 버전 만들기
- 보통은 스토리북을 이용하여 만듦

3. 3단계: UI state에 대한 최소한의 (하지만 완전한) 표현 찾아내기
- 애플리케이션에서 필요로 하는 변경 가능한 state의 최소 집합을 생각해보아야 합니다. 여기서 핵심은 중복배제원칙입니다.
  - 객체지향적인 스토어 설계를 하면 대부분 해결할 수 있음.

4. 4단계: State가 어디에 있어야 할 지 찾기
애플리케이션이 가지는 각각의 state에 대해서

- state를 기반으로 렌더링하는 모든 컴포넌트를 찾으세요.
- 공통 소유 컴포넌트 (common owner component)를 찾으세요. (계층 구조 내에서 특정 state가 있어야 하는 모든 컴포넌트들의 상위에 있는 하나의 컴포넌트).
- 공통 혹은 더 상위에 있는 컴포넌트가 state를 가져야 합니다.
- state를 소유할 적절한 컴포넌트를 찾지 못하였다면, state를 소유하는 컴포넌트를 하나 만들어서 공통 오너 컴포넌트의 상위 계층에 추가하세요.

5. 5단계: 역방향 데이터 흐름 추가하기

- onChange 이벤트를 사용해서 state에 업데이트하도록 callback을 넘겨서 전달해준다.

재사용, 캡슐화, 단방향식 데이터 흐름, 상속, 특수화, 확장성, 단일 책임 원칙
