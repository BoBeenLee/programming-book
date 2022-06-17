
When To Fetch: Remixing React Router - Ryan Florence

- https://www.youtube.com/watch?v=95B8mnhzoCM&list=WL&index=2&t=669s

## Status Quo(현상 유지) (for us)

- Clicked a link URL changed but UI didn't?
- Clicked two links quickly, UI flickers and sometimes shows the wrong page?
	- cancellation

## Oh, no
- How do i refetch when other components update the invoice?

```
npm i react-query
``` 

## What's the problem?

## Component Fetching
```
function Root() {
	// 1. initiator + 2. reader + 3. fallback
	let user = useFetch(url);
	return (
		<Layout>
			{user ? <Sales /> : <Spinner />}
		</Layout>
	);
}
```
- great hooks, but parent 'fallback' blocks child fetch 'initialization'!
	- UI blocked

## What's the solution?

## Load in parallel faster, no jank

## How?

## You need to 'initiate' fetches 'before' you render

## How!?

## Decoule
- decoupling is always the answer
	- 'initiating' fetches
	- 'reading' results
	- rendering 'fallbacks' 

## You need to 'initiate' fetches 'before' you render

## "I heard React 18 and React Server Components fixes all of this."

- heard wrong

```
- RSC: moves rendering and data fetching to the server
- Streaming: sends the document in chunks as they become available during the initial SSR
- Suspense: defines where the UI can fallback when components are trying to read data from, uh ... somewhere
```

```
Suspense is "not designed to define where you *initiate* fetches, but rather *where you access* the results."
```
- *액세스*하는* 위치를 정의하도록 설계되어있다.

## React is a Rendering Library
### not a data library

- X when to 'initiate' fetches
- X when to 'read' results
- O when to 'fallback'

## What do you know so you can 'initiate' fetches 'before' you render?
	- what is available to you to make decision?

## URL
- Maybe the User?, Math.random() ?

```
<Route
	path=":id"
	element={<Invoice />}
	loader={async ({ params, signal }) => { // <--- initiate
		return fetch('/invoices....');
	}} />;


function Invoice() {
	let invoice = useLoaderData(); // <---- read
	return <InvoiceView data={invoice} />
}

```

## "If your UI is nested, your Routes should be nested."

examples
```
loader <------- initiate in parallel
ReactDOM.render(
	<DataBrowserRouter fallback={<Spinner />} exceptionElement={<ErrorScreen />}>
		<Route loader={Root.loader} element={<Root />}>
			<Route path="sales" loader={Sales.loader} element={<Sales />}>
				<Route path="invoices" loader={Invoices.loader} element={<Invoices />}>
					<Route path=":id" loader={Invoice.loader} element={<Invoice />} />
				</Route>
			</Route>
		</Route>
	</DataBrowserRouter>,
	document.getElementById("root")
);

```

## "But I like my components defining their data dependencies"

## "Close Enough"

- distance: Component Fetching --- Nested Route Fetching ------- URL Route Fetching

## Before

```
export default function Invoice() {
	let params = useParams();
	let { isLoading, error, data } = useQuery(`invoice:...`, async () => { 
		// ...fetching
	});

	if(error) {
		return <ErrorScreen error={error} />;
	}
	if(isLoading) {
		return <Spinner />;
	}

	return <InvoiceView data={data} />;
}
```

## After 
- with remix
```
export async funciton loader({ params }) {
	return fetch('/invoices...');
};

export default function Invoices() {
	let data = useLoaderData();
	return <InvoiceView data={data} />;
}
```

after flatten all those requests into one things.

## Less Code, Better UX.

## Data Loading Not Event the Best Part.

## Mutations
- Automatic data revalidation, pending state management, error handling, optimistic UI, and more.

- Time to First Byte
- First Contentful Paint
- Cumulative Layout Shift
- Largest Contentful Paint
- Time To Interactive

- initiate in parallel하게 호출하여 First Contentful Paint ~ Largest Contentful Paint, Time To Interactive 주기를 단축시킬 수 있다. 

## parallelize unblock
- but we've some blocked. (by document and main JS)
- remix comes in and it's a server
	- fetch server side (server knows the URL)

- Server fetching을 진행해도 TTFB, FCP, LCP, TTI duration은 동일하다. TTFB가 data에 의해 blocked 당하고 있다.
 	- faster
 		- LCP no longer blocked on client side Javascript
	- slower
		- TTFB now blocked by data

- server fetching
	- smaller (servers can fetch faster)
- TTFB
	- larger (data in HTML + duplicated hydration script)
- FCP & LCP & ~TTI
	- smaller (javascript data abstractions stay server side)

## levers TTFB <> CLS, LCP

- "TTFB" blocked by data
	- how do we get rid of that?
		- caching
			- ssg (caching html documents)
			- redis
			- request response cache-control
## Transitions

- Component Fetching
	- but parent 'fallback' blocks child fetch 'initialization' 

- Route Fetching
	- loader in parellel

- Route Pre-Fetching
	- prefetch equals intent and if you focus or hover link, actually just prefetch all that stuff with html link tags

- Route Fetching
	- "Data Diff" only loads the data for changing layouts
	- nested routes which part of the page is changing which box is should go into a pending state

## One more thing

- Server Fetching
	- blocked by data (TTFB)
		- indirectly through the document, CSS and images especially problematic because they block FCP/LCP!
	--> send tiny chunk of the document
- Streaming
	- TTFB, FCP
		- faster
			- initiate fetching on the server but fallback ASAP for fastest TTFB, FCP
	- CLS
		- falling back unblocks the resources from the document
	- LCP, TTI
		- faster
			- javascript, CSS, fonts, images download in parallel with the document

- Server Fetching w/ Cache
	- Streaming과 동일한 퍼포먼스를 갖고 같은 시각에 인지한다.

- levers less CLS vs TTFB, FCP, LCP, TTI

## Demo
