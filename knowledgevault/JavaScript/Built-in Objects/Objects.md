## Iterative & transformative

### Object.entries()

Return array of an object's own key-value pairs where each pair is an array of two elements: string key and corresponding value.

```js
const example: {
	a: "string"
	b: 123
}

for (const [key, value] of Object.entries(example)) {
	console.log(`${key}: ${value}`)
}

// Expected output:
// "a: string"
// "b: 123"
```

## Inspection

### hasOwnProperty()

Returns a _boolean_ indicating whether an object has the _specified property_.

```jsx
const tempObject = {
  property1: "I'm here",
};

console.log(tempObject.hasOwnProperty("property1")); // output: true
```

## Looping

### `for ... in`

Iterates over the _enumerable property keys_ of an object.

```js
for (const key in object) {
  // ..
}
```

### `for ... of`

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
