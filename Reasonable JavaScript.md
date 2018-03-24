[Reasonable JavaScript](https://www.youtube.com/watch?v=0cJqiO_Q0KA)

## Goals
+ What makes code easy to reason about
+ Why Javascript sometimes makes it hard to write code
that is easy to reason about
+ Different methodologies we can use to write Javascript
code that is easy to reason about

Walk away knowing what it means to reason about code

Javascript is a fantastic language for many reasons.
Run everywhere, Versatile, Immediate Feedback Loop, Community

## Redesign our program
Step 1: Don't mutate original argument
Step 2: Remove global dependencies
Step 3: Handle invalid input arguments

Understand our improved program's behavior

More battle testing

## Redesign our program (again)
add testing -> fixed.

What did we learn?
+ Reliance on global variables causes our programs to be unreliable.
+ Mutable data can lead to unintended side effects
+ Having no way to restrict the type of data that can be passed into a 
function makes you to think extra hard about error handing
+ Type coercion makes it harder to predict the behavior of our code

first, let's define what makes code easy to reason about
+ Does not affect or mutate external state (i.e. no sdie effects)
+ Does not rely on external state
+ Always returns the same corresponding output for a given input
	+ Easier to understand intent
	+ Easier to reuse
	+ Easier to maintain
	+ Easier to refactor
	+ Easier to test
	+ ... easier to reason about

Unit test
### Result
+ Always returns the same corresponding output for a given input 

Why tests
+ Verify that our code behaves correctly
+ Test error cases and edge cases
+ Living documentation
+ Make changes without fear

Types
A type is a classification of data which tells the compiler 
or interperter how the programmer intends to use the data.

Why types?
1) Separates data from behavior
2) Documentation
3) Removes convoluted error handling & testing
4) Elimates entire categories of bugs
ex) 
type AppState = {
	isFetching: boolean,
	messages: ?Array<string>
}

Other benefits of types
+ Earlier detection of mistakes
+ If it compiles, it runs
+ Can refactor with greater confidence
+ Domain modeling tool

### Result
+ Always returns the same corresponding output for a given input. maybe?
+ Guaranteed to work as intended by the programmer

Immutable data
An immutable object's state cannot change after it's created.
If you want to change an immutable object, you don't

Instead, you create a new object with the changed value
and point your reference to it.

Quicksort using immutable data
```javascript
function quickSort(list) {
	if(list.isEmpty()) {
		return list;
	}

	var pivot = list.fisrt();
	var remaining = list.rest();

	var lessThanPivot = remaining.filter(v => v < pivot);
	var greaterThanPivot = remaining.filter(v => v >= pivot);

	return quickSort(lessThanPivot)
		.concat(pivot)
		.concat(quickSort(greaterThanPivot));
}
```

But .. performance

Make it correct, make it clear, make it concise, make it fast.
In that order. - Wes Dyer

Why immutable data
+ When data doesn't change, we can just use the data and not think about whether making changes is safe.

No one can mess with your data.
Nor you thiers.

### Result
+ Does not affect or mutate external state (i.e. no sdie effects)
+ Guaranteed to work as intended by the programmer

Other reasons for immutability
+ No temporal coupling
+ Persistance
+ Lazy operations

Pure function
What is not a pure function
+ Relies on some external state that is not explicitly passed to it as arguments.

What is a pure function
+ Relies only on what is explicitly passed to it as arguments to produce a result.

### Result
+ Does not rely on external state
+ Always returns the same corresponding output for a given input
+ Guaranteed to work as intended by the programmer

But wait, there's more
Pure functions + Immutability = ???
Referential transparency
+ The ability to freely replace an expression with its value and not change the behavior of the program.

Why does Referential transparency matter?
+ Does not affect or mutate external state (i.e. no sdie effects)
+ Does not rely on external state
+ Always returns the same corresponding output for a given input
+ Guaranteed to work as intended by the programmer


Take advantage of functions as first class entities

What does it mean for a function to be a first class entity?
+ Refer to them from constants and variables
+ Pass them as parameters to other functions
+ Return them as results from other functions

Why use functions as first class entities?
Suggestion 1: Replace loops with higher order functions
ex) 
```javascript
const lessThan10000 = x => x < 10000;
const odd = x => x % 2 === 1;
const square = x => x * x;
const sumOfOddSquares3 = R.pipe(
	R.map(square),
	R.takeWhile(lessThan10000),
	R.filter(odd),
	R.sum);
```

Why higher order functions
+ Shorter and less clunky
+ Easier to read
+ More descriptive
+ Allows us to define computations by defining what we want instead of how to get what we want
+ Overall, more information and less noise

Suggestion 2:
Parameterize all the things

ex)
```javascript
const calculateArea = radius => 3.14 * (radius * radius);
const calculateDiameter = radius => 3.14 * (radius * radius);

const actionOnList = (action, list) => {
	return R.map(item => action(item), list)
};

const areas = actionOnList(calculateArea, [1,2,3]);
const diameters = actionOnList(calculateDiameter, [1,2,3]);

Generic functions everywhere
const square = x => x * x;
const double = x => x * 2;
const negate = x => -x;

actionOnList(square, [1,2,3]);
...
```


Why parameterize
+ Parameterized the behavior of calculating the area
	+ ... and calculating the diameter
	+ ... and squaring the value
	+ ... and pretty much anything
+ Now we can pass any list and any action
+ Decouples the behavior from the data

Suggestion 3:
Partial application
Partial application means we can turn a function that expects multiple parameters into one that will keep returning a new function until it receives all it's arguments.

Why partial application
+ Readability
+ Powerful way of transforming your data in a functional way
+ Use functions as generic building blocks that can work with different kinds of data
+ Dependency injection

Suggestion 4:
Use composition

Once we get used to the idea of passing functions to other functions,
we start to discover ways to combine two or more functions together.
This is known as Composition.

ex)
```javascript
const applyTax = x => x * 1.08;
const applyShippingAndHandling = x => x + 10;

const totalCost = R.compose(applyShippingAndHandling, applayTax);
```

Why composition
+ Each function is useful on it's own
+ Easily create fresh, new functionality from existing functions
+ Break apart pieces of behavior, test them independently & reassemble
+ Declutters code >> Readability

Taking advantage of functions as first class entities encourages us to use functions as the primary unit of abstraction.

Small, independent and composable functions become the tool 
we use to model & solve any problem.

### Result
+ Modular and generic
	+ Easier to under intent
	+ Easier to reuse
	+ Easier to maintain
	+ Easier to refactor
	+ Easier to test
	+ ... easier to reason about

## Recap
+ Tests
+ Types
+ Immutable data
+ Pure functions
+ Functions as first class entities
	+ Higher order functions over loops
	+ Parameterize all the things
	+ Composition
	+ Partial Application

Just remember that Javascript wouldn't be where it is today if it weren't this way.
It's incredible flexibility and forgiving nature is exactly what gets beginners in the door and enables it to be used for lots of things.
We are fortunate enough that there are tools and methodologies enable us to write good Javascript code.
I call this a WIN:WIN situation.

