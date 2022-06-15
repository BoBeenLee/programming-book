[React and the Three Layers of Testing - Bart Waardenburg](https://www.youtube.com/watch?v=L2yOoxzXmw8)


### Static analysis is the analysis of software that is performed without actually executing programs.

### Using Flow or TypeScript could have prevented 15% of the public bugs for public projects on GitHub.

```javascript
type MyCustomButtonProps = { text: string };

const MyCustomButton = ({ text }: MyCustomButtonProps) => (
	<button>hello</button>
);
```

### You can have every single variable and function completely typed and linted but still have none of your functions doing what they should be doing

### A unit test is a way of testing a unit - the smallest piece of code that can be logically isolated in a system

```javascript
const multiply = (a: number, b: number): number => a + b;

test('Multiply should return the arguments multiplied', () => {
	expect(multiply(4, 3)).toBe(12);
});
```

### A snapshot test verifies that a piece of functionality works the same as it did when the snapshot was created


```javascript
const Button = ({ type }: ButtonProps) => (
	<button className={`btn-${type}`} />
);


test('The Button component renders correctly', () => {
	const component = renderer.create(
		<Button type="good" />
	).toJSON();

	expect(component).toMatchSnapshot();
});
```

### You can have every single component and function unit test passing but still have none of your functions working together like they should

### Integration testing is the phase in software testing in which individual software modules are combined and tested as a group.


```javascript
import { mount } from 'enzyme';

const Button = () => (
	<button 
		onClick={() => mutilply(1, 2)}
		onMouseEnter={() => alertNumber(mutilply(1, 2))}
		>Multiply</button>
);

alertNumber = jest.fn();

test('The Button component should run a function on click', () => {
		const component = mount(<Button type="test" />);
		component.find('button').simulate('click');
		expect(alertNumber).toHaveBeenCalledTimes(1);
});
```

### You can have everything working together completely as intended but still have an empty screen for an application.

```javascript
const multiply = (a: number, b: number): number => a * b;
const alertNumber = (value: number): void => alert(value);

const Button = () => (
	<button 
		onClick={() => alertNumber(multiply(1, 2))}
		>Multiply</button>
);

document.querySelector('body').style.cssText = 'display: none';
```

### User interface testing

### User interface testing is the process of testing a product's graphical user interface to ensure it meets its specifications.


### tools
#### Selenium, Nightmare, Nightwatch, TestCafe, CasperJS, Protractor, Cypress, Puppeteer, Codecept, Navalia, Chromeless

```javascript
import { Chrome } from 'navalia';
import { toMatchImageSnapshot } from 'jest-image-snapshot';

expect.extend({ toMatchImageSnapshot });

const chrome = new Chrome();

test('The routing input component should display as expected', async () => {
	await chrome.goto('http:....');
	await chrome.wait('.ROVE-routing-input');
	const screenshot = await chrome.screenshot('.ROVE-routing-input');
	await chrome.done();

	expect(screenshot).toMatchImageSnapshot();
});
```

```javascript
import { Chromeless } from 'chromeless';

const chromeless = new Chromeless();

const screenshot = await chromeless.goto('http....')
	.screenshot('#routing', {
		base64: true
	});

const file = new Buffer(screenshot, 'base64');
expect(file).toMatchImageSnapshot();
await chromeless.end();
```

1. Local Setup
new Chormeless() ... Chrome runs locally

2. Remote Proxy Setup
```javascript
new Chromeless({
	remote: true
});
Forwards commands via Proxy
via Websockets

new Chromeless();
Chrome runs on AWS Lambda
```

### With chromeless you can run hundreds of browsers in parallel
### You can easily execute > 100.000 tests for free in the free tier

3. User interface testing
2. Integration testing
1. Unit testing
0. Static Analysis
