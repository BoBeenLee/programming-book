
What is Functional Programming?
- Functional programming (often abbreviated FP) is the process of building software by composing pure functions.

a pure function is a function which given the same inputs, always returns the same output, and has no side-effects.

Examples of Side Effects
- Somtimes these are necessary, but they are not pure functions.

Mutation [1]
- Modifying the argument that's passed in.

```
// Mutates the given array
function pop(arr) {
	return arr.splice(0, 1);
}

const arr = [1,2,3,4];
pop(arr);
console.log(arr); // [2,3,4];

Shared State [1]
// These have different values every time you call them.
let i = 0;
function increment() {
	return i++;
}

function decrement() {
	return i--;
}

Asynchronous Code [1]

let i = 0;
function incrementAsync(obj) {
	setTimeout(() => {
		i++;
	}, 0);
}

incrementAsync();
console.log(i); // 0
// later
console.log(i); // 1
```

Isolate Your State; Isolate Your Side Effects!

Lets look at an example

```
// This is a pure function
function clone(obj) {
	return {...obj};
}

// This mutates the given object
function killParents(wizard) {
	wizard.parents = "Dead";
	return wizard;
}
```

```
import { useState, useEffect } from "react";

function ImpureComponent() {
	const [count, setCount] = useState(0);

	// Update the document title using the browser API
	useEffect(() => {
		document.title = `You clicked ${count} times`;
	});

	return (
		<button onClick={() => setCount(count + 1)}>
			Click me
		</button>
	);
}

```

Only Call Hooks from React Functions
- Don't call Hooks from regular Javascript functions. Instead, you can:
  - Call Hooks from React function components.
  - Call Hooks from custom Hooks (we'll learn about them on the next page).

By following this rule, you ensure that all stateful logic in a component is clearly visible from its source code.


Declarative and Imperative

Declarative code describes what is does.

```
function ReactComponent({ counter }) {
	return <span>{counter}</span>
}
```

Imperative code describes how it does it.

```
function UpdateCounter({ counter }) {
	document.getElementById('counter').innerHTML(
		`<span>${counter}</span>`
	);
}
```

Note: Declarative code will always end up either compiling down to or being processed by something imperative.

Separation
- If you try to perform effects and logic at the same time, you may create hidden side effects which cause bugs in the logic. Keep functions small. Do one thing at a time, and do it well.

Composition
- Plan for composition. Write function whose outputs will naturally work as inputs to many other functions. Keep function signatures as simple as possible.

Example (Separation + Composision)
```
function sortFilesByName(files) {
  return lodash.sortBy(files, 'name');
}

function getPdfFiles(files) {
  return lodash.filter(files, { extension: PDF });
}

function getFileNames(files) {
	return lodash.map(files, 'name');
}

const getSortedPDFFileNames = lodash.flow(
	getPdfFiles,
	getFileNames,
	lodash.sortBy
);

// Alternative
const getSortedPdfFileNames = (files) => (
	lodash.sortBy(
		getFileNames(
			getPdfFiles(files)
		)
	);
);
```

Immutability
- The true constant is change. Mutation hides change.
Hidden change manifests chaos. Therefore, the wise embrace history. [4]

Memoization
- Memoization is an optimization technique used primarily to speed to computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again. [5]

Example (Immutability + Memoization)

```
function killSibling(wizard) {
	return {
		...wizard,
		numSiblings: wizard.numSiblings - 1,
	};
}
const killSiblingMemoized = lodash.memoize(killSibling);
const ron = { name: "Ron Weasley", siblings: 6 };
const ronAfterFredDies = killSiblingMemoized(ron);
ron === ronAfterFredDies // false, he's a different person now.

const ronAfterFredDiesAgain = killSiblingMemoized(ron);
ronAfterFredDies === ronAfterFredDiesAgain // true

const ronAfterMovieFredDies = killSibling(ron);
ronAfterFredDies === ronAfterMovieFredDies // false
```

Higher Order Functions
- In mathematics and computer science, a higher-order function is a function that does at least one of the following:
   - takes one or more functions as arguments (i.e., procedural paramters),
   - returns a function as its result. [6]


Function that takes a function
- Callback
```
fetch('user', { userId: 1 }).then((response) => {
	persistUser(response);
})
```
- Closure
Function that takes a function and returns a function

Wrapper Function
```
const killSiblingMemoized = lodash.memoize(killSibling);

const getSortedPDFFileNames = lodash.flow(
	getPdfFiles,
	getFileNames,
	lodash.sortBy
);

const castSpell = () => console.log("Expelliarmus");
const castSpellDebounced = lodash.debounce(castSpell, 100);
castSpellDebounce();
castSpellDebounce();
castSpellDebounce();
```

Currying + Partial Application

Currying
- Currying is the technique of translating the evaluation of a function that takes multiple arguments (or a tuple of arguments) into evaluating a sequence of functions, each with a single arguments. [7]

Partial Application
- Partial application (or partial function application) refers to the process of fixing a number of arguments to function, producing another function of smaller arity. [8]
Aside: Arity is a term for the number of arguments a function takes. [2]

```
const sortFilesByName = lodash.partialRight(lodash.sortBy, 'name');
const getPdfFiles = lodash.partialRight(lodash.filter, { extension: PDF });
const getFileNames = lodash.partialRight(lodash.map, 'name');
```

Take a step back
- Make our code more readable
- Make our code easier to reason about
- Make our code easier to test
- Make our users happier
