[Bartosz Król - How to become a hipster with React Recompose](https://www.youtube.com/watch?v=SM9vp41GRNY&index=13&list=WL&t=0s)

Why would you want to use recompose?
- Clean Code

So What is this mysterious clean code?
- Modular
- Well documented
- Testable
- Reads like a well written prose

If your code is a reflection of your soul, ask yourself this:
is your soul a piece of shit?
- Mateusz Budzar

What is Clean Code for me?
- Idiomatic
- Compoasable


() => <div>Hello</div>
Not everything can be like that
- Lifecycle methods
- this.setState
- Event handlers
- Branches
- Pure rendering

Separate the View from Effects

Presentational vs. Container Components

Higher Order Components (HOC)

HOC :: Component => Component

```
const withLoader = Component => ({ isLoading }) => {
	if(isLoading) {
		return <Loader />;
	} else {
		return <Component />;
	}
}

export default withLoader(MyWidget);
```

Let's try more generic, shall we?

```
const branch = (predicateFn, Comp1, Comp2) => 
	props => predicateFn ? <Comp1 {...props} /> : <Comp2 {...props} />;

const betterBranch = curry(branch);

const withLoader = betterBranch(props => props.isLoading, Loader);

export default withLoader(MyWidget);
```

React State issues
- View is inseparable from state
- Difficult to reuse
- Unnecessary re-renders
- Have to use Class keyword

```
function withState(
stateName: string,  // counter
stateUpdater: string, // setCount
initialState: any // 0
)
```

Component with State


```
const withCount = withState("counter", "setCounter", 0);

const Counter = withCounter({ counter, setCounter });

const increment = setCounter(n => n + 1);
const decrement = setCounter(n => n - 1);

<div> 
	Count: {counter}
	<button onClick={increment}>+</button>
	<button onClick={decrement}>-</button>
 </div>
````

Handlers inside the HOC

const withCounter = compose(
	withState("counter", "setCounter", 0),
	withHandlers({
		increment: event => ({ setCounter }) => setCounter(n => n + 1),
		decrement: event => ({ setCounter }) => setCounter(n => n -1)
	}),
	pure
);

How to decouple from Redux?

Let's use it with Recompose
const withBuffer = compose({
	renameProp("users", "previousUsers"),
	withReducer("users", "dispatch", usersReducer, props => props.previousUsers),
	withHandlers({
		addUser: () => ({ dispatch }) => dispatch({
			type: ADD_USER,
			user: createEmptyUser()
		}),
		removeUser: (user) => ({ dispatch }) => dispatch({
			type: REMOVE_USER,
			user
		}),
		reset: ({ previousUsers }) => ({ modifyUsers }) =>  dispatch({
			type: RESET,
			users: previousUsers
		}),
		save: () => ({ modifyUsers }) => modifyUsers(users)
	}),
	pure
});

*Recompose helps with HOC creation
- Re-render optimization
- DisplayName boilerpate reduction
- shallowEqual almost for free
- Painless Class conversion

What else can Recompose do?
- Create component from props
- Manipulate Context
- Lifecycle methods
- Oberservable toolbox
- ...and much, much more

Recompose is for React what Lodash is for Javascript

is it worth adding Recompose to my project?

Think about different ways to develop software
Find your own style
... or just use it if you hate classes


