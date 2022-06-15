
[ReactNYC - Functional Programming Fundamentals - Matthew Gerstman (@MatthewGerstman)](https://www.youtube.com/watch?v=kkRyjXDpYqg&index=1&list=WL&t=0s)

What are we gonna talk about today?
* Functional Programming
* Declarative vs Imperative styles

What are we not gonna talk about today?
* Monads
* Lambda calculus
* Functors
* Other scary function jargon

Let's take a step back
I believe in two things
Use the best tool for the job
Moderation is key

What's the point?
* Make our code more readable
* Make our code easier to reason about
* Make our code easier to test
* Make our users happier

When is Functional Programming most usefurl?
* Functional Programming is most useful when we're doing 1 to 1 data transformations.

What is Functional Programming?
* Functional programming (often abbreviated FP) is the process of building software by composing pure functions.

A pure function is a function which given the same inputs, always returns the same output, and has no side effects.

Examples of side effects
Sometimes these are necessary, but they are not pure functions.

Mutation
Modifying the argument that's passed in.

```
function pop(arr) {
	return arr.splice(0, 1);
}

const arr = [1,2,3,4];
pop(arr);
console.log(arr);
```

Shared State

```
let i = 0;
function increment() {
	return i++;
}

function decrement() {
	return i--;
}
```

Asynchronous Code
```
let i = 0;

function incrementAsync(obj) {
	setTimeout(() => {
		i++;
	}, 0);
}
incrementAsync();
console.log(i);
// later
console.log(i);
```

Lets look at an example
```
// This is a pure function
function clone(obj) {
	return {...obj};
}

// this mutates the given object
function killParents(wizard) {
	wizard.parents = "Dead";
	return wizard;
}

```

Declarative vs Imperative 

Declarative code describes what it does.
```
function ReactComponent({ counter }) {
	return <span>{counter}</span>
}

```

Imperative code describes how it does it.
```
function UpdateCounter({ counter }) {
	document.getElementById('counter').innerHTML(`<span>${counter}</span>`);
}
```
Note: Declarative code will always end up either compiling down to or being processed by something imperative.

Separation
If you try to perform effects and logic at the same time, you may create hidden side effects which cause bugs in the logic. Keep functions small. Do one thing at a time, and do it well.

Composition
Plan for composition. Write functions whose outputs will naturally work as inputs to many other functions. Keep function signatures as simple as poissible.

Example (Separation and Composition)
```
function sortFilesByName(files) {
	return lodash.sortBy(files, 'name');
}

function getPdfFiles(files) {
	return lodash.filter(files, {extension: PDF});
}

function getFileNames(files) {
	return lodash.map(files, 'name');
}

const getSortedPDFFileNames = lodash.flow(
	getPdfFiles,
	getFileNames,
	lodash.sortBy
);

// alternative
const getSortedPdfFileNames = (files) => (
	lodash.sortBy(
		getFileNames(
			getPdfFiles(files)
		)
	)
);
```

Immutability
The true constant is change. Mutation hides change. Hidden change manifests chaos. Therefore, the wise embrace history.


Memoization
Memoization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again.

HOF (Higher Order Functions)
in mathematic and computer science, a higher-order function is a function that does at least one of the following:
* takes one or more functions as arguments (i.e. procedural parameters),
* returns a function as its result.

Function that takes a function
Callback

```
fetch('user', {userId: 1}).then((response) => {
	persistUser(response);
});
```

Function that returns a function
Closure
```
function counterGenerator() {
	let i = 0;
	return function() {
		console.log(++i);
	}
}

// Usage
const counter = counterGenerator();
counter(); // => 1
counter(); // => 2
counter(); // => 3
```

Function that takes a function and returns a function

Wrapper Function
```
const killSiblingMemoized = lodash.memoize(killSibling);
const getSortedPDFFileNames = lodash.flow(
	getPdfFiles,
	getFileNames,
	lodash.sortBy
);

const castSpell = () => console.log('Expelliarmus');
const lodash.debound(castSpell, 100);
castSpell();
castSpell();
castSpell();
```

Currying + Partial Application

Currying
Currying is the technique of translating the evaluation of a function that takes mutiple arguments (or a tuple of argments) into evaluating a sequence of functions, each with a single argument.
```
function sum(a, b, c) {
	return a + b + c;
}

const curredSum = lodash.curry(sum);

curriedSum(1,2,3); // 6

const addFive = curredSum(2,3);
addFive(7); // 12
addFive(8); // 13

const addOne = curredSum(1);
addOne(2,3);

const addThree = addOne(2);
addThree(3);
```

Partial Application
Partial application (or partial function application) refers to the process of fixing a number of arguments to a function, producing another function of smaller arity.

Aside: Arity is a term for the number of arguments a function takes.

```
function learnSpell(spell, wizard) {
	return {
		...wizard,
		spells: [
			...wizard.spells,
			spell
		]
	};
}

const learnExpelliarmus = lodash.partial(learnSpell, "Epell");
const learnExpectoPartronum = lodash.partial(learnSpell, "Expect");

```



