- Data structure that allows key-value pairs
  - Distinct keys are mapped to a value that can be any JavaScript [data type](obsidian://open?vault=knowledgevault&file=JavaScript%2FData%20Types%2FOverview%20-%20Data%20Types)
- Store keyed collections of various data and more complex entities
- Can be created with figure brackets `{...}` (aka “object literal”) or using `new Object()`
  - Made with an optional list of properties
    - Properties are a `key: value` pair, where `key` is a string (aka “property name”) and `value` can be anything

### `Object()` constructor
- Turns the input into an object

```js
new Object()
new Object(value)

Object()
Object(value)

const o = new Object();
o.foo = 42;

console.log(o);
// { foo: 42 }
```

## Literals and properties

- A property has a key (aka “name” or “identifier”) before the colon `:` and a value to the right of it

```js
let user = {
	name: "Sarah"
	age: 30
}
```

- Properties are accessed using dot notation

```js
user.name; // Sarah
user.age; // 30
```

- Properties can be of any data type and can be removed using the `delete` operator

```js
user.isAdmin = true;

delete user.age;
```

- The last property in the list may end with a comma, commonly called the “trailing” or “hanging” comma
  - Makes it easier to add/remove/move around properties because all lines are alike

### Square brackets

- For multiword properties, dot access does not work
  - Dot requires a key be a valid variable identifier which implies no spaces, doesn’t start with a digit, and doesn’t include any special characters aside from `$` or `_`
- The alternative is to use square bracket notation

```js
let user = {};

// set
user["likes cats"] = true;

// get
user["likes cats"]; // true

// delete
delete user["likes cats"];
```

- More powerful than dot notation since they allow any property name or variable
  - Due to how complex the names can get, property names are best kept simple so dot notation can be used but if there’s a need for more complex ones, square brackets can be used

#### Computed properties

- Square brackets can be used in an object literal when creating an object - these are called computed properties
  - The meaning of a computed property is that the property name should be taken from the variable

```js
let fruit = "apple";
let bag = {
  [fruit]: 5,
};
bag.apple; // 5

// or

let fruit = "apple";
let bag = {};
bag[fruit] = 5;
```

- More complex expressions can be used inside square brackets

```js
let fruit = "apple";
let bag = {
  [fruit + "Computers"]: 5, // bag.appleComputers = 5
};
```

## Property value shorthand

- Existing variables can be used as values for property names

```js
function makeUser(name, age) {
  return {
    name: name,
    age: age,
    // ...other properties
  };
}

let user = makeUser("John", 30);
alert(user.name); // John
```

- Since doing this is so common, there’s a shorthand used to make it shorter:

```js
function makeUser(name, age) {
  return {
    name, // same as name: name
    age, // same as age: age
    // ...
  };
}

// can be mixed as well
let user = {
  name, // same as name:name
  age: 30,
};
```

### Property name limitations

- Unlike variable names, object properties do not have a restriction on language-reserved words
- There are no limitations on property names, they can be [strings]([[Strings]]) or [symbols]([[Symbol]]l) and other types will just be automatically converted to strings (`0` → `"0"`)
- The only limitation is `__proto__` but that is related to [prototypes]([[Prototypes]])

## Property existence test

- Reading a non-existing property just returns `undefined`
- There’s also a special operator `"in"`
  - Left side of `in` must be a property name in the form of a quoted string
  - Better to use because if a property exists but _stores_ `undefined`, comparing it to `undefined` will show an unintended `true`

```js
let user = {
  name: "Sarah",
  age: 30,
};

user.noSuchProperty === undefined; // true
"age" in user; // true
"blabla" in user; // false
```

> Note that having `undefined` being explicitly assigned is not recommended. `Null` should be used for “unknown” or “empty” values

## `for...in` loop

- To walk over all keys, you can use the `for...in` loop

```js
for (key in object) {
  // executes the body for each key among object properties
}
```

## Object orders

- Objects are ordered in a special fashion
  - Integer properties are sorted, others appear in creation order
	  - Integer properties mean a string that can be converted to-and-from an integer without a change
	  - If keys are non-integer, then they are listed in order of creation
- Object may be used to suggest a list of options to the user

```js
let codes = {
  49: "Germany",
  41: "Switzerland",
  44: "Great Britain",
  // ..,
  1: "USA",
};

for (let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```



Resources:

- https://javascript.info/object
