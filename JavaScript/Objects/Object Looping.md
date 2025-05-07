---
title: Objects
date created: Tuesday, April 22nd 2025, 11:01:34 am
date modified: Tuesday, April 22nd 2025, 11:28:48 am
---

## `for … in`

Iterates over the _enumerable property keys_ of an object.

```js
for (const key in object) {
  // ..
}
```

## `for … of`

Iterates over the _values_ of an iterable object.

```js
for (const values of object) {
  // ..
}
```

## Maps

Holds key-value pairs and _remembers_ the original insertion order of the keys

### Map Methods

#### Set

## Searching Objects

### Finding key by value

```jsx
function getKeyByValues(object, value) {
  return Object.keys(object).find((key) => object[key] === value);
}
```
