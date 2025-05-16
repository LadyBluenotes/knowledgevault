---
title: API
date created: Friday, May 16th 2025, 11:05:30 am
date modified: Friday, May 16th 2025, 12:24:36 pm
---

# API

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
    - If empty, state's type will automatically extend with undefined
    - If not empty, extend the type manually if you want setting to `undefined` to not error
  - `options`(optional): object used for debugging purposes
    - `name` (optional): string to assign a custom name
    - `equals`(optional): comparator function for the previous and next value to allow fine-grained control over the reactivity
      - if `false`, value is always considered changed and updates will _always_ trigger
      - if a function, it should compare the previous and next values and return `true` if they're equal (no update), or `false` if they are different (trigger an update)
    - `interal` (optional): 

- Returns a tuple with an [Accessor](Imported%20Types.md#Accessor) and [Setter](Imported%20Types.md#Setter)

```ts
[state: Accessor<T>, setState: Setter<T>]
```

### Interfaces

```ts
interface BaseOptions {
  name?: string;
}

interface EffectOptions extends BaseOptions {}

interface MemoOptions<T> extends EffectOptions {
  equals?: false | ((prev: T, next: T) => boolean);
}

interface SignalOptions<T> extends MemoOptions<T> {
  internal?: boolean;
}
```
