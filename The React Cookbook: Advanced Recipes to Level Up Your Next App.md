[The React Cookbook: Advanced Recipes to Level Up Your Next App](https://www.youtube.com/watch?v=lG6Z0FQj_SI&t=0s&index=2&list=WL)

## Design Patterns
- "Solutions to recurring problems"

 Recurring Software Problem
 =>
 Design Pattern
 => 
 food

Design Patterns are the recipes that help us cook delicious react apps.

Let's add some recipes to your react cookbook.

React Top Chefs

## Our Cookbook
- Context API
- Presentation/Container Components
- Render Props

## Cookbook Recipe #1:
Context API

Passing props can be annoying.


Profile - Sidebar - Settings - ResetPassword

Prop Drilling

Sometimes we want our state to be global, but React doesn't.

No way to directly access parent state from a deeply nested component.
...until now!!!

Context API:
"a way to pass data through the component tree without having to pass props down manually at every level."

Profile - - - - - ResetPassword

<Provider> Global State Container

<Consumer> Has Access To The Provider

```
/* creates a provider + consumer pair */
const { Provider, Consumer } = React.createContext();

/* whatever is passed to value will be available to the Consumer */
<Provider value={/* some value */}>

<Consumer>
	{value => /* render something based on the context value */}
</Consumer>
```

Prop Drilling X, Redux X

- When you find yourself passing props down deep into your tree.
- You truly need 'global state' (auth, user settings, translations, themes)
- Someone tells you you need redux.

## Recipe #2: 
Presentation / Container components

<WeatherWidget />

Request some weather data from the API.
Display that data on the page.

Bloated components
- Difficult to reason about
- Hard to modify / reuse
- Unfriendly to other devs

separation of concerns.

Concern
- Something your code is responsible for.

Weather Widget
- Fetching Data ( Logic )
- Displaying Data ( UI )


Container Components for logic.
Presentation Component for user inteface.

Container Component a.k.a "What is does"
Presentational Component a.k.a "What it looks like"

Why is this useful?
- Readable
- Easier to hunt down bugs
- Re-usable
- Testable

When do I use it?
- Too many things!!
- Mixture of behaviour/presentation
- Bloated Component

## Recipe #3: 
Render Props

Puppy Voting App
<PuppyFeed>
<KittenFeed>
<PetFeed>

1. GET /api/puppies or GET /api/kittens
2. Surface 'loading' spinner
3. Render adorable puppies or kittens
4. If error, render error

<UserProfile>

1. GET /api/profile
2. Surface 'loading' spinner
3. Render user's profile
4. If error, render error

Tight coupling of logic + presentation made our components less reusable and flexible.

Render Props:
"a simple technique for sharing code between React components"

What they have in common:
- Request data from API
- Need loading states
- Have error states

How they differ
- Render different things
- Render different spinners

Common logic, different presentation
<Resource />

Same logic, different presentation = huge win

Why render props are so important:
- Self document incredibly well
- Separate presentation from logic
- Decrease code duplication
- Extendable
- Reusable
- Abstract away logic

When to use them
- Don't start with a render prop. Start simple, refactor later
- Share logic between components but not UI
- Other developers to re-use your code
- Defer rendering UI to a later date
- Dealing with common states/events in different components

three time -> abstract.

Battle Tested.
Shareable.
Fun to Use. 
Familiar.
