# Get a sneak peek of Framer Motion Recipes!

- https://www.youtube.com/watch?v=lpywNeB3EnU&list=WL&index=2

## Check Steps

- framer motion을 이용한 선언적 애니메이션 구현 방법

```
<motion.div animate={status}>
	<motion.div
		variants={{
			active: {
				scale: 1,
				transition: {
					delay: 0,
					duration: 0.2,
				}
			},
			complete: {
				scale: 1.25
			},
		}}
		transition={{
			duration: 0.6,
			delay: 0.2,
			type: 'tween',
			ease: 'circOut',
		}}
		className="absolute ..."
	></motion.div>

	<motion.div initial={false}
		variants={{
			inactive: {...},
			active: {...},
			complete: {...}
		}}
		className="flex ..."
		>
		CheckIcon or Number
	</motion.div>
</motion.div>
```
