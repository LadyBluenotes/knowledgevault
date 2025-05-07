- Objects have a special hidden property `[[Prtotype]]` that is either `null` or references another object called a “prototype”
  - Property is internal and hidden, but there are many ways to set it

## Prototypal inheritance

- Language feature that helps you take an object and extend it
- When a property needs to be read from an object and is missing, JS will automatically take it from the prototype
  - If a prototype has many useful properties and methods, then they automatically become available, or are “inherited”

```js
let animal = {
  eats: true,
};
let rabbit = {
  jumps: true,
};

rabbit.__proto__ = animal; // sets rabbit.[[Prototype]] = animal
```

- With this method, if the property is missing, JS will automatically inherit it from the prototype that was set

```js {8, 11}
let animal = {
  eats: true,
};
let rabbit = {
  jumps: true,
};

rabbit.__proto__ = animal; // (*)

// we can find both properties in rabbit now:
rabbit.eats; // true (**)
rabbit.jumps; // true
```

- Where `(*)` is, the animal is set to the prototype of `rabbit` and when it is read (at `(**)`), JavaScript follows the reference and finds it in `animal`
  - We can say that “`animal` is a protype of `rabbit`” or “`rabbit` prototypically inherits from `animal`”
- Prototype chains can be longer, but there are 2 limitations:
  - References cannot go in circles - an error will be thrown if `__proto__` is assigned in one
  - The value of `__proto__` can either be an object or `null`, other types are ignored
- Additionally, there can only be **one** `[[Prototype]]`. An object _cannot_ inherit from two others

> Note: `__proto__` is a historical getter/setter for `[[Prototype]]`
>
> `__proto__` is _not_ the same as the internal `[[Prototype]]` property. It is a getter/setter **for** `[[Prototype]]`. Using it, however, is a bit outdated but modern JavaScript suggests the use of `Object.getPrototypeOf` or `Object.setPrototypeOf` functions.
>
> `__proto__` must be supported by browsers and other environments, including server-side support so it is safe to use.

### Writing does not use prototype

- Write/delete operations work directly with the object
- Accessor properties are an exception, as assignment is handled by a setter function
  - Writing to such a property, is actually the same as calling a function

```js {19, 22}
let user = {
  name: "John",
  surname: "Smith",

  set fullName(value) {
    [this.name, this.surname] = value.split(" ");
  },

  get fullName() {
    return `${this.name} ${this.surname}`;
  },
};

let admin = {
  __proto__: user,
  isAdmin: true,
};

admin.fullName; // John Smith (*)

// setter triggers!
admin.fullName = "Alice Cooper"; // (**)

admin.fullName; // Alice Cooper, state of admin modified
user.fullName; // John Smith, state of user protected
```

- Line `(*)` has a getter in the prototype so it is called
- Line `(**)` has a setter in the prototype so it is called

### Value of `"this"`

- `this` is not affected by prototypes
  - No matter where the method is found (ie. object or its prototype), `this` is always the object before the dot
  - This means that the setter call `admin.fullName` uses `admin` as `this`, not `user`
- Important because if objects have many methods, and have objects that inherit from it, when inheriting objects run the inherited methods, they will **only modify their own states** not the state of the larger object

```js
// animal has methods
let animal = {
  walk() {
    if (!this.isSleeping) {
      alert(`I walk`);
    }
  },
  sleep() {
    this.isSleeping = true;
  },
};

let rabbit = {
  name: "White Rabbit",
  __proto__: animal,
};

// modifies rabbit.isSleeping
rabbit.sleep();

alert(rabbit.isSleeping); // true
alert(animal.isSleeping); // undefined (no such property in the prototype)
```

- If there were multiple objects inheriting from a single prototype, they would gain the methods from the prototype but each `this` method call would be the corresponding object, evaluated at call-time (before dot), not the prototype
  - Thus, when data is written in `this`, it is stored into those objects
  - As a result, _methods_ are shared, _objects_ are not

### `for...in` loop

- Will loop over _inherited_ properties too
- If that is not wanted, it can be excluded through using `obj.hasOwnProperty(key)` and it will return `true` if `obj` has its own (non-inherited) property named `key`
  - Lets you filter out inherited properties (or do something else with them)
  - Comes from the `Object.prototype.hasOwnProperty` meaning it is inherited
  - However, it is **not** present in a `for...in` loop because it is not enumerable and `for...in` only lists enumerable properties
    - This is why it and the rest of the `Object.prototype` properties are not listed

> Almost all other key/value-getting methods ignore inherited properties
>
> This means `Object.keys`, `Object.values` and so on also ignore inherited properties. They only operate on the **object itself**. Properties taken from the prototype are _not_ taken into account

https://javascript.info/function-prototype


Resources:

- https://javascript.info/prototype-inheritance
