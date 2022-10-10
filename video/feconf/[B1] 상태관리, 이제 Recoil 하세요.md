# [B1] 상태관리, 이제 Recoil 하세요.
- https://www.youtube.com/watch?v=0-UaleJZOw8

## Recoil의 핵심 컨셉
- 오직 React만을 위해 React처럼
- React 내부 상태만 이용
- 작은 Atom 단위로 관리
- 순수함수 Selector
- Re-Render 최소화
- 데이터 흐름을 따라서
- 곧 새로운 React기능과 호환성

## 예제로 보는 Recoil활용

### Modal
```
export const modalState = atom({
	key: 'modalState',
	default: false,
});

```

```

function List() {
	const [modalOpen, setModalOpen] = useRecoilState(modalState);
	const handleRegister = () => {
		setModalOpen(true);
	} // hooks처럼 호출해서 사용
}
...
```

### List
```
export const productsState = atom({
	key: 'productsState',
	default: {
		idx: 0,
		name: '',
		category: '',
		brand: '',
		price: 0,
		desc: '',
	}
});

```

```
// useRecoilValue 읽기전용
function ProductList() {
	const list = useRecoilValue(productsState);

	return list && ...
}
...
```

### Register

```
function RegisterModal() {
	const [formData, setFormData] = useState();
	const setList = useSetRecoilState(productsState);
	const setIsOpen = useSetRecoilState(modalState);

	const handleChange = (e) => {
		setFormData({
			...formData,
			[e.target.name]: e.target.value,
		});
	};

	const handleSubmit = async (e) => {
		e.preventDefault();
		setList((prev) => [...prev, formData]);
		setIsOpen(false);
	};

	return ...
}
```

### Detail

```
function Product({data}) {
	const list = useRecoilValue(productsState);
	const setProduct = useSetRecoildState(productState);

	const handleDetail = (idx) => {
		setProduct(list.filter((row) => row.idx === idx)[0]);
		setRegisterOpen(true);
	}

	return data && ...
}

```

### Update

```
function RegisterModal({data}) {
	const [list, setList] = useRecoilState(productsState);
	const product = useRecoilValue(productState);
	const resetProduct = useResetRecoilState(productState);

	...

	const handleSubmit = async (e) => {
		e.preventDefault();
		if(product) {
			let newList = list.map((row) => {
				if(row.idx === product.idx) {
					return product;
				}
				return row;
			});
			setList(newList);
		}
		setRegisterOpen(false);
	}

	useEffect(() => {
		return () => {
			resetProduct();
		}
	}, []);

	return <input type="text" name="name" defaultValue={product?.name} onChange={handleChange} />
}

```

### Selector

```
function selector<T>({
	key: string,
	get: ({
		get: GetRecoilValue,
		getCallback: GetCallback,
	}) => T | Promise<T> | RecoilValue<T>,
	set?: ({
			get: GetRecoilValue,
			set: SetRecoilState,
			reset: ResetRecoildState,
		}, 
		newValue: T | DefaultValue,
	) => void,
})

```
### Read-only/Writable
- gettter는 필수
- Selector (get/set) - useRecoildState, useRecoilValue, useSetRecoilState, 
	- 네이밍을 직관적으로 ex) listState
- Selector (get) - useRecoilValue
	- 네이밍을 직관적으로 ex) listReadOnlyState
	
### Filtered List
```
export const filteredProductsState = selector({
	key: 'filteredProductsState',
	get: ({ get }) => {
		const filter = get(filterState);
		const list = get(productsState);
		// 상호 의조성
		// 구독중인 State가 변경
		// -> Selector재평가
		// -> 참조 컴포넌트 Re-Render

		if(!filter) {
			return;
		}
		if(filter.brand) {
			list = list.filter(row => filter.brand === row.brand);
		}
		if(filter.category) {
			list = list.filter(row => filter.category === row.category);
		}
		return list;
	}
})

```

