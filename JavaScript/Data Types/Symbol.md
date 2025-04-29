- Unique and immutable primitive data type introduced in ECMAScript 6
  - Often used to create unique property keys for objects, ensuring no property key collisions occur
- Each Symbol value is distinct, even when multiple are created with the same description
  - Can be created using the `Symbol()` function
- Primary use case is to add hidden / special properties to objects that won’t interfere with other properties or methods
- Only 2 primitive types can serve as object property keys - string or symbol
- At creation time, can give them a description (“symbol name”) that is helpful for debugging purposes
  - Guaranteed to be unique, even if they have the same description

```js
let id = Symbol("id");
let id2 = Symbol("id");

id == id2; // false
```

## “Hidden” properties

- Symbols allow for the creation of “hidden” properties of an object, that no other part of code can accidentally access or overwrite
- To use in an object literal `{...}`, square brackets need to be around it

```js
let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123, // not "id": 123
};
```
 - They are skipped in `for ... in` loops

```js
let id = Symbol("id");
let user = {
  name: "John",
  age: 30,
  [id]: 123
};

for (let key in user) console.log(key); // name, age (no symbols)

// the direct access by the symbol works
alert( "Direct: " + user[id] ); // Direct: 123
```
- Also skipped in `Object.keys`
	- Part of “hiding symbolic properties”
	- Won’t unexpectedly access a symbolic property

- `Object.assign` copies both string **and** symbol properties by design
	- When cloning or merging objects, all properties are usually wanted to be copied (including symbols like `id`)

```js
let id = Symbol("id");
let user = {
  [id]: 123
};

let clone = Object.assign({}, user);

clone[id] // 123
```

## Global symbols
- To access same-named symbols, a *global symbol registry* is needed
	- Can create symbols in it and access them alter and guarantees that repeated accesses by the same name return _exactly_ the same symbol

- To read, or create, a symbol from the registry: `Symbol.for(key)`
	- Checks global registry, if there’s a symbol described as `key`, then it is returned, otherwise it will create a _new symbol_ (`Symbol(key)`) and store it in the registry by the given `key`

```js
let id = Symbol.for("id");
let idAgain = Symbol.for("id");

id === idAgain // true
```

- Inside a registry, Symbols are called *global symbols*
	- Application-wide symbols which are accessible everywhere in the code

## `Symbol.keyFor`
- Returns a name by global symbol
- Internally uses global symbol registry to look up key for symbol
	- Does not work for non-global symbols and will return `undefined`
```javascript
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

Symbol.keyFor(sym) // name
Symbol.keyFor(sym2) // id
```

