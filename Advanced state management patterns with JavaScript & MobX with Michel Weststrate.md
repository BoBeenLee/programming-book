

[Advanced state management patterns with JavaScript & MobX with Michel Weststrate](https://www.youtube.com/watch?v=uWIT9M95mqQ&index=2&list=WL&t=0s)

## Why?
like Excel
+ Pattern used in the most successful software product
+ Natural way of thinking


Box 1: Data Cells
Box 2: Formulas
Box 3: Draw on screen
Box 4: Users enters data

## MobX
Makes sure data is always, automatically and
efficiently reflected in derived values and
that necessary side effects are fired.
<br/>
Box 1: Obersable values @observable<br/>
Box 2: Computed Values @computed<br/>
Box 3: Reactions autorun(observer, reaction, when)<br/>
Box 4: Actions @action<br/>
<br/>
Note, using decorators is optional!

## Recipes
+ Forms
+ Async
+ Designing stores
+ Dependency injection
+ Testing
+ Routing
+ Time

### Observables as component state
+ Optional, but used by many MoXites
+ Better optimized and simpler to use than setState
+ Easy refactoring into stores
+ Blog: 3reasons why I stopped using setState

### Libraries
+ mobx-react-form
+ formstate

### Async stuff
+ Async = two synchronous actions at different points in time
+ Track progress with observables
+ Nothing special about it

#### Async: fromPromise
+ Part of mobxUtils package

### Domain State
+ "What your app is about"
+ Unlike component state which is volatile
+ Should be reusable, distributable and testable
+ Should not be owned by UI
+ Should not be affected by UI
+ Many architectural patterns possible; MobX is unopinionated
+ Classes <> plain objects
+ Object graph <> Object tree
+ Normalized <> Denormalized Data
+ Class methods <> Dispatching Actions(Flux)
+ Tip: serializr
+ Tip: mobx-state-tree

### Serialization
JSON is just another representation of the state.
So can be derived by MobX

### Connecting multiple stores
+ Global imports
+ Dependency injection (e.g. InversifyJS)
+ Root store

## Root store pattern
+ One for all, all for one
+ No global state
+ Straight forward
+ Can provide environment specific things(fetch)
+ Strongly typed
+ Can be made generic

### Root store
+ Scalable pattern
+ Abstract away environment specific things
+ Easily testable and zero-state

## Provide / inject
+ Provider / inject: inject stores in components
+ Uses context, but: doesn't break shouldComponentUpdate
+ mobx-react package
+ Blog: How to safely use React context

## Making the UI dumb
+ The less logic lives in components, the easier your app is to test
+ Portable components and domain logic

## Dumb UI: create a view store
+ Capture crucial app state in a browser unaware store
+ UI just renders this state
+ Browser url/history is just another derivation
+ Navigation triggers state changes instead of component hooks
+ Blog: How to decouple state and UI (a.k.a. you don't need componentWillMount)

### Libraries
+ mobx-router: Hooks, renders comps, store structure
+ yester: Hooks, strong typed
+ mobx-react-router: Simplifies MobX + React-router, like react-router-redux
+ mobx-location: Window.location as observable

## mobxUtils.now()
+ Time is the ultimate observable
+ Takes interval. Synchronizes similar intervals.
+ frame for requestAnimationFrame.
+ Countdown demo

## MobX
+ Find minimal set of observables that expresses the state of your app
+ Derive all other things from the minimal state
+ MobX keeps derivations in sync using runtime analysis

1. Super simple to Write<br/>
Focus on what you want to achive.
Ignore how it should affect your application.
It will be derived.

2. Eliminates bugs related to cascading updates<br/>
If the family name changes, don't forget to update spouse name...

3. Eliminates bugs related to staleness<br/>
If the spouce name changes, should be reflected on screen..

4. Fine grained updates perform much better then event based updates<br/>
Don't notify components rendering persons, only those which will be affected by this change...
