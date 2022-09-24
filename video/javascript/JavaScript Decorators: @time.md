# JavaScript Decorators: @time

- https://www.youtube.com/watch?v=mM3zJ86QfBk&list=WL&index=2
- https://jsfiddle.net/andrew8088/cfd5h39n/

- ex) time 데코레이터를 이용한 구현 with Babel

```js
function time(target, key, descriptor) {
  const originFn = descriptor.value.bind(target);
  let i = 0;

  descriptor.value = function (...args) {
    let i = i++;
    const keyId = key + id;
    console.time(keyId);
    let value = originFn(...args);
    console.timeEnd(keyId);
    return value;
  };
}

const fns = {
  @time
  squareAll(arr) {
    return arr.map((x) => x * x);
  },
};

console.log(fns.squareAll(Array(1000).fill(4)));
```
