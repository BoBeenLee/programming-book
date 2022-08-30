# How to speed up your workflow with Console shortcuts | DevTools Tips

- https://www.youtube.com/watch?v=hdRDTj6ObiE

## $\_ 최근 콘솔에 계산한 값을 가져올 수 있다. (변수는 안된다.)

```
2+2
$_ (4)
```

## $0, $1...를 이용한 마지막으로 선택한 5개 DOM 선택

- 사용 케이스가 어떻게 될지 감이 안옴.

## 콘솔에서도 jQuery와 비슷하게 $로 querySelector가 가능하다.

```
$("body")
```

## $$ querySelectorAll과 유사하게 모든 요소를 가져온다.

- 모든 svg태그 요소를 가져옵니다.

```
$$("svg")

```

## $x xPath?

```
$x("//p")

```

## queryObjects (Identify objects created with a certain constructor)

- 특정 생성자로 생성된 객체 식별하여 리스트로 뿌려줍니다.

```
queryObjects(Promise)

```

## keys, values, copy

```
keys(player)
values(player)
copy(player)
```

## getEventListeners, monitorEvents, unmonitorEvents

```
monitorEvents(window, "resize");
unmonitorEvents(window)
```

## My Opinion

- jQuery처럼 쓸수 있다는 점
- queryObjects를 이용하여 모든 객체 생성 요소 상태를 확인할 수 있는 부분
- Object클래스 이용없이 keys, values를 이용할 수 있다는점
- \*\*monitor 함수를 이용하여 콘솔로 value watching이 가능할 수 있기에 개발 값 확인용도로 기억하고 있다면 유용할것으로 보입니다.
  - ex) 로그인 후 accessToken 값이 제대로 바뀌고 있는지 여부
