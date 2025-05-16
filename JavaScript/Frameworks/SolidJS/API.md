## `createSelector`

- Creates a conditional signal that only notifies subscribers when entering or exiting their key matching the value

```ts
function createSelector<T, U>(
source: () => T
fn: (a: U, b: T) => boolean,
options?: { name?: string }
): (k: U) => boolean;
```

## `createSignal`

- Creates a simple reactive state with a getter and setter
  - `value`: initial value of the state
    - If empty, state’s type will automatically extend with undefined
    - If not empty, extend the type manually if you want setting to `undefined` to not error
  - `options`: optional object used for debugging purposes
    - `name`: optional string to assign a custom name
    - `equals`: comparator function for the previous and next value to allow fine-grained control over the reactivity
        - if `false`, value is always considered changed and updates will *always* trigger
        - if a function, it should compare the previous and next values and return `true` if they’re equal (no update), or `false` if they are different (trigger an update)

```typescript
function createSignal<T>(
  value: T,
  options?: {
    name?: string;
    equals?: false | ((prev: T, next: T) => boolean);
  },
);
```

- Returns a tuple
```ts
[state: Accessor<T>, setState: Setter<T]
```
