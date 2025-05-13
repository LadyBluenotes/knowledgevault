- `Set` is a collection of **unique values** (no duplicates).
- No keys, only values.
- Values can be of any type.
- Great for tracking **unique items** without manual duplication checks.
- Faster and more optimized than using an `Array` with `find()` or `includes()` for uniqueness.
- If an iterable (e.g., array) is provided, its values are added to the Set.

```js
let set = new Set([iterable]);
```

- Duplicate values are automatically ignored.

```js
let set = new Set();
set.add(john);
set.add(mary);
set.add(john); // ignored
console.log(set.size); // 2
```

## Properties and methods

| Property | Description                             |
| -------- | --------------------------------------- |
| size     | Returns the number of elements in a Set |

| Method    | Description                                                  |
| --------- | ------------------------------------------------------------ |
| new Set() | Creates a new Set                                            |
| add()     | Adds a new element to the Set                                |
| clear()   | Removes all elements from a Set                              |
| delete()  | Removes an element from a Set                                |
| entries() | Returns an Iterator with the \[value,value] pairs from a Set |
| forEach() | Invokes a callback for each element                          |
| has()     | Returns true if a value exists                               |
| keys()    | Same as values()                                             |
| values()  | Returns an Iterator with the values in a Set                 |

## Iterating over

- Supports `for..of` and `forEach` loops
  - `forEach` uses 3 arguments (value, valueAgain, set) for **Map compatibility**.

```js
for (let value of set) console.log(value);

set.forEach((value, valueAgain, set) => {
  console.log(value); // value === valueAgain
});
```
