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

```typescript
function createSignal<T>(value: T, options?: SignalOptions<T>): Signal<T>;
```

- Creates a simple reactive state with a getter and setter

  - `value`: initial value of the state
    - If empty, state’s type will automatically extend with undefined
    - If not empty, extend the type manually if you want setting to `undefined` to not error
  - `options`: optional object used for debugging purposes

- Returns a tuple with an [Accessor](Imported%20Types.md#Accessor) and [Setter](Imported%20Types.md#Setter)

```ts
[state: Accessor<T>, setState: Setter<T>]
```

### Interfaces

```ts
interface SignalOptions<T> extends MemoOptions<T> {
  internal?: boolean;
}
```


## 