## [Composition](https://www.youtube.com/watch?v=qJgff2spvzM)
- mechanism to combine simple functions to build more complicated ones

```
Ramda, lodash/fp
pipe(a, b, c, d) == compose(d, c, b, a)


import { compose } from 'ramda'
==
import { compose } from 'lodash/fp'
== 
import { compose } from 'recompose'
==
import { compose } from 'react-apollo'
```

### Creation > Consumption

### Back to Function

### Goal for Color API
"provide a set of composeable color functions"

### 3 requirement
1. every function must accept and return a CSS colour string
```
don't
lighten(0.3, '#422').toCSS()
lighten(0.3, '#422').toString()
```

2. a color function accepts all arguments except the last and return a function that accepts the color as argument

```
const colorFunc = compose(
	saturate(0.3),
	lighten(0.3)
);
const newColor = colorFunc('#422');

const lightenWith03 = lighten(0.3);
const newColor = lightenWith03('#422');
==
const newColor = lighten(0.3)('#422');
!=
const newColor = lighten(0.3, '#422');
```

### Currying
- currying is the technique of translating the evaluation of a function that takes multiple arguments ( or a tuple of arguments ) into evaluating a sequence of functions, each with a single argument

### Higher-order Function
- function is a function that does at least one of the following:
	- takes one or more functions as arguemtns
	- returns a function as its result

3. the argument to be modified must be at the last argument
```
lighten('#422', 0.3) => lighten(0.3, '#422')
```

e.g.
```
const withLoadingIndicator = Component => props => {
	if(props.data.loading) {
		return <div>Loading</div>;
	}
	return <Component {...props} />;
}

const ProfilePage = props => (
	<div>
		{props.data.username}
	</div>
);

export default compose(
	graphql(ProfilePageQuery),
	withLoadingIndicator,
	withErrorMessage
)(ProfilePage);
```

### Feature Request
- We need a custom loading text for every page.

```
const withLoadingIndicator = text => Component => props => {
	if(props.data.loading) {
		return <div>{text}</div>;
	}
	return <Component {...props} />;
}

const ProfilePage = props => (
	<div>
		{props.data.username}
	</div>
);

export default compose(
	graphql(ProfilePageQuery),
	withLoadingIndicator('loading.....'),
	withErrorMessage
)(ProfilePage);
```

### Higher-order Components
- a higher-order component is a function that takes a component and returns a new component

```
import React from 'react';
import { asset, Sphere, View } from 'react-vr';

...
export default withInfiniteRotation({ axis: 'y', speed: 2000 })(Earth);
```

Components are the primary unit of code reuse in React. <br />
However, you'll find that some patterns aren't a straightforward fit for traditional components. <br />
Use Higher-order Components for cross-cutting concerns.
