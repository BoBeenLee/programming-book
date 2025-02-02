# What React Refs Can Do for You

- https://www.youtube.com/watch?v=TgpTG5XYoz4

- 1. useMemo로 렌더링 최적화
- 2. ref로 리렌더 발생하지 않게 구성

## Usage

- ex) https://github.com/timolins/react-hot-toast/blob/main/src/components/toaster.tsx#L22

```

// React v18
const setRef = useCallback((divRef) => {
	if(divRef === null) {
		// cleanup
		return;
	}
	// other code
}, [])

// React v19
const setRef = useCallback((divRef) => {
	// other code
	return () => {
		// cleanup
	}
}, [])


```
