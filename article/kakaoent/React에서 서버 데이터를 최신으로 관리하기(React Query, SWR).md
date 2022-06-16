
# React에서 서버 데이터를 최신으로 관리하기(React Query, SWR)
- https://fe-developers.kakaoent.com/2022/220224-data-fetching-libs/

-  SWR에서 React Query로 변경하는 작업을 진행
	- 개발 컨텍스트를 맞추어 스위칭 비용을 낮추기 위함

일반적으로 사용하는 상태(state) 를 세 가지로 구분
- Local State: 리액트 컴포넌트 안에서만 사용되는 state
- Global State: Global Store에 정의되어 프로젝트 어디에서나 접근할 수 있는 state
- Server State: 서버로부터 받아오는 state

기존에는 리덕스와 같은 상태 관리 라이브러리에 Global State와 Server State를 전부 포함하는 방법으로 프로그래밍<br/>
data fetching 라이브러리를 사용함으로써 상태 관리 라이브러리에서 비동기 로직을 제거하여 관심사가 분리되고 선언적으로 프로그래밍할 수 있게 되었습니다.

## 리덕스에서 Server State를 처리해 봅시다
- redux-thunk, redux-saga를 통한 처리
- 리덕스에서 Global State와 Server State를 하나의 스토어에서 관리하게 되면서 스토어는 점점 비대해지고 관심사의 분리

## SWR & React Query

data fetching 라이브러리는 위에서 말한 리덕스의 단점들을 해결합니다.
- 선언적으로 프로그래밍 할 수 있음(장황하지 않은 코드)
- 동일한 API 요청이 여러 번 호출될 경우 한 번만 실행
- 데이터가 dirty 해진 경우 적절한 시점에 알아서 업데이트
- Global State와 Server State의 관심사를 분리

### SWR
- 
key 값이 null 이거나 key 대신 함수를 사용할 경우 falsy한 값을 return 하면 fetch를 멈출 수 있습니다.

React Query
- enabled 값으로 멈출수 있습니다.

## 사용자가 ‘프로필 수정’ 기능을 통해 데이터를 수정해서, 프로필 정보를 refetch 하고 싶은 경우에는 어떻게 할까요?

### SWR
- mutate 라는 함수를 통해서 키에 해당하는 query를 refetch 하도록 요청할 수 있습니다.

### React Query
- invalidateQueries 함수를 통해 해당 key의 query가 invalid 하다고 알려줄 수 있습니다.

## refetch를 하지 않고 업데이트하고 싶다면 어떻게 할까요?

### SWR
- 위에서 사용한 mutate 함수에 키뿐 아니라 데이터를 같이 파라미터로 전달하면 refetch 없이 업데이트 할 수 있습니다.

### React Query
- setQueryData 라는 함수를 통해 데이터를 직접 업데이트해 줄 수 있습니다.

## 그외

- 브라우저의 오래된 탭에 해당 페이지가 살아있다면 세션에 대한 처리 해야하는 경우 revalidateOnFocus, refetchOnWindowFocus 옵션 하나로 해결 할 수 있다.

### React Query 부가 기능
- query를 invalid 하다고 처리할 때 array의 filter처럼 유효하지 않은 query를 predicate를 통해 한 번에 처리가 가능합니다.
```
queryClient.invalidateQueries({
  predicate: query => query.queryKey[0] === "todos" && query.queryKey[1]?.version >= 10,
});

```

### QA
- SWR이 아닌 React Query를 선택한 이유는?
  - 둘다 동일하기에 부가 기능들이 있기에 선택한것으로 보여짐