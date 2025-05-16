## Basic

### Accessor

```ts
type Accessor<T> = () => T;
```

### Ref

- Type of `props.ref` for use in `Component` or `props`

```ts
type Ref<T> = T | ((val: T) => void);
```

## Components

### Component

- General component with no implicit `children` prop
- Can specify one as in `Component<{name: String, children: JSX.Element}>`

```ts
type Component<P extends Record<string, any> = {}> = (props: P) => JSX.Element;
```

### Flow Component

- Used for components where a specific child type is needed, typically a function that receives a specific argument type
- Requires a `children` prop with a specified type

```ts
type FlowComponent<
  P extends Record<string, any> = {},
  C = JSX.Element,
> = Component<FlowProps<P, C>>;
```

### Parent Component

- Use for components where you need a specific child type, typically a function that receives specific argument types

```ts
type ParentComponent<P extends Record<string, any> = {}> = Component<
  ParentProps<P>
>;
```

- Extend props to require `children` prop with specified type

### Void Component

- Used to prevent accidentally passing `children` to to components that would silently throw them way
- Forbids the `children` prop

```ts
type VoidComponent<P extends Record<string, any> = {}> = Component<
  VoidProps<P>
>;
```

## Props

### Component Props

- Takes the props of the passed component and returns its type

```ts
type ComponentProps<T extends ValidComponent> =
  T extends Component<infer P>
    ? P
    : T extends keyof JSX.IntrinsicElements
      ? JSX.IntrinsicElements[T]
      : Record<string, unknown>;
```

### Flow Props

- Used for components where you need a specific child type, typically a function that receives specific argument type
- Extend to require `children` prop with the specified type

```ts
type FlowProps<P extends Record<string, any> = {}, C = JSX.Element> = P & {
  children: C;
};
```

### Merge Props

```ts
type MergeProps<T extends unknown[]> = Simplify<_MergeProps<T>>;
```

### Parent Props

- Use for components that you want to accept children

```ts
type ParentProps<P extends Record<string, any> = {}> = P & {
  children?: JSX.Element;
};
```

- Optional `children` prop
  - `JSX.Element` ← Allows elements, arrays, functions, etc.

### Void Props

- Use to prevent accidentally passing `children` to components that would silently throw them away
- - Extends to forbid the `children` prop

```ts
type VoidProps<P extends Record<string, any> = {}> = P & {
  children?: never;
};
```
