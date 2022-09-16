# Subtle, yet Beautiful Scroll Animations

- https://www.youtube.com/watch?v=T33NN_pPeNI&list=WL&index=2

## 구현 방법

아래 방법 중 IntersectionObserver위주로

- AOS 다만 14.1kb 번들사이즈
- next gen css features 호환성 문제
  - @scroll-timeline
  - https://developer.mozilla.org/en-US/docs/Web/CSS/@scroll-timeline
- IntersectionObserver를 이용한 구현방법

## Intersection Observer를 이용한 Scroll Animations

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    console.log(entry);
    if (entry.isIntersecting) {
      entry.target.classList.add("show");
    } else {
      entry.target.classList.remove("show");
    }
  });
});

const hiddenElements = document.querySelectorAll(".hidden");
hiddenElements.forEach((el) => observer.observe(el));
```

```css
.hidden {
  opacity: 0;
  filter: blur(5px);
  transform: transplateX(-100%);
  transition: all 1s;
}

.show {
  opacity: 1;
  filter: blur(0);
  transform: transplateX(0);
}

@media (prefers-reduced-motion) {
  .hidden {
    transition: none;
  }
}
```
