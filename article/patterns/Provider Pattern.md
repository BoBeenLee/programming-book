
## Provider Pattern

- 컴포넌트를 props 속성으로 전달하지만 대부분 모든 컴포넌트 props 값 접근이 필요하다면 어려울 것이다.
- prop drilling은 props를 컴포넌트 트리 깊숙히 전달합니다.
- props에 의존하는 리팩토링할 코드들은 대부분 불가능하게 만들고 어디서 데이터가 오는지 알기 어렵게 만듭니다.

- prop drilling이 아닌 데이터를 직접 접근할 수 있는 무언가가 필요합니다.
- Provider는 Context객체가 제공하는 Higher order 컴포넌트입니다.
- createContext메소드를 통해 context객체를 생성합니다.
- Provider는 하위 모든 컴포넌트에 접근 가능한 데이터를 value props에 받습니다.
- useContext hook을 통해 각 컴포넌트에서 데이터를 접근할 수 있습니다.
- 데이터 값을 사용하지 않는 컴포넌트는 더이상 해당 데이터를 다루지 않습니다.

## Hooks
- 각각의 컴포넌트 컨텍스트 설정을 useContext로 설정하는 대신에 커스텀한 훅으로 사용할 수 있습니다.
```
function useThemeContext() {
  const theme = useContext(ThemeContext);
  if (!theme) {
    throw new Error("useThemeContext must be used within ThemeProvider");
  }
  return theme;
}
```
ThemeContext.Provider를 직접 래핑 대신에 Theme값을 제공하는 컴포넌트를 감싸 HOC는 만들수 있습니다. 이 방법으로 렌더링하는 컴포넌트로부터 컨텍스트 로직을 분리할 수 있습니다.
분리함으로 인해 provider 재사용성을 개선합니다.
```
function ThemeProvider({children}) {
  const [theme, setTheme] = useState("dark");

  function toggleTheme() {
    setTheme(theme === "light" ? "dark" : "light");
  }

  const providerValue = {
    theme: themes[theme],
    toggleTheme
  };

  return (
    <ThemeContext.Provider value={providerValue}>
      {children}
    </ThemeContext.Provider>
  );
}

export default function App() {
  return (
    <div className={`App theme-${theme}`}>
      <ThemeProvider>
        <Toggle />
        <List />
      </ThemeProvider>
    </div>
  );
```
### 장점
- 수동적인 props drilling 방식이 아닌 컴포넌트 데이터를 각각의 컴포넌트 레이어에 직접 전달할 수가 있다.
- 코드를 리팩토링할 때 실수로 버그를 도입할 위험을 줄입니다. 이전에는 나중에 prop의 이름을 바꾸려면 이 값이 사용된 전체 애플리케이션에서 이 prop의 이름을 바꿔야 했습니다.
- Provider패턴과 함께 몇몇 다양한 글로벌 상태는 컴포넌트들이 글로벌 상태를 접근할 수 있습니다.

### 단점
- 과남용했을 경우 퍼포먼스 이슈가 발생할 수 있습니다.
	- 각컴포넌트들이 상태변화 context를 consume하여 리렌더링이 발생하기에
- 예시처럼 CounterContext에 Increment, Reset 하는 컴포넌트가 존재한다면 Increment에서 counter가 증가 했을 경우 Reset 컴포넌트 또한 리렌더링되어 동작합니다.
	- 작은 프로젝트에선 중요하진 않으나 큰 프로젝트일 경우 자주 값이 업데이트되어 퍼포먼스에 부정적인 영향을 줄 수 있습니다.
	- 해당 이슈를 해결하기 위해선 각각의 increment provider, reset provider를 만들어 분리하여 생성해야할것입니다.

### Usecase
- Theme UI
	- ex) ThemeProvider
- Locale

### My Opinion
- 대체로 state management(mobx, mobx-state-tree, zustand, jotai)를 이용하여 관리가 가능하므로 따로 React Context를 이용할 필요는 없겠다만 React-Query, SWR, React Server Component를 이용하여 server state관리를 분리하고 global한 영역의 관리도 최대한 줄이고 있는 추세를 보았을땐 state management 라이브러리를 최대한 사용하지 않고 React-Query(server state), React Context(global state)로 관리하는것도 하나의 방법일거 같다.
- Provider, Context 구조로 어떻게 전달할 수 있는지 멘탈모델에 대한 설명을 기대했으나 아니어서 따로 찾아봐야할듯한?