# I never thought this would be possible with CSS

- https://www.youtube.com/watch?v=OGJvhpoE8b4

## :has()

```
div:has(h1) {
	background-color: hotpink;
}

div:has(p) {
	background-color: limegreen;
}

div:has(p:empty) {
	background-color: firebrick;
}

div:has(.fancy-paragraph) {
	color: rebeccapurple;
	background: white;
}

div:has(> a) {
	background: steelblue;
}


```

## Browser support

- Firefox, IE11이하 미지원
  - https://caniuse.com/?search=%3Ahas(

## className selector와 :has와 차이점

- :has는 조건문과 같은 역할을 한다.
  ex) div:has(p) p태그가 존재한다면 div태그 css스타일을 적용한다.

- className selector
  ex1) div p div내 p태그가 존재할 경우 div내 p태그 css스타일을 적용한다.
  ex2) div.empty div의 empty클래스가 존재할 경우 div의 empty클래스 css스타일을 적용한다.
  - ex2 예시와 :has가 유사할듯 싶다.

## Usecase

- article**title클래스 하단 마진을 article**subtitle여부에 따라 조정하고 싶을때

```
<article>
  <h1 class="article__title">A really interesting article</h1>
  <p class="article__subtitle">More info about it here</p>
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Facere, quam!</p>
  <p>Dolorem impedit est ab laborum quisquam atque a sit debitis!</p>
  <p class="example">Delectus inventore corrupti veritatis voluptates ipsam earum a rem praesentium.</p>
</article>

<article>
  <h1 class="article__title">Another article</h1>
  <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Facere, quam!</p>
  <p>Dolorem impedit est ab laborum quisquam atque a sit debitis!</p>
  <p>Delectus inventore corrupti veritatis voluptates ipsam earum a rem praesentium.</p>
</article>


.article__title:has(+ .article__subtitle) {
	color: lime;
}

.article__title:not(:has(+ .article__subtitle)) {
	color: pink;
	margin-block-end: 5rem;
}
```

## Conclusion

- parent DOM기준 스타일을 :has조건문에 따라 스타일을 적용하고자 할경우, :has()사용으로 간단하게 해결할 수 있다.
