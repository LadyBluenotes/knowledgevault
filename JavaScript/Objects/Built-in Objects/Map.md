- a collection of keyed data items
- keys can be of any time (unlike plain objects which convert keys to strings)
- Uses **SameValueZero** comparison:
  - Similar to `===`, **but** `NaN === NaN` is `true` in Map.
  - Allows `NaN` as a key.

```js
let map = new Map();
```

## Methods and properties

| Method    | Description                                                     |
| --------- | --------------------------------------------------------------- |
| clear()   | Removes all the elements from a Map                             |
| delete()  | Removes a Map element specified by a key                        |
| entries() | Returns an iterator object with the [key, value] pairs in a Map |
| forEach() | Invokes a callback for each key/value pair in a Map             |
| get()     | Gets the value for a key in a Map                               |
| groupBy() | Groups object elements according to returned callback values    |
| has()     | Returns true if a key exists in a Map                           |
| keys()    | Returns an iterator object with the keys in a Map               |
| set()     | Sets the value for a key in a Map                               |
| size      | Returns the number of Map elements                              |
| values()  | Returns an iterator object of the values in a Map               |

`set()` returns the map itself:

```js
map.set("a", 1).set("b", 2).set("c", 3);
```

### Iterating over map

- maintains insertion order
- Iteration methods:
  - `map.keys()` – Iterable of keys
  - `map.values()` – Iterable of values
  - `map.entries()` – Iterable of `[key, value]` pairs (default in `for...of`)

```js
for (let [key, value] of map) {
  console.log(key, value);
}

// Can use forEach like what is used in Array's

map.forEach((value, key) => {...})
```

## Key types and type preservation

- keys are **not converted to strings**
- Avoid using `map[key]` - treats `Map` as a plain object which causes type limitations

### Using objects as keys

- Objects, including functions, can be used as keys
- In plain objects, object keys are converted to `"[object Object]"`.

```js
let john = { name: "John" };
map.set(john, 123);
console.log(map.get(john)); // 123
```

## Map from object

- Convert object to Map using `Object.entries(obj)`:

```js
let obj = { name: "John", age: 30 };
let map = new Map(Object.entries(obj));
```

## Objects from map

- Convert Map to plain object using `Object.fromEntries(map)`:

```js
let obj = Object.fromEntries(map); // same as Object.fromEntries(map.entries())
```
