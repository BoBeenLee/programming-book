
[Reactjs - Speed up Server Side Rendering - Sasha Aickin](https://www.youtube.com/watch?v=PnpfGy7q96U)

1. Production Mode
+ Why?<br/>
There's a TON of error checking in React in dev mode,
which makes it very slow

### Downsides
No real downside; just do it!

2. Use Minified React
Yes, in node.
Yes, even though node doesn't need minified JS.
```
Change
import ReactDOMServer from "react-dom/server"
to 
import ReactDOMServer from "react/dist/react.min"
```

Why?
Main reason seems to be that checking process.env.NODE_ENV is expensive.

### Downsides
Makes the server harder to debug.
Removes a lot of great dev warnings.

3. Babel Transforms
Constant Elements finds constant JSX
elements and hoists them to a higher scope
so they are not re-instantiated every time 
the render method runs.

Inline Elements gets rid of all calls to 
React.createElement and replaces them with
literal objects.

Then add to Babel config:
```
"plugins": ["transform-react-constant-elements", "transform-react-inline-elements"]
```
Note that constant elements needs to be before inline elements.

### Downsides
Requires a Babel build step.

4. Avoid createClass

5. Streaming
react-dom's renderToString returns a fully-rendered String.

<b>react-dom-stream</b>

TTFB statys constant as the content gets longer.
TTLB scales linearly with content length,
roughly the same as react-dom.

Finally, Change all your calls to renderToString to return a Stream.

### Downsides
Beta quality. Need to decide what your risk tolerance is,
but relatively trivial to remove.

Intervening proxies might defeat streaming ( especially CDNs ).

6. Cache Components
Page-level caching is way too coarse.
We need component-level caching.

(props, state) => string
then we can cache (or memoize) to speed it up.

Add a cache object to the renderToString method.

```
ReactDOMServer.renderToString(<Foo />).pipe(res);

to

const cache = new LRURenderCache();
ReactDOMServer.renderToString(<Foo />, {cache: cache}).pipe(res);

Add a method called componentCacheKey()
componentCacheKey() {
	return JSON.stringify(this.props);
}
```

### Downsides
Alpha quality, hasn't been tried in production yet.
If the cache has low hit rate, caching is a net negative.
Very dangerous! If you get the cache key wrong,
you can serve data to the wrong person.

Should I Use These 6 Weird Tricks?
+ Production Mode: Yes!
+ Minified React: Yes!
+ Babel Transforms: Yes!
+ ES6 Classes & Stateless Components: Maybe.
+ Streaming: Maybe.
+ Cache: Probably Not Yet.
