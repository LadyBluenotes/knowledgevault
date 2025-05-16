## Accessor

```ts
type Accessor<T> = () => T;
```

## Component
- General component with no implicit `children` prop
- Can specify one as in ``

```ts
type Component<P extends Record<string, any> = {}> = (props: P) => JSX.Element;
```

## Flow Props

```ts
type FlowProps<P extends Record<string, any> = {}, C = JSX.Element> = P & {
  children: C;
};
```

## Parent Props

- Use for components that you want to accept children

```ts
type ParentProps<P extends Record<string, any> = {}> = P & {
  children?: JSX.Element;
};
```

- Optional `children` prop
  - `JSX.Element` ← Allows elements, arrays, functions, etc.

## Parent Component

- Use for components where you need a specific child type, typically a function that receives specific argument types

```ts
type ParentComponent<P extends Record<string, any> = {}> = Component<
  ParentProps<P>
>;
```

- Extend props to require `children` prop with specified type
