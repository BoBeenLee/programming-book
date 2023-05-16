# The Power of TypeScript Generics

- https://www.youtube.com/watch?v=0Mr3t0zA4SY

```tsx
type DropdownOption = { value: string };

type DropdownProps<T extends ReadonlyArray<DropdownOption>> = {
  options: T;
  onSelect: (arg: T[number]) => void;
};

declare function Dropdown<T extends ReadonlyArray<DropdownOption>>(
  props: DropdownProps<T>
): void;

Dropdown({
  options: [
    { value: "gadget" as const },
    { value: "widget" as const },
    { value: "foobar" as const },
  ] as const,
  onSelect: (arg) => {
    console.log(arg.value);
  },
});
```
