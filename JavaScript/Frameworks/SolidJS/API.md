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
- Returns 

```typescript
const [state: Accessor<T>, setState: Setter<T>] = createSignal<T>(
    value: T,
    options?: { 
        name?: string, 
        equals?: false | ((prev: T, next: T) => boolean) 
        }
    )
```

