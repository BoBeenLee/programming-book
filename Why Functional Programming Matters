Why Functional Programming Matters

What do programming languages do for us?
- they provide "first-class concepts"
- they provide a means for thinking about the problem.
- they provide an abstraction principle.
 - like most languages, programming languages give us a framework--a set of abstractions--by which we can think about (and solve) problems.
 - if the abstraction does not exist within the language, it is difficult  (if not impossible) to embrace or use.

object - state, behavior

don't fit
- transactional

Functional programming is a diffrecnt way of thinking about modularizing applications.
And, admittedly at times it is a different way of thinking that runs entirely contradictory to the way that object-oriented programmers think.

Some basic functional concepts
- immutable values over mutable variables
 - Immutable values
  - once bound, a binding remains constant throughout its lifetime
  - thus offers no opportunity for confusion/reassignment/etc
 - Values over variables
  - "values" are not "variables"
  - name/value binding is fixed once bound
- functions as first-class values
 - think about common operations--if we could vary the actual operation itself as a parameter, how much work could be saved?
   example: you need to iterate through a collection to...
   ...and each time you write is as a "for" loop, you're violating DRY
 - this enables the use of functions as "higher-order" functions
  - "take this function, and execute inside your context"
  - similar in some ways to a callback, but with clearer semantics
  - in a lot of ways, this is Inversion-of-Control all over again.
- curring, partial-application of functions
 - Partial application
  - Providing some of the parameters (but not all) to a function and capturing that as a function to be called
 - Currying
  - it turns out that all functions can be reduced to functions taking one parameter and either yielding a result or another function
  - this permits easy 'pipelining' and composition of functions in a highly reusable manner (as the micro level)




- expressions-not-statements
 - this is an outgrouwth of the functions-as-first-class-citizens idea: if functions yield values, what is the practical difference between a keyword and a function?
 - even C++ tried to make user-defined elements look and feel like built-in constructs and vice versa
 - if we're really goot about this, developers can create new "language" primitives and nobody will know the difference
- laziness/deferred execution
 - object-oriented laziness has nothing on functional laziness
 - don't compute anything until absolutely necessary (but make sure to maintain the dependency graph so everything is there when needed)
 - laziness is highly encouraged/permissible in pure FP
 - just to be fair, laziness is highly desirable inside the process, not so across processes unless carefully managed
- Sequences
 - lots of things can be seen as sequence
  - characters in a string
  - fields in a record
  - records in a database
  - files in a directory
  - algorithmic calculations (factorial, fibonacci, ...)
  - lines in a file
 - sequences and collections have a deep relationship
  - in many ways, this is the gateway to FP ideas/concepts


Some optional functional concepts
 - strongly-typed, type-inferenced
  - Strongly-typed
   - the dynamic language community will have you believe that it's better to write unit tests by hand than to have a system that can do common-sense checking for you.
  - Type-inferenced
   - why do i have to be explicit to the language, when it can figure out what i'm trying to do and when?
 - recursion
  - immutable values doesn't mean no state changes instead, hold state on the stack, not in mutable memory.
 - tuples, lists
  - "bundles" of data in different directions
  - tuples give developers a "lightweight" object that needn't be named or otherwise formalized


 - pattern-matching
  - switch/case is to pattern-matching as my kid's soccer team is to Arsenal or Manchester United
  - pattern-matching also encourages "destructuring" of data when necessary/desired
  - pattern-matching can operate off of collections of values
