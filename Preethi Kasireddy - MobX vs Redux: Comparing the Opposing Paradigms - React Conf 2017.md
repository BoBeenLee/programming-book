[Preethi Kasireddy - MobX vs Redux: Comparing the Opposing Paradigms - React Conf 2017](https://www.youtube.com/watch?v=76FRrbY18Bs&index=4&list=PLXB3WIVcnsH1TZxTuF6YaiRV0eVWAJhfC)

### Goals
- Explore difference in Mobx vs Redux for state management
- Evaluate benefits and tradeoffs of the opposing paradigms
- How to choose: setState vs. Mobx vs. Redux vs. something else?

### Redux & Mobx
- Open source client-side state management libs
- Describe UI as a function of state
- No relation to React
- Work especially well with React

### Redux
- Single store / Domain class
- Plain objects
- Immutable
- Normalized state

one way data flow

### Mobx
formulas spreadsheet
- Multi-store / Domain classes
- Observable data
- Mutable
- Nested state

### Single store vs. Multi-store
- Single source truth
- Distributed Domain Classes

### Plain data structures vs. Observable data
- Plain
{
	user = {
		id: '123',
		name: 'Preethi'
	}
}
- Observable
let user = observable({
	id: '123',
	name: "Preethi"
});
class User {
	@observable user;

	constructor(user) {
		this.user = user;
	}
}

### Mobx observes references.
Any observable property (blue) that is dereferenced,
(i.e. "dotted into") in a tracked function will be recorded.
If a reference is changed, Mobx will react

### Redux
- Manually track updates
- Explicit
- Passive

### Mobx
- Automatically tracks updates
- Implicit
- Reactive

### Redux
- Read-only state
- (prevState, action) => newState
- Pure

### Mobx
- Read and writee to state
- state => state
- Impure

### Redux 
Actions required

### Mobx
Actions not required

### setState
- Start here.
- NOT an anti-pattern.
- Learn React lifecycle methods
- Learn (internal) component state management
- State is hierarchical & matches component

### Problem
- Share more state across components -> (Internal) state mgmt becomes difficult

- Distant leaf components need access to state -> That intermediary components don't need

### Solution
- Manage application state external to the components
Mobx or Redux
- Individual leaf components can access and manipulate state

### Mobx
- Simpler application
- Rapid prototyping
- Small team

### Redux
- Complex application
- Large team
- Chaning requirements

### Mobx
Single domain class can encapsulate all its update logic

### Redux
1 part of state affected by an action

### Mobx
- Reacting to state changes
- Examples =>
 - Real-time systems, dashboards, etc
 - Text editors, presentation software, etc.
 - NOT for event based

### Redux
- Reacting to actions or events
- Examples ->
	- Business apps
	- Event based systems
	- Game events involving a complex reaction


### Something else??
- Referential transparency
	- Redux: ALWAYS
		- Pure reducer functions
		- Immutable state
	- Mobx: SOMETIMES
		- Observable data -> Derivation
		- Event -> Observable data mutation
- Reactivity
	- Mobx: YES
	- Redux: NO
- Reducer + Observable

### Conclusion
- Whichever one you choose, it's not an end-game
- No vendor lock-in
- Not framework-specific
- Relatively "do-able" to go Redux -> Mobx or Mobx -> Redux
