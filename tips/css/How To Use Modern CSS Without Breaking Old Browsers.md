# How To Use Modern CSS Without Breaking Old Browsers

- https://www.youtube.com/watch?v=IVqPIIJi0qs

## IE만 제외하고 supports css를 지원하고 있는듯하다.

- https://developer.mozilla.org/en-US/docs/Web/CSS/@supports#browser_compatibility

ex)

```css
@supports (display: flex) {
  body {
    background-color: lightgreen;
  }
}
```
