## Experience Order ( https://www.youtube.com/watch?v=0c9OC9NBsro )
- User Experience ( AJAX )
- Developer Experience ( React, Angular, Vue )
- Offline Experience ( kill the dinosaur )
- Provide Application like user Experience

## Programming Term
- [Imperative vs Declarative Programming](https://blog.webix.com/difference-between-declarative-and-imperative-programming-with-language-examples/)
- monkey patch
- Event loop
- closure
- [Coroutine](https://en.wikipedia.org/wiki/Coroutine)
  - https://medium.com/@jooyunghan/%EC%BD%94%EB%A3%A8%ED%8B%B4-%EC%86%8C%EA%B0%9C-504cecc89407
- hoisting
- [generator function](http://meetup.toast.com/posts/73)
- IIEF ( Immediately-Invoked Function Expression )
- [CORS](http://homoefficio.github.io/2015/07/21/Cross-Origin-Resource-Sharing/)
- apply, call, bind
- fisrt class ( function, object, component? )
- lexical scope : use environment where function [and variable] is defined 
<=> dynamic scope
  http://bestalign.github.io/2015/07/12/Lexical-Scope-and-Dynamic-Scope/
- Iterator, Generator <br/>
  https://github.com/nhnent/fe.javascript/wiki/October-12---October-16,-2015
- Promise
- Syntactic sugar
- partial, curry
- callback
- prototype, prototype chain <br/>
  https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67
- tag template literals <br/>
  ex) styled-component
- high order function, component
- short-circuit
- debounce
- Single source of truth
- DRY ( Don't repeat yourself )
- Magic Number
- landing page
- [Optimistic UI](https://www.apollographql.com/docs/react/recipes/authentication.html)
- milestone
- Single point of failure (SPOF)

http://jstherightway.org/ko-kr/

# Image
- image sprite
- Progressive Image or Image Optimization (https://medium.com/@kyle.robert.gill/ridiculously-easy-image-optimization-with-gatsby-js-59d48e15db6e)


# GraphQL
- query language for your API
- Odata(http://www.odata.org/)

## [apollo](https://www.apollographql.com/), [urql](https://github.com/FormidableLabs/urql)
- supported client side
- make easy query, mutation, but more better urql

# React, React Native

## SSR ( Server Side Rendering )
- Rendering Optimzation ( Hastening React SSR with Component Memoization and Templatization )
  - Memoization: Component's rendered markup is stored in a cache and used for sub-sequent requests of 
  the exact same component.
  - Templatization: Component's rendered markup is templatized and used for sub-sequent requests of the 
  same component with different props.

## Component
- [Compound Components](https://www.youtube.com/watch?v=hEGg-3pIHlE)

## Render Props
- https://github.com/renatorib/react-powerplug
- https://github.com/pedronauck/react-adopt

## Redux
- http://bestalign.github.io/2015/10/26/cartoon-intro-to-redux/
- [Ducks Pattern](https://github.com/erikras/ducks-modular-redux)
  - To me, it makes more sense for these pieces to be bundled together in an isolated module that is self contained, and can even be packaged easily into a library. if you wanna more detail, click ducks link.
- [redux-box](https://github.com/anish000kumar/redux-box)
### Services
- https://github.com/hql287/Manta

### Flux Concept
- http://bestalign.github.io/2015/10/06/cartoon-guide-to-flux/
### Action
- Redux-Thunk
based on High order Function
- Redux-Saga 
based on Generator Function
- Redux-Obervable
like Observer pattern.
### Reducer
- Hierarchy Tree
### Store
- a Store 

## MobX
- https://mobx.js.org/intro/concepts.html
- It Seems Like Excel Spreadsheets
- [mobx-state-tree](https://github.com/mobxjs/mobx-state-tree)
### Services
- https://github.com/meetfranz/franz


## Obervable
- https://redux-observable.js.org/

## translator
- babel
- grunt

## Other Patterns
- LINQ
- CQRS(Command Query Responsibility Segregation) - Redux패턴의 유래가 CQRS에 있다함.
- Codifies patterns
- [Proxy and Decorator Patterns](https://lostechies.com/derickbailey/2012/03/29/proxies-and-decorators-in-javascript/)
  - 구현은 비슷하나 개념은 다르다. <br/>
  Decorator: 3rd party software, middleware
  Proxy: Mobx, immer, internet proxy server <br/>
  Proxy objects are the same in software. You make a call to a resource or service and the call that you make is handled by an object that can figure out how to make the real call, possibly pre-process the results and send any response you need, back to you.
- Hijacking a javascript function Pattern
- [Registration Pattern](https://www.youtube.com/watch?v=smBND2pwdUE)
- [TCC - Try Confirm Cancel Pattern](https://www.popit.kr/rest-%EA%B8%B0%EB%B0%98%EC%9D%98-%EA%B0%84%EB%8B%A8%ED%95%9C-%EB%B6%84%EC%82%B0-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B5%AC%ED%98%84-1%ED%8E%B8/)

## Error
Uncaught promise errors in Chrome
```javascript
window.onunhandledrejection = event => {
  event.preventDefault(); // prevent the console.error warining
  console.log('Unhandled promise rejection: ' + event.reason);
}
window.onrejectionhandled = event => {
  console.log('promise rejection handled');
}

function foo() {
  const promise = Promise.reject(new Error('trichobezoar'));
  setTimeout(() => promise.catch(error => console.log('eventually caught')),
  5000);
}

foo();
```
### Remember
- Only throw/Promise.reject Error objects
- Make sure all promise chains have a proper catch
- Code defensively with debugging in mind

### JavaScript error Tracking services
bugsnag, rollbar, sentry, raygun, honeybadger, trackjs, airbrake.io

## Best Tools
- [Freactal](https://github.com/FormidableLabs/freactal)
  - input, toggle등 반복적인 state처리가 필요할 시 provideState로 컨테이너 분리하면 효율적으로 사용할 수 있음.
- [Carousel](https://github.com/FormidableLabs/nuka-carousel)
  - 말이 필요없는 깔끔한 Carousel
- [Radium](https://github.com/FormidableLabs/radium)
  - CSS in JS. inline style로 모든 CSS를 표현할수 있다. ex) mediaquery, :hover, :active ...

