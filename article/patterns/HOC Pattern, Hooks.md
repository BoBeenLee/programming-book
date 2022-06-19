
# HOC Pattern, Hooks
- https://www.patterns.dev/posts/hoc-pattern/

앱내에 컴포넌트 간에 재사용가능한 속성들을 내려주기 위해 사용합니다.

- 앱내에 다수의 컴포넌트에서 같은 로직을 사용합니다.
	- 스타일링 적용, 인증, 글로벌 상태를 추가하는 부분들..
- 같은 로직을 재사용하는 방법으로 higher order component패턴이 있습니다.

ex) 로딩 HOC

## Composing
- 다수의 HOC 컴포넌트들을 구성할 수 있습니다.
ex) withHover(withLoader(TargetComponent))

## Hooks
- 경우에 따라 훅은 HOC 패턴을 대체할 수 있다.
- ex) withHover -> useHover

- 보편적으로 훅은 HOC패턴을 대체할 수 없다하지만 대부분의 경우 훅만으로 충분하며 당신의 감싸진 컴포넌트 트리를 줄이는데 도움줄 수 있습니다.
- 훅을 사용함으로서 컴포넌트 트리의 깊이를 줄여줍니다.
ex) 
```
<withAuth>
  <withLayout>
    <withLogging>
      <Component />
    </withLogging>
  </withLayout>
</withAuth>
```
현재 모든 로직을 유지하면서 HOC를 사용하면 많은 컴포넌트에 같은 로직을 제공할 수있습니다. 
훅은 컴포넌트 내에 커스텀한 행동(useHover와 같은)을 추가하여 행할 수 있습니다.
이 행동이 다수 컴포넌트에 의존하고 있다면 HOC패턴과 비교하여 소개하는 잠재적 위험이 증가할겁니다.

### HOC Usecase
- 같은 행동, 커스텀하지 않는 행동을 컴포넌트들에게 사용될때
- 추가적인 커스텀 로직 없이 독립적으로 작동하는 부분이 필요할때

### Hooks Usecase
- 사용하는 각 컴포넌트 위한 커스텀한 행동을 해야할때?
- 앱내에 전체적으로 퍼져있지 않고 오직 하나, 몇몇 컴포넌트에 사용할때
- 컴포넌트에 행동에 의해서 많은 속성들을 추가해야할때

### Case Study
- ex) Apollo Client
- graphql() HOC를 통해 이용가능한 클라이언트 데이터를 만들 수 있습니다.
	- this.props.mutate ...

- useMutation 훅을 사용하여 데이터를 제공할때 필요한 많은양의 코드를 줄일 수 있습니다.
- 보일러플레이트 감축과 다양한 resolvers 데이터를 쉽게 이용할 수 있습니다.
- HOC compose대신에 다양한 hooks를 간단하게 사용할 수 있습니다.
- 더 작은 조각(hook)들로 나누어 있어 컴포넌트 리팩토링할때 개발자 경험을 개선할 수 있습니다.

### Pros
- HOC를 사용하여 한 장소에 재사용 가능한 로직을 유지할 수 있습니다.
- 중복된 코드에 의한 버그의 위험을 줄일 수 있습니다.
- DRY(do not repeat yourself)를 유지하며 관심사의 분리를 행합니다.

### Cons
- HOC는 props전달할때 네이밍 충돌 원인을 유발시킬 수 있습니다.
	- HOC withStyle에서 style속성을 전달하는데 Button 컴포넌트에서 이미 style속성을 사용할때, 머지하거나 rename해야합니다.
		- 해당 부분 감지하기 어려울 수 있습니다.
- 다수의 컴포즈된 HOCs를 사용할때 HOC에 전달받은 props 책임들이 불명확하여 어떤 HOC에서 온 props인지 인지하기 어렵습니다. 이는 디버깅 및 애플리케이션 확장을 쉽게 방해할 수 있습니다.

## My Opinion
- 다양한 곳에 쓰임 fetch, auth, style 등등