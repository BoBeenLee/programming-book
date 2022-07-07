# React 18 for External Store Libraries

- https://www.youtube.com/watch?v=oPfSC5bQPR8

## Concurrent Rendering and Libraries

- Opt-in concurrent features in React 18
- Concurrent rendering
- Libraries affected - External stores, Libraries not affected

## Tearing with Concurrent Rendering

- Libraries affected by concurrent rendering - External stores

- tearing is a visual inconsistency

## What are External Stores?

- External stores

  - Redux store, Zustand store, Global variables, document.body, Date ...

- Interval states
  - useState, useReducer

## How Tearing Can Happen in Concurrent Rendering

## New Hook to Solve: useSyncExternalStore

External Stores ->

```
useSyncExternalStore(subscribe, getSnapshot) => State
``

## Demo
- 마이그레이션 방법에 대한 설명

## What are external stores again?
- Interval : External
			External Stores
				<- Subscribe <- useSyncExternalStore

## What Should Be Migrating
- React 17 (useState, useEffect, useRef)
			|								-> External stores
- React 18 (useSyncExternalStore)

## More to Cover Vairous Use Cases
- getServerSnapshot : For server side rendering
- useSyncExternalStoreWithSelector : For inline selectors
- useState / useReducer : For some use cases


## Get Ready for React 18
React 18 -> Concurrent Rendering -> useSyncExternalStore : for external stores

## My Opinion
- Concurrent Rendering에 영향이 있는 라이브러리는 어떤것들이 있는가?
	- 영향이 있기에 External stores를 이용하여야할것이다.


```
