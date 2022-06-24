
# Concurrent Rendering in React 18 by Ifeoma Imoh

- https://www.youtube.com/watch?v=gAFAlckB4Jo&list=WL&index=3

## What is Concurrency?
- Having more than one task in progress at once or multiple computations happening simultaneously

## Synchronous React - Blocking

## Concurrent Mode - Interruptible

- Introduced interruptible rendering.

First
- Event handler schedules an update(setState) Update is queued but not yet commited. React starts rendering.

Two
- Render phrase might be interrupted by a higher-priority setState.
- If so, the work-in-progress is discarded and restarted later (with memoization).
- So, the render phase must have zero side effects.

Three
- All side effects and mutations are committed simultaneously. only once the entire tree is complete.

## startTransition()
- startTransition lets you keep your UI responsive by allowing you mark specific updates (updates that may take some time) as transitions.

- Urgent Updates: Clicking, Typing, Scrolling, e.t.c
- Transition Updates: Rendering search results, changing UI views, e.t.c

startTransition()
- Wrap non-urgent updates with startTransition.

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

useTransition()
- Use the isPending flag to update the state of your UI by showing your user a feedback when your transition updates aren't ready.