## 비동기 데이터 다루기
### 실제 서버 데이터를 가져와보자

```
const productsAynsState = selector({
	key: 'productsAsyncState',
	get: async ({ get }) => {
		const filter = get(filterState);
		return await getProductList(filter);
	}
})

const getProductList = async (options) => {
	// fetch product list
}

```

### 상세 데이터 조회
```
export const productIdxState = atom({
	key: 'productIdxState',
	default: 0
})

export const productAsyncState = selector({
	key: 'productAsyncState',
	get: async ({ get }) => {
		const idx = get(productIdxState);
		return idx > 0 ? await getProductDetail(idx) : null;
	}
})

```
#### Family

```
// Family는 매개변수 전달가능
export const productAsyncState = selectorFamily({
	key: 'productAsyncState',
	get: ({ idx }) => async ({ get }) => {
		return idx > 0 ? await getProductDetail(idx) : null;
	}
})
```

### Suspense는 실험적? Recoil에서는 적극 권장
- 비동기 요청에러가 뜰 경우 Suspense를 이용하라고 에러가 뜨게된다.
- Suspense가 싫다면 Loadable을 이용하여 구현
```
<Suspense fallback={<Indicator type="small" />}>
	<ProductList />
</Suspense>
```

### Error Handling
```
<RecoilRoot>
	<ErrorBoundary>
		<Suspense fallback={<Indicator type="small" />}>
			<ProductList />
		</Suspense>
	</ErrorBoundary>
</RecoilRoot>
```
- 두번째 방법으론
```
const listLoadable = useRecoilValueLoadable(listAsyncState);
switch(listLoadable.state) {
	case 'hasValue':
		return listLoadable.contents:
	case 'loading':
		return <Indicator />;
	case 'hasError':
		throw <Error />;
}
```

## 한번 사용한 API를 다시 호출한 경우
- Server-Client 모델의 근본적인 문제
  - ex1) 찜한 상품이 마이페이지에 반영이 안되요
  - ex2) 다른 사람이 추가한 게시글이 내 앱에는 안보여요!
  - ex3) 배송중이라는 문자를 받았는데 앱에서는 아직도 준비중이네요?
- 데이터를 가져오는 시점과 실제 데이터를 사용하는 시점이 다르기때문에 발생함
	- 주기적으로 동기화하는 방식을 채택하기도함
		- 이러한 방색은 웹환경에서는 생산성, 성능까지 챙길 수 없는 방법이다.
## 비동기 데이터를 갱신하는 방법들
### 비동기 데이터 갱신에 영향을 주는 요소
- 내부에서 구독중인 다른 Recoil state의 변경을 감지한 경우
- 요청 파라미터가 완전 새로운 값으로 변경된 경우

### Recoil이 제안한 Request ID를 이용한 명시적 갱신
```
export const productReqIDState = atom({
	key: 'productReqIDState',
	default: 1
})

export const productAsyncState = selector({
	key: 'productAsyncState',
	get: async ({ get }) => {
		const idx = get(productIdxState);
		get(productReqIDState); // 의존성 주입
		return idx > 0 ? await getProductDetail(idx) : null;
	}
})

function useRefreshProductAsyncState() {
	const setProductID = useSetRecoilState(productReqIDState);
	return () => {
		setProductID(id => id + 1);
	}
}

function RegisterModal() {
	const refreshProductState = useRefreshProductAsyncState();
	const handleSubmit = async (e) => {
		e.preventDefault();
		if(data.idx > 0) {
			refreshProductState();
		}
		setRegisterOpen(false);
	}
	...
}
```

### Setter를 활용한 개선 버젼

