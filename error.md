## Error

Uncaught promise errors in Chrome

```javascript
window.onunhandledrejection = (event) => {
  event.preventDefault(); // prevent the console.error warining
  console.log("Unhandled promise rejection: " + event.reason);
};
window.onrejectionhandled = (event) => {
  console.log("promise rejection handled");
};

function foo() {
  const promise = Promise.reject(new Error("trichobezoar"));
  setTimeout(
    () => promise.catch((error) => console.log("eventually caught")),
    5000
  );
}

foo();
```
