- A variable is named storage for data
- There are two limitations on variable naming in JS
  - Name must contain _only_ letters, digits, or the symbols `$` and `_`
  - First character must not be a digit
- camelCase is commonly used when a name contains multiple words
- Case is important - the variables `apple`, `Apple`, and `APPLE` are all different.
- JS is dynamically typed meaning that you do **not** need to specify the data type a variable will contain

### Reserved names

- There is a list of reserved words that cannot be used as variable names since they are used for the language itself.
- These include:
  - `let`
  - `class`
  - `return`
  - `function`
  - and [more](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords)

## Declaring a variable

- To declare a variable, you have to type the keyword followed by the name you wish for your variable to be called:

```js
let myName
const myBirthday
var myAge
```

### `let`

- declares re-assignable, block-scoped local variables, optionally initializing each to a value

```js
let myName = "Beatrice";

myName = "Sarah";
```

### `var`

- `var` may be something encountered with older scripts
- It is almost the same as `let`, but declares a variable in a different way
  - Most times `var` can be replaced by `let` or vice-versa
- `var` has no **block scope**
  - Are function-scoped or global-scoped
- It _can_ be redeclared, however if `var` is used with an _already-declared_ variable, it will be **ignored**

```js
var user = "Pete";

var user = "John";

alert(user); // John
```

- Can be declared _below_ their use and

```js
function sayHi() {
  phrase = "Hello";

  alert(phrase);

  var phrase;
}

sayHi();
```

- Since `var` ignores code blocks, this will also work

```js
function sayHi() {
  phrase = "Hello"; // (*)

  if (false) {
    var phrase;
  }

  alert(phrase);
}
sayHi();
```

- This is called hoisting and while declarations are hoisted, **assignments are not**
  - This means that the declaration is processed at the start of the function execution (hoisted), but the assignment always works at the place where it appears therefore:

```js {2,4,6}
function sayHi() {
  var phrase; // declaration works at the start...

  alert(phrase); // undefined

  phrase = "Hello"; // ...assignment - when the execution reaches it.
}

sayHi();
```

### `const`

- To declare an constant, or unchanging, variable `const` is used
  - These _cannot_ be reassigned
- Constants can be used as aliases for hard-to-remember values that are known before execution
  - These are named using capital letters and underscores (`const COLOR_RED = "#F00"`)

```js
const birthYear = 1994

birthYear = 1995 ❌ // will cause an error
```

- Use `const` when you can and only use `let` when you have to
  - This means that if you can initialize a variable when you declare it and it will not be reassigned, make it a constant
- Block-scoped

## Summary

- `let` is a modern variable declaration
- `var` is old-school variable declaration.
  - Not currently used
- `const` is used when a variable cannot be changed

Resources:

- https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/Variables
- https://javascript.info/variables
