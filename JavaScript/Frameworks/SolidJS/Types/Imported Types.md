---
title: Imported Types
date created: Friday, May 16th 2025, 11:37:50 am
date modified: Friday, May 16th 2025, 11:44:27 am
---

# Imported Types

## Basic

### `Accessor`

- Function that returns the current value and registers each call to the reactive root

```ts
type Accessor<T> = () => T;
```

### `Ref`

- Type of `props.ref` for use in `Component` or `props`

```ts
type Ref<T> = T | ((val: T) => void);
```

### `Setter`

- A function that allows directly setting or mutating a value

```ts
type Setter<in out T> = {
  <U extends T>(
    ...args: undefined extends T
      ? []
      : [value: Exclude<U, Function> | ((prev: T) => U)]
  ): undefined extends T ? undefined : U;

  <U extends T>(value: (prev: T) => U): U;

  <U extends T>(value: Exclude<U, Function>): U;

  <U extends T>(value: Exclude<U, Function> | ((prev: T) => U)): U;
};
```

### `Signal`

```ts
type Signal<T> = [get: Accessor<T>, set: Setter<T>];
```

## Components

### `Component`

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

### `ParentComponent`

- Use for components where you need a specific child type, typically a function that receives specific argument types

```ts
type ParentComponent<P extends Record<string, any> = {}> = Component<
  ParentProps<P>
>;
```

- Extend props to require `children` prop with specified type

### `VoidComponent`

- Used to prevent accidentally passing `children` to to components that would silently throw them way
- Forbids the `children` prop

```ts
type VoidComponent<P extends Record<string, any> = {}> = Component<
  VoidProps<P>
>;
```

## Props

### `ComponentProps`

- Takes the props of the passed component and returns its type

```ts
type ComponentProps<T extends ValidComponent> =
  T extends Component<infer P>
    ? P
    : T extends keyof JSX.IntrinsicElements
      ? JSX.IntrinsicElements[T]
      : Record<string, unknown>;
```

### `FlowProps`

- Used for components where you need a specific child type, typically a function that receives specific argument type
- Extend to require `children` prop with the specified type

```ts
type FlowProps<P extends Record<string, any> = {}, C = JSX.Element> = P & {
  children: C;
};
```

### `MergeProps`

```ts
type MergeProps<T extends unknown[]> = Simplify<_MergeProps<T>>;
```

### `ParentProps`

- Use for components that you want to accept children

```ts
type ParentProps<P extends Record<string, any> = {}> = P & {
  children?: JSX.Element;
};
```

- Optional `children` prop
  - `JSX.Element` ← Allows elements, arrays, functions, etc.

### `SplitProps`

```ts
type SplitProps<T, K extends (readonly (keyof T)[])[]> = [
  ...{
    [P in keyof K]: P extends `${number}`
      ? Pick<T, Extract<K[P], readonly (keyof T)[]>[number]>
      : never;
  },

  {
    [P in keyof T as Exclude<P, K[number][number]>]: T[P];
  },
];
```

### `VoidProps`

- Use to prevent accidentally passing `children` to components that would silently throw them away
- Extends to forbid the `children` prop

```ts
type VoidProps<P extends Record<string, any> = {}> = P & {
  children?: never;
};
```

## Resource

### `InitializedResource`

```ts
type InitializedResource<T> = Ready<T> | Refreshing<T> | Errored;
```

### `InitializedResourceOptions`

```ts
type InitializedResourceOptions<T, S = unknown> = ResourceOptions<T, S> & {
  initialValue: T;
};
```

### `InitializedResourceReturn`

```ts
type InitializedResourceReturn<T, R = unknown> = [
  InitializedResource<T>,
  ResourceActions<T, R>,
];
```

### `Resource`

```ts
type Resource<T> = Unresolved | Pending | Ready<T> | Refreshing<T> | Errored;
```

### `ResourceActions`

```ts
type ResourceActions<T, R = unknown> = {
  mutate: Setter<T>;
  refetch: (info?: R) => T | Promise<T> | undefined | null;
};
```

### `ResourceFetcher`

```ts
type ResourceFetcher<S, T, R = unknown> = (
  k: S,

  info: ResourceFetcherInfo<T, R>,
) => T | Promise<T>;
```

### `ResourceFetcherInfo`

```ts
type ResourceFetcherInfo<T, R = unknown> = {
  value: T | undefined;

  refetching: R | boolean;
};
```

### `ResourceOptions`

```ts
type ResourceOptions<T, S = unknown> = {
  initialValue?: T;
  name?: string;
  deferStream?: boolean;
  ssrLoadFrom?: "initial" | "server";
  storage?: (
    init: T | undefined,
  ) => [Accessor<T | undefined>, Setter<T | undefined>];
  onHydrated?: (
    k: S | undefined,
    info: {
      value: T | undefined;
    },
  ) => void;
};
```

### `ResourceReturn`

```ts
type ResourceReturn<T, R = unknown> = [
  Resource<T>,
  ResourceActions<T | undefined, R>,
];
```

### `ResourceSource`

```ts
type ResourceSource<S> =
  | S
  | false
  | null
  | undefined
  | (() => S | false | null | undefined);
```
