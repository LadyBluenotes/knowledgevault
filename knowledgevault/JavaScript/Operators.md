## Equality

- Checks whether its two operands are equal
- Returns a _boolean_
- Attempts to _convert_ and compare operands that are of different types

```ts
console.log(1 == 1);
// Expected output: true

console.log("hello" == "hello");
// Expected output: true

console.log("1" == 1);
// Expected output: true

console.log(0 == false);
// Expected output: true
```

### Strict Equality

- Checks whether two operands are equal
- Returns a _boolean_
- Considers operands of different _types_ to be different

```ts
console.log(1 === 1);
// Expected output: true

console.log("hello" === "hello");
// Expected output: true

console.log("1" === 1);
// Expected output: false

console.log(0 === false);
// Expected output: false

"3" === 3; // false

true === 1; // false

null === undefined; // false

3 === new Number(3); // false

const object1 = {
  key: "value",
};

const object2 = {
  key: "value",
};

console.log(object1 === object2); // false
console.log(object1 === object1); // true
```

- Numbers must have the same numeric values. `+0` and `-0` are considered to be the same value.

* Strings must have the same characters in the same order.
* Booleans must be both `true` or both `false`.

### Objects

- Will only evaluate to true when the _same object_

```ts
const object1 = {
  key: "value",
};

const object2 = {
  key: "value",
};

console.log(object1 == object2); // false
console.log(object1 == object1); // true
```

### Strings and String objects

- If a string was constructed using `new String()`, if compared to a _string literal_, the `String` object will be converted to a string literal and contexts will be compared
- If _both_ are `String` objects, they are compared as _objects_ and must reference the _same object_ to succeed

```ts
const string1 = "hello";
const string2 = String("hello");
const string3 = new String("hello");
const string4 = new String("hello");

console.log(string1 == string2); // true - both to string literals
console.log(string1 == string3); // true - both to string literals
console.log(string2 == string3); // true - comparing existing `String` object to a new one
console.log(string3 == string4); // false - comparing two different `String` objects
console.log(string4 == string4); // truesame object
```
