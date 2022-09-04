# CSS Transform Is Dead! Use This Instead

- https://www.youtube.com/watch?v=416MT-VmJdI

## transform의 문제점

- transform 속성이 override되기에 여러 transform속성을 지정할 수가 없다.

```
.box.small {
	transform: scale(.5);
}
.box.moved {
	transform: translate(50px);
}

<div class="box small moved" />
```

### Solution

- 각 css 속성별 설정을 지정한다.

```
.box.small {
	scale: .5;
}
.box.moved {
	translate: 50px;
}

<div class="box small moved" />
```

## Case2

- really janky animation

```
.box {
    width: 100px;
    height: 100px;
    background-color: blue;
    transform: scale(var(--scale, 1))
        translate(var(--translate, 0))
        rotate(var(--rotate, 0))
}
.box.small {
	--scale: .5;
}
.box.moved {
	--translate: 50px;
}
.box:hover {
    animation: rotate 500ms infinite alternate;
}

@keyframes rotate {
    0% {
        --rotate: 0;
    }
    100% {
        --rotate: 45deg;
    }
}

<div class="box small moved" />
```

### Solution

```
.box {
    width: 100px;
    height: 100px;
    background-color: blue;
}
.box.small {
	scale: .5;
}
.box.moved {
	translate: 50px;
}
.box:hover {
    animation: rotate 500ms infinite alternate;
}

@keyframes rotate {
    0% {
        rotate: 0;
    }
    100% {
        rotate: 45deg;
    }
}

<div class="box small moved" />
```
