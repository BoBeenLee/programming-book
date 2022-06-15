# Everything you need to know about React 18: Shruti Kapoor

- https://www.youtube.com/watch?v=Z-NCLePa2x8

## UI centric updates focussed on performance.

- new features - concurrent features - transitions, suspense on the server
- improvements: automatic batching, better rendering performance

## React 18
- Release in march 22

- ReactDOM.render -> ReactDOM.createRoot

Root
- Root no longer opaque to the user.
- Makes all new features available.
- Without root, new features and concurrent rendering will be turned off.

## Quick Guide
- Concept: Concurrent React
- Features: Automatic Batching, Transitions, Suspense on the server
- APIs: createRoot, hydrateRoot, renderToPipeableStream, renderToReadableStream
- Hooks: useId, useTransition, useDeferredValue, useSyncExternalStore, useInsertionEffect
- Updates: Strict mode
- Deprecated/discouraged: ReactDOM.render, renderToString

## What's New
- Automatic Batching
Automatic Batching = making a list of grocery items.

## What is batching?
```
function handleClick() {
	setIsFetching(false);
	setError(null);
	setFormStatus("success");
}
```
re-rendered 1 times

Before React 18, updates outside events were not batched
Before React 18: not batched

```
fetch('/something').then(() => {
	setIsFetching(false);
	setError(null);
	setFormStatus("success");
})
```

re-rendered 3 times

## With React 18, updates are batched automatically

### React 18: Automatic Batching
```
fetch('/something').then(() => {
	setIsFetching(false);
	setError(null);
	setFormStatus("success");
})
```
re-rendered 1 times

With automatic batching, all updates even within promises, setTimeouts, will be batched.

## Concurrent React
Concurrency

----|--------------|--------------|------------
 chat with Alice   chat with Bob

----------|--------------|------------------
		    chat with Bob
----|-------------------------|------------
         chat with Alice   

React can interrupt, pause or abandon a render.

### Concurrent Rendering
- Not a feature.
- Behind-the-scenes mechanism.
- Implementation details are hidden from the developer.
- Enables React to prepare multiple UI version.
- Enables interruptible rendering.
- React guarantees that the update will appear consistent event if a render is interrupted.
- Waits to do DOM mutations until the end, once the entire tree has been evaluated.
- Enables **Reusable state** - Concurrent React can remove sections of UI from screen, then add them back later while reusing previous state.
- Eg: a user tabbing away and coming back to the screen.
- No concurrent mode.
- Replaced by concurrent features.


## Transitions

Transitions - startTransition, useTransition

1. Prioritize updates
2. Mark non-urgent UI updates as "transitions"
3. Helps in letting React "interrupt" when urgent updates come in

```
import { startTransition } from "react";

// Urgent: Show what was typed
setInputValue(input);

// Mark any state updates inside as transitions
startTransition(() => {
	// Transition: Show the results
	setSearchQuery(input);
});
```

What if we want to do something while transition is happening?

```
import { useTransition } from "react";

const [isPending, startTransition] = useTransition();
```

Where to add startTransition?

1. Slow rendering: React performs a lot of work.
2. Slow network: React waits for data from network.
Needs Suspense - use with libraries like Relay.


## Suspense on the server
Code Splitting on server

Before React 18: All or nothing

```
<Suspense fallback={<Spinner />}>
...
<Suspense>
```

- One slow part doesn't slow down the whole page.
- Show initial HTML early and stream the rest.
- Code splitting fully integrated with server rendering.

Changes
- Server API changes
	- renderToPipeableStream (Node)
	- renderToReadableStream (edge env)
	- renderToString deprecated
- Client API changes
	- render -> createRoot
	- unmountComponentAtNode -> root.unmount
	- ReactDOM.Hydrate -> hydrateRoot
- Library API changes
	- useId()
	- useSyncExternalStore()
	- useInsertionEffect()

How does your codebase get affected?
- Your code should work fine

Is this a breaking change?
- Components behave slightly differently with concurrent rendering.
- Some components may require some migration efforts.
- New rendering behavior is only enabled in parts of your app that use new features.

Upgrade strategy
1. Upgradte to React 18 without breaking code.
2. Gradually start adding concurrent features.
3. Use StrictMode to surface concurrency related bugs in dev.
4. Start using concurrent features after upgrading to React 18


Most apps should work after upgrading to React 18 with little to no changes

Concurrent features are opt-in, and you decide where and whether you want to use

Edge cases to watch out for
- StrickMode became stricter (but you can disabled it)
- flushSync() lets you opt out automatic batching
- Concurrent featues may require library updates

React 18 for app develops
- Out-of-the-box improvements
- New foundational features
- Upgrade in one afternoon
