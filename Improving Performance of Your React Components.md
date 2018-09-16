[Improving Performance of Your React Components](https://www.youtube.com/watch?v=y8b57Y5Q1s4&list=WL&index=3&t=0s)

Finding the culprits
- why did you update

Why are they slow?
- Excess renders
- Excess reconciliations

What causes excess reconciliations?
- Passing down unnecessary props
  <Component {...rest} />
- Object literals defined in render
  <Component style={{ margin: 0 }} />
- Anonymous functions defined in render
  <Component onChange={(e) => this.handleChange(e)}

How to reduce reconciliations
- Define constants and bind functions outside of render

```
<Component onChange={(e) => this.handleChange(e)} />
```
->
```
<Component onChange(this.handleChange) />
```

```
<Component style={{ margin: 0 }} />
```
->

```
const myStyles = { marign: 0 };
<Component style={myStyles} />
```

<Component {...rest} />
->
<Component neccesary={neccesary} />

- PureComponent
```
MyComponent extends React.PureComponent {}

shouldComponentUpdate(nextProps, nextState) {
	return this.props !== nextProps && this.state !== nextState;
}
```

Alternative for Functional Components
- recompose
  - pure
  - updateOnlyForKeys

  ```
  import { lifecycle, compose , pure } from "recompose";
  ...
  export default compose(withLifecycle, pure)(Component);
  ```

In Summary
- Use tools to find problematic components
  - why-did-you-update
  - performance dev tools
- reduce unnecessary reconciliations
  - shouldComponentUpdate()
  - PureComponent
  - Define constants and functions outside of render()
- Keep Your components rendering based only on (preferably immutable) state/props







