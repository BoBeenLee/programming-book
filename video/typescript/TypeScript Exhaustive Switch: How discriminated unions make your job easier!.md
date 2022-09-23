# TypeScript Exhaustive Switch: How discriminated unions make your job easier!

- https://www.youtube.com/watch?v=CG3_Y9T03J4&list=WL&index=49&t=1s

- ex) assertCannotReach함수를 x:never 파라미터 변수를 통해 타입에러를 발생시켜 유니온타입이 추가된걸 감지합니다.

```ts
function getId() {
  let id = "";
  switch (options.table) {
    case "users":
      id = options.userId;
      break;
    case "widgets":
      id = options.widgetId;
      break;
    case "sessions":
      id = options.sessionId;
      break;
    case "sales":
      id = options.saleId;
      break;
    default:
      assertCannotReach(options);
  }
  return id;
}

function assertCannotReach(x: never) {
  throw new Error("cannot reach this place in the code");
}
```
