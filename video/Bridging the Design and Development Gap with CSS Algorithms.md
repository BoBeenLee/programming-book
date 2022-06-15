[Bridging the Design and Development Gap with CSS Algorithms](https://www.youtube.com/watch?v=YYdVDwfJKsw)

Pramming Paradigms

- Imperative "How" Control Flow
Javascript, Ruby, C++, Python

- Declarative "What" No Control Flow
Domain-Specific, SQL, HTML, CSS

CSS is a domain-specific declarative programming language.

In 2018
- Turing Complete
- Math
- Functions + Variables
- Conditional Logic

CSS developers program the layout of boxes

Algorithm
- A well-defined computational procedure that takes input and produces output.

A CSS pattern is a well-defined declaration or set of declarations that produces a specific styling output.

Algorithms 1: clearfix

Algorithms 2: positioning

```
.outer-thing {
	position: relative;
}
.sticky-thing {
	position: absolute;
	bottom: 100%;
	left: 0;
}

```

Algorithms 3: aspect ratio(one way)
```
.image-container {
	position: relative;
	padding-bottom: calc((2/3) * 100%);
}
.image-container > img {
	position: absolute;
	width: 100%;
	height: 100%;
	object-fit: cover;
}
```

Algorithms 4: arrows with borders
```
.arrow-up {
	width: 0;
	height: 0;
	border-left: 15px solid transparent;
	border-right: 15px solid transparent;
	border-bottom 15px solid red;
}
```
Algorithms 5: Fluid Type

```
h1 {
	font-size: calc(2rem + 3vw);
}

@media(min-width: 800px) {
	h1 {
		font-size: calc(2rem + (800px * (3/100)));
	}
}

```

Algorithm Interview
1) Plan
2) Brute force solution
3) Walk through
4) Optimize solution

Programming Boxes
1) Pseudocode boxes
2) Write smelly CSS
3) figure out the algorithms
4) Give them names/selctors

CSS is declarative + domain-specific
(unique + resilient!)
