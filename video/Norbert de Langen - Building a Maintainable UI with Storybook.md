
Norbert de Langen - Building a Maintainable UI with Storybook | ReactNext 2018

https://www.youtube.com/watch?v=9lQMmbITt0c&index=9&list=WL&t=101s

Writing better components using
Storybook

Writing apps is hard

How often are your estimations correct?

is de-composing your big application into smaller application to answer?
yes

Distributed monolith

What can we learn from this?
How can we build UIs to minimize this?

Abstraction, Isolation, Autonomy

Good abstraction is the key to good software
If you create abstractions where you shouldn't you'll get complexity.
If you don't create abstractions where you should you'll get complexity.

If developers are like ninja fighting complexity...

Complexity is the dragon
If we fail to fighting it effectively, we feed it.

To create correct abstractions
We must understand the problem well

"If you know the enemy and know yourself, you need not fear the result of a hundred battles. 
If you know yourself but not the enemy, for every victory gained you will also suffer a defeat.
If you know neither the enemy nor yourself, you will succumb in every battle."

Isolation is the possible result of good abstraction.

An isolated component can be switch by a similar one.

The API of your component
Isolated pieces will have some API for communication
It's this API, the props if you will, that will determine if your component will be love.

The trade off in isolation
If your component isolates too much...
The API will either have to grow to compensate for it's multitude of use-cases; increasing the complexity.


When components:
- Abstract the right amount of stuff
- Isolate enough but to too much
- Have a good API to do things
then...

They won't have to change as often
And when they do, their use-cases are limited

It's easier to re-use

Autonomy

Components abstract a section of UI
right?

Components should abstract a UI pattern/concept.
- This is different from "a section of visible UI".

UI concepts can be visible.
But they can also provide data/state/layout/styles etc.

A well implmented UI concept should abstract/isolate that particular concept and nothing else.
Rememeber, if you abstract too much, it will likely result in complexity later.

Design an API for your component so encapsulates the UI Pattern.
no more, no less

remember:
to abstract correctly you must understand the problem well dragon.

A '/(carousel|tabs|accordion)/' component should should toggle activity of list-items.children

Encapsulates the UI Pattern, no more, no less.

Key take away
Embrace using components beyond the visual

Problem
So manuy components

Solution:
Storybook
