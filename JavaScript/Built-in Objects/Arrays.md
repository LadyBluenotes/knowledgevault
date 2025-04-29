---
title: Arrays
date created: Tuesday, April 22nd 2025, 11:01:12 am
date modified: Tuesday, April 22nd 2025, 11:28:49 am
---

# Arrays

## Modification

### push(_element 1…. elementN_)

`Array.push()` adds the specified elements to the _end_ of an array and returns the new length of the array.

```jsx
const animals = ["pigs", "goats", "sheep"];

const count = animals.push("cows");
console.log(count);
// Expected output: 4
console.log(animals);
// Expected output: Array ["pigs", "goats", "sheep", "cows"]
```

_Returns_ the length property of the object upon which the method was called.

## Iterative

### filter(_callbackFn, thisArg_)

`Array.filter` creates a _shallow copy_ of a portion of a given array, filtered down to just the elements from the given array that _pass the test implemented by the given function_. Constructs a _new array_ of all values for which the `callbackFn` returns a truthy value.

```jsx
const words = ["spray", "elite", "exuberant", "destruction", "present"];

const result = words.filter((word) => word.length > 6);

console.log(result);
// Expected output: ["exuberant", "destruction", "present"]
```

`callbackFn` - should return a truthy value to indicate the element passes the test (or falsy otherwise). Only invoked for array indexes _with values._

- `element` - current element being processed
- `index` - index of current element being processed
- `array` - the array the `forEach` was called on
  `thisArg` (optional) - value that is used to set the `this` context of the `callbackFn`.

### some(_callbackFn, thisArg_)

Tests whether _at least one element_ in the array passes the test implemented by the provided function. If **true**, finds an element for which the provided function returns true immediately, otherwise returns **false** and _does not modify the array_. Does not mutate the array but the _callback function can._

```jsx
const array = [1, 2, 3, 4, 5];

const even = (element) => element % 2 === 0;

console.log(array.some(even)); // Expected output: true
```

`callbackFn` - should return a truthy value to indicate the element passes the test (or falsy otherwise). Only invoked for array indexes _with values._

- `element` - current element being processed
- `index` - index of current element being processed
- `array` - the array the `forEach` was called on
  `thisArg` (optional) - value that is used to set the `this` context of the `callbackFn`.

### forEach(_callbackFn, thisArg_)

Executes a provided function _once_ for each array element.

```jsx
const array1 = ["a", "b", "c"];

array1.forEach((element) => console.log(element));

// Expected output: "a"
// Expected output: "b"
// Expected output: "c"
```

`callbackFn` - return value is _discarded_, and is called with the following arguments:

- `element` - current element being processed
- `index` - index of current element being processed
- `array` - the array the `forEach` was called on
  `thisArg` (optional) - value that is used to set the `this` context of the `callbackFn`.

### find(_callbackFn, thisArg_)

Returns the _first element_ in the provided array that satisfies the provided testing function. Returns `undefined` if no values satisfy. Will _not_ mutate the array.

```jsx
const array1 = [5, 12, 8, 130, 44];

const found = array1.find((element) => element > 10);

console.log(found);
// Expected output: 12
```

`callbackFn` - returns a truthy value to indicate a match, and falsy otherwise. Invoked at _every_ index. Can mutate the array.

- `element` - current element being processed
- `index` - index of current element being processed
- `array` - the array the `forEach` was called on
  `thisArg` (optional) - value that is used to set the `this` context of the `callbackFn`.

### findIndex(_callbackFn, thisArg_)

Returns the _index_ of the _first element_ in an array that satisifies the provided testing function.

```jsx
const array1 = [5, 12, 8, 130, 44];

const isLargeNumber = (element) => element > 13;

console.log(array1.findIndex(isLargeNumber));
// Expected output: 3
```

`callbackFn` - returns a truthy value to indicate a match, and falsy otherwise. Calls in an _ascending-index_ order at _every_ index.

- `element` - current element being processed
- `index` - index of current element being processed
- `array` - the array the `forEach` was called on
  `thisArg` (optional) - value that is used to set the `this` context of the `callbackFn`.

### indexOf(_searchElement, fromIndex_)

Returns the _first index_ at which a given element can be found in the array or `-1` if it is not present. compares to elements of the array using _strict equality_. Empty slots are skipped/

```jsx
const beasts = ["ant", "bison", "camel", "duck", "bison"];

console.log(beasts.indexOf("bison"));
// Expected output: 1

// Start from index 2
console.log(beasts.indexOf("bison", 2));
// Expected output: 4

console.log(beasts.indexOf("giraffe"));
// Expected output: -1
```

`searchElement` is the element to _locate_.

`fromIndex` (optional) - zero-based index at which to start searching

- Negative index counts from the back of the array
  - if `fromIndx < 0` then `fromIndex + array.length` will be used
  - if `fromIndex < -array.length` or `fromIndex` is omitted, `0` is used and entire array will be searched.
  - If `fromIndex >= array.length`, the array is not searched and `-1` is returned

### includes(_searchElement, fromIndex_)

Determines whether an array _includes_ a certain value among its entries, returning `true` or `false` as appropriate.

```jsx
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// Expected output: true

const pets = ["cat", "dog", "bat"];

console.log(pets.includes("cat"));
// Expected output: true

console.log(pets.includes("at"));
// Expected output: false
```

`searchElement` is the element to _locate_.

`fromIndex` (optional) - zero-based index at which to start searching

- Negative index counts from the back of the array
  _ if `fromIndx < 0` then `fromIndex + array.length` will be used
  _ if `fromIndex < -array.length` or `fromIndex` is omitted, `0` is used and entire array will be searched. \* If `fromIndex >= array.length`, the array is not searched and `-1` is returned
  **\*Note:** Values of zero are all considered to be equal, regardless of sign.\*