```
export const productReqIDState = atom({
	key: 'productReqIDState',
	default: 1
})

export const productAsyncState = selector({
	key: 'productAsyncState',
	get: async ({ get }) => {
		const idx = get(productIdxState);
		get(productReqIDState); // 의존성 주입
		return idx > 0 ? await getProductDetail(idx) : null;
	},
	set: ({ set }) => {
		// Refresh Hooks대신 setter
		set(productReqIDState, (id) => id + 1);
	}
})

function RegisterModal() {
	const [productState, setProductState] = useRecoilState(productAsyncState);
	const handleSubmit = async (e) => {
		e.preventDefault();
		if(data.idx > 0) {
			// 상태 변경이 없는 set실행
			setProductState(productState);
		}
		setRegisterOpen(false);
	}
	...
}

```

### Atom 구독 공유시 주의점

```
A Selector  -> A Component -> Atom -> A Selector 
B Selector -> B Component 
```
- 의존 관계를 갖는 상태끼리 파일로 관리하거나 or atomFaily를 이용하여 그룹화할 수 있는 값을 매개변수로 받아서 그룹핑하는 방법도 생각할 수 있다.
- Private으로 정의
- RecoilRoot 분리
- Family로 Grouping


### 데이터 갱신하는 다른 방법
```
const userInfoState = atomFamily({
	key: 'UserInfo', // Selector 대신 Atom으로 데이터 관리
	default: userId => fetch(userInfoURL(userId))
})

function RefreshUserInfo(userId) {
	const refreshUserInfo = useRecoilCallback(({ set }) => async id => {
		const userInfo = await myDBQuery({ userId });
		set(userInfoState(userId), userInfo)
	}, [userId])

	useEffect(() => {
		const intervalId = setInterval(refreshUserInfo, 1000);
		return () => clearInterval(intervalId);
	}, [refreshUserInfo])
	// useEffect에 설정한 조건에 따라 useRecoilCallback을 이용해 데이터 갱신하는 로직	
	return null;
}
```

### 명시적 / 주기적 업데이터
- 프로필, 보유 상품, 찜한 상품
	- 내 Event만 영향주는 데이터 -> 명시적 업데이트 필요
- 판매 내역, 구매 내역, ...
	- 언제 변경될지 모르는 데이터 -> 실시간/주기적 업데이트 or No-Cache or Recoil X


### Version Param을 이용한 주기적 갱신
- 고전적이지만 확실한 Cache Control
- 1분 / 30초 / 1시간 세부 설정 가능

```
export const productReqIDState = atom({
	key: 'productReqIDState',
	default: 1
})

export const productAsyncState = selectorFamily({
	key: 'productAsyncState',
	get: ({ ver }) => async ({ get }) => {
		const idx = get(productIdxState);
		return idx > 0 ? await getProductDetail(idx, ver) : null;
	}
})

function getVersion() {
	return 'YMDHMS';
}
const data = useRecoilValue(productAsyncState({ ver: getVersion() }))
```
- useEffect로 version변경
	-> 데이터 변경 시점 차이 발생
	-> 더블링 발생!
- New Data(), Timestamp
	-> 무한 요청...

### 올 7월에 캐싱을 컨트롤할 수 있는 기능을 추가한다는 얘기


## 마무리
- Recoil이 강조하는 핵심은 데이터 플로우 그래프를 잘설계해서 의존성을 갖는 여러 상태들을 체계적으로 관리하라는것 같습니다.

### 초기 설계시 고려할 점
- 꼭 전역으로 관리되야만 하는가?
	-> 간단한건 hooks, props로 충분
- 여러 상태값을 사용 용도에 따라 분류
	-> UI전용 상태 / 폼데이터 처리 상태 / 서버 데이터 조회용 상태
- 어떤 데이터를 캐싱하고, 실시간으로 반영되야 하는지 파악
	-> 캐싱: 코드성 데이터, 사용자 정보 등 / 주기적: 자주 바뀌지 않는 정보 / 실시간: 주요 데이터
- 데이터가 어느 시점에서 변경되고 어떤 부분에 영향을 주는지 예측

### 이외
- constSelector, errorSelector
- Multiple<RecoilRoot>
- Concurrent Request - waitFor*()
- Pre-Fetching Snapshot
- ...
