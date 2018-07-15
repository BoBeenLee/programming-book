[React Native How we do it at InterNations](https://www.youtube.com/watch?v=qYyEG9ioWqU&list=PLXB3WIVcnsH1byiN0Ipav5m_UPXnUpzV6&index=9&t=3957s)


Objectives:
1. First class native feel & performance
2. Android & iOS simultaneously
3. Offline-first
4. Support a broad range of features

write solid code

Flow
Good
- Prevents many classes of errors
- Significantly reduces refactoring effort
Bad
- Library types are missing or outdated
- Error reporting is bad (but somewhat consistent)
- Doesn't play well with Saga
- Issues are slow to get fixed


Step 2: Release
Nightlies & Countinuous Delivery

Jekins, Code Push, Fastlane

state?
Redux
Standard, most popular solution
Lots of tooling, libraries
Functional in style
Rather boring

Actions
1. Separate concerns
2. Traceable side effects

2: Higher Order Components
UI Behavior
- Connect
- Dispatch on mount (data bootstrapping)
- Dispatch on interval
- Pull down to refresh
- Show modal
- Show action sheet
- Placeholder
- Orientation lock
- Infinite scrolling
- Error boundary**


3: Composition Layouts
Behavior
compose(
connect(mapConversationList),
data({
	onMount: apiActions.reqConversations,
}),
pagination('conversations', {
	limit: 10,
	onLoadNextPage: apiActions.reqConversations,
})
)


Composition Presentation
(props: ConnectProps & PaginationProps) => (
	<FlexView>
		<SwipeableList
			data={props.conversations}
			onSwipe={props.onSwipe}
			renderItem={renderItem}
			onEndReached={props.onLoadNextPage}
		/>
		<FloatingButton onPress={props.onCreateMessagePress} />
	</FlexView>
);


Offline first
Redux Saga : Powerful, Expressive, Awesome, Mobile

## To do:
1. FSA -> Fetch -> FSA
```
while(true) {
	const req = yield take('REQUEST');
	const res = yield call(fetch, req.payload);
	yield put({ type: 'RESPONSE', payload: res });
}
```
2. Persist REQUEST, destroy RESPONSE
3. Buffer incoming requests
```
const reqChannel = yield actionChannel('REQUEST'); // Construct
while(true) {
	const req = yield take(reqChannel);
	const res = yield call(fetch, req.payload);
	yield put({ type: 'RESPONSE', payload: res });
}
```

4. Time out after 5 seconds
```
const reqChannel = yield actionChannel('REQUEST');
while(true) {
	const req = yield take(reqChannel);
	const [res] = yield race([
		call(fetch, req.payload),
		call(delay, 5000)
	]);
	if(res) {
		yield put({ type: 'RESPONSE', payload: res });
	}
}
```

5. Pause work when device offline

```
const reqChannel = yield actionChannel('REQUEST');

// Last slide, wrapped in a function:
function *work() {...}

// Cancel when offline, fork when online
while(true) {
	yield race([
		fork(worker),
		take('OFFLINE')
	]);
	yield take('ONLINE')
}
```

6. Handle more than one request at once

```
// Handle more than one request at once
const reqChannel = yield actionChannel('REQUEST');
function *work() {
	try {
		while(true) {
			const req = yield take(reqChannel);
			const [res] = yield race([
				call(fetch, req.payload),
				call(delay, 5000)
			]);
			if(res) {
				yield put({ type: 'RESPONSE', payload: res });
			}
		}
	} finally {
		if(yield cancelled()) {
			yield put(req);
		}
	}
}

// Fork a saga n-times
const forkTimes = (saga, ntimes) => fork(function*() {
	for(let i = 0; i < ntimes; i++) {
		yield fork(saga);
	}
})

while(true) {
	yield race([
		forkTimes(worker, 5), // Usage
		take('OFFLINE')
	]);
	yield take('ONLINE')
}
```


Saga Modules
Modules named by side effect source Saga dedicated acrtions


```
import saga, { sagaMiddleware } from 'app/saga';
import makeStore from 'app/Store';
import ui from 'app/ui';

const store = makeStore(sagaMiddleware);

sagaMiddleware.run(saga);

const app = ui(store);

export default app;

```

"Regular" Redux Saga Tests are flawed
use Redux Saga Test Plan

Time to ship
Debugging

Use React Native Debugger But...
- Saga stack traces source the same (wrong) line
- Hot module reloading doesn't work

Debugging API calls in Chrome
- GLOBAL.XMLHttpRequest = GLOBAL.originalXMLHttpRequest || GLOBAL.XMLHttpRequest;
- https://youtu.be/qYyEG9ioWqU?t=54m57s

Stack traces are often in native code

Ship again
React Native Performance

Android First

Optimization
- Reduce re-renders
	1. React.PureComponent
	2. shouldComponentUpdate()
	3. Getter cache(reselect)
	4. Remove arrow functions in render, notably in lists
	5. Control re-render (redux-batched-subscribe)
- Native Navigation
- Reduce time to component mount

Otherwise...

Scaling
https://youtu.be/qYyEG9ioWqU?t=1h17s

Production Monitoring

MS App Center
- Release, builds, tests, crashes, events
- Works with Code Push
- Javascript stack traces in crash logs
- Nice to use, but events still suck

How much native code did you write?
0*

How much code is reused between iOS and Android?
+95%

so?
```
Native Mobile App Challenges | RN Ecosystem Solutions |
UI | React Naitve |
Business Logic & Side Effects | Redux Saga |
State Management | Redux |
Tests | Jest, Calabash, Detox |
Types | Jest & TypeScripts |
Code Quality | Eslint, Prettier |
Debugging | React Native Debugger |
Continuous Delivery & Deployments | Code Push, Fastlane, Jenkins |
Performance optimization | Android first |
Production Monitoring | MS App Center |
Scaling | ? |

Library | Usage | Do you care? |
prettier | developer efficiency | **** |
eslint | stability | **** |
redux | state management, action-based infra | *** |
flow | stability | *** |
redux-saga | side effects/bus.logic | ** |
reselect, batched subscribe | render cost reduction | ** |
fastlane | sane builds | * |
app center | crash analytics | * |
calabash, detox | acceptance tests | * |
```






