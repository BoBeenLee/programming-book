
  
## Proxy Pattern
- https://www.patterns.dev/posts/proxy-pattern/
- 프록시 오브젝트는 우리가 상호작용할떄마다 행동들을 측정합니다.
ex) setValue, getValue 하였을 경우

- Proxy객체의 두번째 arguments는 handler이고 get, set을 대표적으로 쓰인다.
- 프록시는 validation을 추가하는것에 유용하다.


### Reflect
- 프록시와 함께 작동할때 Reflect는 target object를 쉽게 조작하게 해줍니다.

- obj[props] = value, obj[props] 했던 부분을 Reflect.get(), Reflect.set() 으로 수정, 접근할 수 있습니다.

### Result
- 프록시는 object의 행동에 따른 컨트롤을 추가하는 파워풀한 방법입니다.
- 각각의 handler에 프록시 과남용, 무거운 작동 수행은 해당 메소드 주입이 앱 퍼포먼스 성능에 부정적인 영향을 줄 수 있습니다.

### Usecase
- validation, formatting, notification, debugging
- SDK axios 기능을 method(get, delete, options, post, put, patch)에 대해서만 호출이 가능하게 제한적이게 하기 위해 사용했었습니다.
  -  public한 SDK이기에 method의 기능 제한을 하기위함.