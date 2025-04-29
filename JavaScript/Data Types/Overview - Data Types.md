- Refers to the type of data a JavaScript variable can hold. There are 7 primitive data types in JavaScript:
  - Number
  - BigInt
  - String
  - Boolean
  - Null
  - Undefined
  - Symbol
- Objects are considered non-primitives

## Numbers

- Represent both integers and floating point numbers
- Can store larger integers up to 1.7976931348623157 \* 10<sup>308</sup>, but outside of the safe integer range, +/- 2<sup>53</sup>-1, there will be a precision error
  - Not all digits fit into fixed 64-bit storage, therefore an “approximate” value may be stored
  - All odd integers greater than 2<sup>53</sup>-1 cannot be stored within this type (must use [BigInt](#bigint) type)
- Many operations possible:
  - Multiplication (`*`)
  - Division (`/`)
  - Addition (`+`)
  - Subtraction (`-`)
  - etc.
- Special numeric numbers are also included within this data type:
  - `Infinity`: represents mathematical infinity (∞)
    - Value is greater than any number
  - `-Infinity`
  - `NaN`: represents computational error
    - Any further mathematical operation on `NaN` returns `NaN`

## BigInt

- Rarely needed
- The “number” cannot safetly represent integer values larger than (2<sup>53</sup>-1) (that’s 9007199254740991), or less than -(2<sup>53</sup>-1) for negatives
- While the +/2<sup>53</sup>-1 is enough in most cases, for things like cryptography or microsecond-precision timestamps, `BigInt` is needed
- Created by appending `n` to the end of an integer:

```js
// the "n" at the end means it's a BigInt
const bigInt = 1234567890123456789012345678901234567890n;
```

## String

- Hold data that can be represented in text form
- Must be surrounded in one of the 3 types of quotes:
  - Double quotes: `"Hello"`
  - Single quotes: `'Hello'`
  - Backticks: `` `Hello` ``

```js
let str = "Hello";
let str2 = "Single quotes are ok too";
let phrase = `can embed another ${str}`;
```

- Double and single quotes are “simple quotes”, meaning JS does not recognize a difference between them
- Backticks are “extended functionality” quotes
  - Allow variables and expresses to be embedded into a string by wrapping them in `${...}`
  - The expression within `${...}` is evaluated and result becomes part of the string
    - Anything from a variable like `name` to an arithmetic expression like `1+1` or something more complex can be used

```js
let name = "John";

// embed a variable
alert(`Hello, ${name}!`); // Hello, John!

// embed an expression
alert(`the result is ${1 + 2}`); // the result is 3
```

## Boolean

- Only two values: `true` and `false`
- Commonly used to store yes/no values
  - `True` for “yes”
  - `False` for “no”

## Null

- Special value that represents “nothing”, “empty”, or “value unknown”
- Used to assign an “empty” or “unknown” value to a variable

## Undefined

- Special value to represent when a value is not assigned
- If a variable is declared, but not assigned, `undefined` will show
- Reserved as a default initial value for unassigned things

```javascript
let age = 100;

// change the value to undefined
age = undefined;

alert(age); // "undefined"
```

## Symbol

- Used to create unique identifiers for objects
-

Resources:

- https://javascript.info/types
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
-
