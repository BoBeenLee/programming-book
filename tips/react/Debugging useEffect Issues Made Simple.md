# Debugging useEffect Issues Made Simple

- https://www.youtube.com/shorts/NkUf0ULcWAE

- 각 콘솔로그(next, user, config) 카운팅으로 어떤 dep에서 무한 호출이 발생하는지 확인할 수 있다.

## 재료
- ninja console

```ts
function User({config}) {
    const [user, setUser] = useState();
    const [next, setNext] = useState(...);

    useEffect(() => {
        console.log(next); // x123
    }, [next]);

    useEffect(() => {
        console.log(user); // x123
    }, [user]);

    useEffect(() => {
        console.log(config); // x4
    }, [config]);

    useEffect(() => {
        // Do Something Fetching
    }, [next, user, config]);
}


```