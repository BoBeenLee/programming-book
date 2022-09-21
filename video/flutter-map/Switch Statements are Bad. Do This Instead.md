# Switch Statements are Bad. Do This Instead.

- https://www.youtube.com/watch?v=baIEys5Ymjw&list=WL&index=5

## Object Literals

### before

```
function getCaffeine(type) {
	let caffeine;
	switch(type) {
		case 'A':
			// A
			break;
		case 'B':
			// B
			break;
		case 'C':
			// C
			break;
	}
	return ;caffeine
}
```

### after

```
function getCaffeine(type) {
	const map = {
		'A': 'A',
		'B': 'B',
		'C': 'C'
	}
	return map[type];
}
```
