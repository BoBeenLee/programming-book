## Container-Presentational Pattern
- 앱 로직으로부터 뷰 분리하여 **관심사의 분리**합니다.

1. Presentational Components
	- 사용자에게 어떻게 데이터를 보여줄것인가
	- props로 데이터를 받고 받은 데이터를 조작(mutate)하는 것이 아닌 스타일적 요소를 포함하여 보여주는것이 주된 기능
	- 일반적으론 stateless, UI 목적이 아니라면 state를 포함하지 않는다.
	- container components 로 부터 데이터를 받는다.

2. Container Components
	- 어떤 데이터를 사용자에게 보여줄 것인가
	- presentational components에게 데이터를 전달하는것이 주된 기능
	- 스타일 요소를 포함하지 않으며 presentational components 외 다른 요소를 렌더링하지 않습니다.

## Hooks
- Hooks의 도입으로 개발자는 해당 상태를 제공하는 컨테이너 구성 요소 없이도 상태를 쉽게 추가할 수 있습니다.
- Hooks는 Container/Presentational pattern 처럼 뷰와 로직을 쉽게 분리합니다. 기존 Container 레이어(extra layer)를 줄여주는 효과를 가지고 있습니다.

```
export default function useDogImages() {
  const [dogs, setDogs] = useState([]);

  useEffect(() => {
    fetch("https://dog.ceo/api/breed/labrador/images/random/6")
      .then(res => res.json())
      .then(({ message }) => setDogs(message));
  }, []);

  return dogs;
}
```

## 장점
- 관심사의 분리
	- Presentational components는 UI 책임을 맡고
	- Container components는 앱 데이터와 상태의 책임을 가진다.
- Presentational components 재사용성이 높아진다.
- Presentational components 모양은 코드베이스 지식(비즈니스 로직) 없이 쉽게 바꿀 수 있다.
- presentational components 테스트도 쉬워진다. (pure function이기에)

## 단점
- 렌더 로직에서 앱로직을 분리하는 것은 쉬우나 Hooks는 Container/Presentational pattern 사용 없이 같은 결과를 만들어낼 수 있다.

### Usecase
- 예전 redux를 사용하고 있는 프로젝트는 거의 대부분 Container/Presentational pattern을 사용하였다.

### My Opinion

- Container/Presentational가 아닌 Hooks를 이용하여 React-Query, SWR를 통한 데이터 호출이 일반적인 방법인듯 싶다.
  - 다만 Container/Presentational pattern을 사용한다면 현재 기능 장황한 코드 작성과 extra layer를 만들어야하는 이슈가 있다.
- Remix 기준으로 봤을땐 Container components 역할을 Nested Route가 대체할 수 있을듯 싶다.
  - https://youtu.be/95B8mnhzoCM?t=669
