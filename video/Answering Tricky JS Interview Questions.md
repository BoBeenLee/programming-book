
[Answering Tricky JS Interview Questions](https://www.youtube.com/watch?v=MY0UBGX2FtA&index=72&list=WL)

1) Explain event delegation

JS event listeners fire not only on a single DOM
element but on all its descendants

2) Describe event bubbling.

Inverse of this. Also known as propogation, events on an element will "bubble up" and also fire on all parents.

3) What's the difference between "target" and "currentTarget" ?

The latter is the element with the listener attached, the former is the actual element that triggered it.

4) Explain why the following doesn't work as an IIFE.

Immediately invoked function expression.

4) Explain the difference on the usage of

function foo() {
	// i am known as 
	// a definition or statement
}

var foo = function() {
	// i am an expression
	// i resolve to a value, event if just "undefined"
};

Functions as expressions vs. definitions
MDN - An expression is any valid unit of code that resolves to a value.

3a) What neends to be changed to properly make it an IIFE?

(function foo() {})();

behold the parentheses

common js, import export, module.exports

why would i ever use one?


5) Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?
You can't predict the future.
- Reduce collision
- Maintain independence
- Easier to write your own code


6) Explain "hoisting"

all variables(var) are declared at the top of any given
function scope whether you like it or not (includes function declarations)


Example - how I write it

function hoist(track) {
	if(track === 'Down With Disease') {
		var action = 'dance';
	} else {
		var action = 'skip';
	}
	return action;
}


In walks const and let
- Not hoisted
- Scoped within the block they are in
- Gives you more control

What do we do with this knowledge?
var, const or let?

7) What's the difference between a variable that is: null, undefined or undeclared?
undefined
- variable declared but no defined value(not initialized)
- object/array exists but nothing at that key/index
- function exists but doesn't return anything
- falsy

null
- null has a value. its value is null.
- null is a "nothing" value
- not zero, not an empty string/object/array
- falsy

7a) How would you go about checking for any of these states?
Undeclared finds you
Except when assigning a value.

// global scope
foo = 5;

console.log(foo);
// prints 5!
// implied global, aka a reason people hate JS

check for undefined
`
let foo;
console.log(typeof foo); // "undefined" as a string
console.log(typeof bar); // undeclared, but also returns "undefined"

// preferred
console.log(foo === undefined); // true boolean

const baz = 'undefined';
console.log(baz === undefined); // false. Hooray, I guess.
`

check for null
const foo = null;
console.log(typeof foo); // object.  let that sink in for a minute

// preferred
console.log(foo === null); // true boolean

8) What is the difference between == and === ?

let foo;
const bar = null;

console.log(foo == bar); // true boolean

Double equals checks for equality
Triple equals checks for equality and type

9) What is the event loop?
9a) What is the difference between call stacl and task queue?
