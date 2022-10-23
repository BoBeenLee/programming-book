# Top 10 Javascript One Liners YOU MUST KNOW!
## Designer Mode
```
document.designMode = "on"
```

## Merging Array

```ts
const arr1 = ["a", "b", "c"];
const arr2 = ["c", "d", "e"];

const merge = [...new Set([...arr1, ...arr2])];

```

## Extracting from Objects
```
const user = {
	age: 27,
	tweets: 20,
	todo: ["a", "b"]
}
const { age, tweets, todo: [a, b]} = user;
```

## Transitionend Event
```ts
const button = document.querySelector('button');
button.addEventListener('click', () => {
	button.style.opacity = 0;
});

button.addEventListener('transitionend', () => button.style.display = 'none');

```

## Screen Capture
- https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia#examples
