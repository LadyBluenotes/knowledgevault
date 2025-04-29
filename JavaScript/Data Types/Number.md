- `Number` **data type** represents floating point numbers (eg. 37 or -9.25)
- `Number` **constructor** provides constants and methods to work with numbers and values of other types can be converted to numbers using the `Number()` function

```js
let num1 = 255; // integer
let num2 = 255.0; // floating-point number with no fractional part
let num3 = 0xff; // hexadecimal notation
let num4 = 0b11111111; // binary notation
let num5 = 0.255e3; // exponential notation

console.log(num1 === num2); // true
console.log(num1 === num3); // true
console.log(num1 === num4); // true
console.log(num1 === num5); // true
```

- Two types of numbers:
  - Regular numbers stored in 64-bit format IEEE-754 (aka “double precision floating point numbers”)
    - What is used most of the time
  - BigInt which represent integers of an arbitrary length
    - Sometimes needed since a regular number cannot safely exceed (2<sup>53</sup>-1) or be less than -(2<sup>53</sup>-1)

## How to write numbers

- Underscores can be used
  - Play the role of syntactic sugar

```javascript
let billion = 1000000000;

let billion = 1_000_000_000;
```

- Can shorten numbers by appending the letter `"e"` to it and specifying the zero count
  - For very small numbers, you just need to write a negative number after `"e"`

```js
let billion = 1e9; // 1 billion, literally: 1 and 9 zeroes

7.3e9; // 7.3 billions (same as 73000000000 or 7_300_000_000)

let mcs = 0.000001;

// or

let mcs = 1e-6; // 6 zeroes

1e-3; // 0.001

1.23e-6; // 0.00000123
```

## Hex, binary, and octal numbers

- Hexadecimal numbers are widely used to represent colors, encode characters, and more
  - Exists a shorter way to write them: `0x` then the number
  - Case _does not matter_

```js
0xff; // 255
0xff; // 255
```

- Binary and octal numeral systems are rarely used, but are supported using the `0b` and `0o` prefixes

```js
let a = 0b11111111; // binary form of 255
let b = 0o377; // octal form of 255

a == b; // true, the same number 255 at both sides
```

## `.toString(base)`

- Returns a string representation of `num` in the numeral system with the given `base`

```js
let num = 255;

num.toString(16); // ff
num.toString(2); // 11111111
```

- Base can vary from `2` to `36` and by default it is `10`
  - Common use cases:
    - **base = 16** used for hex colours, character encodings, etc
      - Digits can be `0...9` & `A...F`
    - **base = 2** used for debugging bitwise operations
      - Digits can be `0` or `1`
    - **base = 36** the maximum
      - Digits can be `0...9` and `A...Z`
      - Used when making a short URL, as an example

> To call a method directly on a number, two dots must be placed after it (`123456..toString(36)`. If using a single dot, there would be an error since JS syntax implies the decimal part after the first dot and the second dot is used to show JS that the decimal part is empty and now uses the method. Can also use brackets (`(123456).toString(36)`).

## Rounding

- Several built-in functions

### `Math.floor`

- Rounds down to the nearest whole numbe

```js
3.1 -> 3
-1.1 -> -2
```

### `Math.ceil

- Rounds up to the nearest whole number

```js
3.1 -> 4
-1.1 -> 1
```

### `Math.round`

- Rounds to the nearest integer

```js
3.1 -> 3
3.5 -> 4
3.5 -> 4 // middle cases round up
-3.5 -> 3
```

### `Math.trunc`

- Not supported by internet explorer
- Removes anything after the decimal point without rounding

```js
3.1 -> 3
-1.1 -> -1
```

### `.toFixed(n)`

- Rounds numbers to `n` digits after the point and returns a **string** representation of the result
- If the decimal part is shorter than required, zeroes are appended to the end

```js
let num = 12.34;

num.toFixed(1); // "12.3"
num.toFixed(5); // "12.34000"
```

## Imprecise calculations

- Internally, numbers are represented by 64-bit format IEEE-754 so there are exactly 64 bits to store a number, 52 of them used to store it and 11 to store the decimal point and 1 bit for the sign
- A really large number may overflow and become the special numeric value `Infinity`

```js
1e500; // Infinity
```

> `0` and `-0` exist due to the internal representation of numbers and signs being represented by a single bit, so it can be set or not set for any number, including 0.

### `isNaN`

- Returns `true` if the argument belongs to the type `number` and it is `NaN`
  - Any other case is false

```js
Number.isNaN(NaN); // true
Number.isNaN("str" / 2); // true

Number.isNaN("str"); // false, "str" belongs to the string type
isNaN("str"); // true, isNaN converts "str" into a number and gets NaN
```

### `isFinite`

- Returns `true` if argument belongs to the `number` type and it is not `NaN/Infinity/-Infinity`
  - Any other case is false

```js
Number.isFinite(123) ); // true
Number.isFinite(Infinity) ); // false
Number.isFinite(2 / 0) ); // false

Number.isFinite("123") // false,"123" belongs to the string type
isFinite("123") // true, isFinite converts string "123" into a number
```

## `parseInt` and `parseFloat`

- “Read” a number from a string until they can’t
  - In case of an error, gathered number is returned
- Return `NaN` when no digits can be read

### `parseInt(str, radix)`

- Returns an integer
- `radix` specifies the base of the numeral system, so hex and binary numbers can be parsed

```js
parseInt("100px"); // 100
parseInt("12.3"); // 12.3
parseInt("a123"); // NaN

parseInt("0xFF", 16); // 255
parseInt("ff", 16); // 255, without the 0x works
parseInt("2n9c", 36); // 123456
```

### `parseFloat`

- Returns a floating-point number

```js
parseFloat("12.5em"); // 12.5
parseFloat("12.3.4"); // 12.3
parseFloat("a123"); // NaN
```

## Other math functions

- More math functions can be found: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math

### `Math.random`

- Returns a random number from 0 to 1 (not including 1)

```javascript
Math.random(); // 0.1234567894322
Math.random(); // 0.5435252343232
Math.random(); // ... (any random numbers)
```

### `Math.max(a,b,c,...)`

- Returns the greatest from the arbitrary number of arguments

```js
Math.max(3, 5, -10, 0, 1); // 5
```

### `Math.min(a,b,c,...)`

- Returns the smallest from the arbitrary number of arguments

```js
Math.min(1, 2); // 1
```

### `Math.pow(n, power)`

- Returns `n` raised to the given power `power`

```js
Math.pow(2, 10); // 2 in power 10 = 1024
```
