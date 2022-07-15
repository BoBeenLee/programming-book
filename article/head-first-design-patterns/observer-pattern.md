# 옵저버 패턴

## Feature

- 주제(=Observable), 옵저버(=Observer, 관찰자)에 의해 정의됩니다.
- 옵저버는 주제에 대한 의존도를 가집니다.
- 일련의 객체들 사이에 일대다 관계를 가집니다.
  - 일(Subject)대 다(Observer)관계이므로 언제든 새로운 옵저버를 추가할 수 있습니다.
- 주제와 옵저버간에 느슨한 겹합(Loose Coupling)을 띄고 있습니다.
  - 주제가 옵저버에 아는것은 옵저버에 구현된 특정 인터페이스(Observer)뿐입니다.
  - 주제와 옵저버는 서로 독립적으로 재사용할 수 있습니다.
  - 주제나 옵저버가 바뀌더라도 서로에 대한 영향을 미치지 않습니다.

## Observable 간단한 구현 방법

observable 는 아래와 같이 나뉩니다.

- observers
  - 이벤트가 발생할때 알림을 주기위한 관찰자들
- subscribe
  - 관찰자를 추가할때
- unsubscribe
  - 관찰자를 제외할떄
- notify
  - 이벤트가 발생할때 모든 관찰자에게 알림을 주기위해

```ts
type Observer<T> = (data: T) => Promise<void> | void;

class Observable<T> {
  observers: Observer<T>[];

  constructor() {
    this.observers = [];
  }

  subscribe(func: Observer<T>) {
    this.observers.push(func);
  }

  unsubscribe(func: Observer<T>) {
    this.observers = this.observers.filter((observer) => observer !== func);
  }

  notify([data]: Parameters<Observer<T>>) {
    this.observers.forEach((observer) => observer(data));
  }
}
```

### setChanged 구현에 대하여

```
setChanged() {
    changed = true;
}
notify() {
    if(changed) {
        ...
       changed = false;
    }
}
```

- 책 내용에는 notify 호출을 최적화하기 위한 용도로 구현하고 있습니다.
  - ex) 0.1도 단위로 쉴새 없이 값이 바뀐다는 가정할때 0.5도 이상 바뀌었을때에만 변경사항을 알려줍니다.
- 다만 이러한 경우는 optional이며 구현 방법은 다양할 듯합니다.
  - debounce, throttle을 이용하여 notify 호출 시점을 최적화한다.
  - Observable 구현체가 notify를 호출할때 값이 변경될때마다 호출하는것이 아닌 0.5도 이상임을 감지하여 notify를 진행한다.

## Example

- Clock Examples

[![Edit Clock - Observer Patterns With TS](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/clock-observer-patterns-with-ts-w25927?fontsize=14&hidenavigation=1&theme=dark)

## Usecase

- DOM onClick 이벤트 리스너
- 상태 관리 라이브러리에서 종종 사용하는 패턴
  - RxJava, RxJS, Mobx, XState (머신간 notify로 전달) ...
- Push Notification 이용하여 앱내 토픽 구독자들에게만 선택적 알림을 주기위해 사용합니다.
  Observable (서버측)
  - Subscribe To Topic API /{topic}/subscribe
  - Unsubscribe From Topic API /{topic}/unsubscribe
  - Get Topics API /topics <-- 현재 구독(Observable)하고 있는 토픽 리스트 조회
    Observer (클라이언트측)
  - Topic onEventListener
    - ex1) Push API - https://developer.mozilla.org/en-US/docs/Web/API/PushEvent#examples
    - ex2) Cloud Messaging - https://firebase.google.com/docs/cloud-messaging/js/receive#web-version-9_1
    - ex3) 자체 구현한다면 Websocket을 이용하여 진행할 수 있다.
    - ex4) Graphql - https://www.prisma.io/blog/tutorial-building-a-realtime-graphql-server-with-subscriptions-2758cfc6d427

## Reference

- https://www.patterns.dev/posts/observer-pattern/
