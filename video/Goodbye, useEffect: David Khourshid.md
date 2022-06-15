Goodbye, useEffect: David Khourshid
- https://www.youtube.com/watch?v=HPoC-k7Rxwo

```
useEffect(() => {
	// componentDidMount?
}, []);

useEffect(() => {
	// componentDidUpdate?
}, [something]);

useEffect(() => {
	return () => {
		// componentWillUnmount?
	};
}, []);

```

useEffect is not a lifecycle hooks

"Imperative"<br/>
When something happens,<br/>
execute this effect.<br/>
<br/><br/>
"Declarative"<br/>
When something happens,<br/>
it will cause the state to chage<br/>
(Dependency array) ---- and depending on which parts of the state changed,<br/>
this effect should be executed,<br/>
but only if some condition is true.<br/>
Adn React may execute it again<br/>
for no reason concurrent rendering.
<br/><br/>

```
useEffect(() => {
	if(foo && bar && (bar || quo)) {
		doSomething();
	} else {
		doSomethingElse();
	}
	// oops, forgot the cleanup
}, [foo, bar, baz, quo]);

```

where do effects go?


```
function Component(props) {
	useEffect(() => {  ---> React 18 runs effects twice on mount (in strict mode)
		...
	}, [...]);

	return <div> ... </div>
}
```

What is useEffect() for?<br/>
**Synchronization.**

```
useEffect(() => {
		const sub = creatThing(input).subscribe(value => {
			// do something with value
		});
		return sub.unsubscribe;
},[input]);
```

one way to think about it is that useEffect is a way to synchronize React with some external system(network, subscription, DOM). if you don't have any external system and just try to manage your data flow with useEffect, you're gonna have all these problems.

Action effects<br/>
"Fire-and-forget"

Activity effects<br/>
Synchronized

Where do action effects go?<br/>
**Event handlers.** Sorta.

Can event handlers have side effects?<br/>
Absolutely! Event handlers are the best place for side effects.

in React, side effects usually belong inside **event handlers.**

useEffect
- however, this approach should be your last resort.

```
<form onSubmit={event => {
	// side-effect!
	submitData(event);
}>
	{...}
</form>}
```

UI is a function of state
(state) => UI

(state, event) => nextState

When do effects happen?
**State transitions. Always**

Middleware, callbacks, sags, reactions, sinks, monads(?), whenever

(state, event) => nextState

->

(state, event) => (nextState, effects)

```
function useSpicyReducer(reducer, initialState, executeEffect) {
	const [state, setState] = useState(initialState);

	const spicyDispatch = useCallback((event) => {
		// Calculate next state
		const nextState = reducer(state, event);

		// Execute effect based on transition
		executeEffect(state, event, nextState);

		// Commit next state
		setState(nextState);
	}, [reducer, state, executeEffect]);

	return [state, spicyDispatch];
}

```

Where do action effects go?<br/>
**Event handlers. <br/>
In state transitions.<br/>
..which happen to be executed at the same <br/>time as event handlers.**
<br/><br/>
Effects with external stores
**useSyncExternalStore()**

```
import { useSyncExternalStore } from 'react';
import { someStore } from "./somewhere";

function Component() {
	const state = useSyncExternalStore(someStore.subscribe, someStore.getSnapshot);

	return (
	<button onClick={() => {
		someStore.dispatch({ type: 'someEvent' });
	}}>Click me</button>)
}

```
->
```
import { createMachine, interpret } from "xstate";
import { useMachine } from "@xstate/react";

const machine = createMachine({
	// ...
});

const Wizard = () => {	
	const [state, send] = useMachine(machine);

	return (
	<form onSubmit={() => sned('SUBMIT')}>
		{state.matches("first") && <FirstStep />}
		{state.matches("second") && <SecondStep />}
		{state.matches("review") && <ReviewStep />}
		{state.matches("submitting") && <Submitting />}
	</form>);
}

```

State management
- State store
- state updates
- Subscriptions
- Event dispatching

- Multiple stores
- Communication
- Effect management
- finite states + transitions

Fetching data <br/>
**Render-as-you-fetch** <br/>
**with Suspense**
<br/><br/>
Fetching data with Suspense

```
function Component() {
	const data = someResource.read(); // might suspend

	return // ...
}

```

Effects are state management.
**Don't put side-effect aside.**

(state, event) => (nextState, **effects**)

useEffect is for synchronization<br/>
State transitions trigger effects<br/>
**Effects go in event handlers**<br/>
Render-as-you-fetch (suspense)<br/>
**Model effects with state machine**
