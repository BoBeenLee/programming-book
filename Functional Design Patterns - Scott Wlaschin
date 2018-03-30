
[https://www.youtube.com/watch?v=srQt1NAHYC0&t=0s&index=4&list=WL](Functional Design Patterns - Scott Wlaschin)

- Core Principles of FP design
	- Functions, types, composition
- Functions as parameters
	- Functions as interfaces
	- Partial application & dependency injection
	- Continuations, chaining & the pyramid of doom
- Monads
	- Error handling, Async
- Maps
	- Dealing with wrapped data
	- Functors
- Monoids
	- Aggregating data and operations

These "patterns" can be buit-in or not,
depending on your programming language

Core Principles of FP
- Functions are things :: --Function--
- Composition everywhere :: logo
- Types are not classes

A function is a standalone thing, not attached to a class

let z = 1;

ex) Funciton apple -> banana

Functions as inputs and outputs

Core principle:
Composition everywhere

f1 apple => banana f2: banana => cherry
composition f3 apple => cherry


-> Low-level operation -> -> Low-level operation -> -> Low-level operation ->
			
Service

Address -> AddressValidator -> Validation Result

A "Service" is just like a microservice but without the "micro" in front


-> Service -> -> Service -> -> Service ->
	
Use-case

Change Profile  Request -> UpdateProfileData -> ChangeProfile Result

-> Use-case -> -> Use-case -> -> Use-case ->

Web Application

Http Request -> Server -> Http Response


Core principle:
Types are not classes

So what is a type then?
A type is just a name for a set of this.

Composition everywhere:
Types can be composed too

New types are built from smaller types using:
"AND" "OR"

Only possible because behavior is separate from data!

"AND"
FruitSalad = One each of Apple and Banana and Cherry

type FruitSalad = {
	Apple: Apple
	Banana: Banana
	Cherry: Cherry
};


"OR" types
Snack = Apple or Banana or Cherry


type FruitSalad = {
	| Apple: Apple 
	| Banana: Banana
	| Cherry: Cherry
};

Real World Example:
We accept three forms of payment:
Cach, Check, or Card.

For Cash we don't need any extra information
For Checks we need a check number
For Cards we need a card type and card number

How would you implement this?

Design principle:
Strive for totality

int TwelveDividedBy(int input) {
	switch(input) {
		case 3: return 4;
		case 2: return 6;
		case 1: return 12;
		case -1: return -12;
	}
}

NonZeroInteger: Solution Constrain the input

Solution Extend the output
Some 4, Some 6, None

Design principle:
Use static types for domain modeling and documentation

Function as Parameter
Guideline:
Parameterize all the thiings

Tip:
Function types are "interfaces"

Function types provide instant abstraction!

interface IBunchOfStuff {
	int DoSomething(int x);
	string DoSomethingElse(int x);
	void DoAThirdThing(string x);
}

Let's take the Single Responsibility Principle and the Interface Segregation Principle
to the extreme...

Every interface should have only one method!

interface IBunchOfStuff {
	int DoSomething(int x);
}

An interface with one method is a just a function type
type IBunchOfStuff: int -> int

Any function with that type is compatible with it

Object-oriented strategy pattern:
class MyClass {
	public MyClass(IBunchOfStuff strategy) {
		...
	}

	int DoSomethingWithStuff(int x) {
		return _strategy.DoSomething(x);
	}
}

Functional Strategy pattern:
let doSomethingWithStuff strategy x => strategy x

with FP approach => you don't need to create an int => int interface in advance.

Decorator pattern
let isEven x = ... // int -> bool

let isEvenWithLogging = logger isEven
Substitutable for original isEven


log isEven log
let isEvenWithLogging = log >> isEven >> log

Bad news:
Composition patterns
only work for functions that have one parameter!

Good news
Every function is a one parameter function

let add x y = x + y
Normal function (Two parameters)

let add = (fun x y => x + y)
Function as a thing (No parameters)

let add x = (fun y => x + y)
One parameter


let three = 1 + 2
let three = (+) 1 2
let three = ((+) 1) 2

let add1 = (+) 1
let three = add1 2

Pattern:
Partial application

let name = "Scott"
printf "Hello, my name is %s" name 
Two parameters

(printf "Hello, my name is %s" name ) name

 Pattern:
 Use partial application when working with lists

 Pattern:
 Use partial application to do dependency injection

 type GetCustomer = CustomerId => Customer
Persistence ignorant

Pattern:
The Hollywood principle*:
	continuations

Don't call us who call you.

Pattern:
Chaining callbacks with continuations

MONADS a.k.a chaning continuations

A switch analogy

input => Some or None

Connecting switches

on Some
Bypass on None

Composing switches

Composing one-tract functions is fine...

How to combine the mismatched functions?

"Bind" is the answer!
Bind all the things!

FP'ers get excited by bind

Building an adapter block

Two tract input => Slot for switch function => Two-tract output

Pyramid of doom: using bind
This pattern is called "mondic bind"

Pattern:
Use bind to chain tasks

Connecting tasks
Wait => when task completes => Wait

Pyramid of doom: using bind of tasks
let taskBind f task = 
	task.WhenFininshed (fun taskResult => f taskResult)

let taskExample input =
	startTask input
	> taskBind startAnotherTask
	> taskBind startThirdTask
	> taskBind ...

This pattern is also a "monadic bind"

Patterh:
Use bind to chain error handlers

Use case without error handling

A structor for managing errors

Connecting switches

This is "two track" model -
the basis for the "Railway Oriented Programming"
approach to error handling.

Guideline:
Most wrapped generic types have a "map". Use it!

Terminology alert:
Mappable types are "functors"
