# React.js TypeScript Conditional Props - Props that depend on other Props
- https://www.youtube.com/watch?v=vXh4PFwZFGI&t=228s

## Discriminating Unions
```ts
export type DrawerProps = { fullName: string; } & ({
	shape: 'circle';
	radius: number;
} | {
	shape: 'square';
	width: number;
} | {
	shape: 'rectangle';
	width: number;
	height: number;
});

```

## Only one property or the other, not both!
```ts
type OneOrTheOtherProps = {
	collapesed?: true; expanded?: never;
} | {
	collapesed?: never; expanded?: true;
}

export function OneOrTheOther(props: OneOrTheOtherProps) {
	return <pre>{JSON.stringify(props)}</pre>
}

function DebugWhileDeveloping() {
	return <OneOrTheOther collapsed />
}

```


## props defaultCollapsed can only be used when collapsable is set

```ts
type PanelProps = {
	collapsable: true;
	defaultCollpsed?: boolean;
} | {
	collapsable?: never;
	defaultCollpsed?: never;
};

export function Panel(props: PanelProps) {
	return <pre>{JSON.stringify(props)}</pre>
}

function DebugWhileDeveloping() {
	return <Panel collapsable defaultCollpsed={false} />
}

```

## Dropdown - label and value props only available when data is an array of objects. Label and Value props have autocomplete for the properties passed in data.
```ts
type DropdownProps<T> = T extends number | string ? {
	data: Array<string | number>;
	labelProps?: never;
	valueProps?: never;
} : {
	data: Array<T>;
	labelProps?: keyof T;
	valueProps?: keyof T;
}

export function Dropdown<T>(props: DropdownProps<T>) {
	return <pre>{JSON.stringify(props)}</pre>
}

function DebugWhileDeveloping() {
	return <Dropdown data={[{id: 5, name: "bruno"}]} labelProps="name" valueProps="name" />
}

```
