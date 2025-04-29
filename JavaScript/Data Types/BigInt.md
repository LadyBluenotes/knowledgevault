- BigInt value represents integer values that are too high or low to be represented by the `number` primitive
- Created by appending `n` to the end of an integer literal, or by calling the `BigInt()` function and giving it an integer or string value
- Cannot be used in methods in the built-in `Math` object and cannot be mixed with a Number value in operations
  - Must be coerced to the same type

```js
const previouslyMaxSafeInteger = 9007199254740991n;

const alsoHuge = BigInt(9007199254740991);
// 9007199254740991n

const hugeString = BigInt("9007199254740991");
// 9007199254740991n

const hugeHex = BigInt("0x1fffffffffffff");
// 9007199254740991n

const hugeOctal = BigInt("0o377777777777777777");
// 9007199254740991n

const hugeBin = BigInt(
  "0b11111111111111111111111111111111111111111111111111111",
);
// 9007199254740991n
```

## Operators

- Most operators support BigInts, however they do not permit operands to be of mixed types. Both operands must be BigInt or neither:
  - Arithmetic operators: `+`, `-`, `*`, `/`, `%`, `**`
  - Bitwise operators: `>>`, `<<`, `&`, `|`, `^`, `~`
  - Unary negation (`-`)
  - Increment/decrement: `++`, `--`
- Boolean-returning operators allow mixing numbers and BigInts as operands:
  - Relational operators and equality operators: `>`, `<`, `>=`, `<=`, \==, `!=`, `===`, `!==`
  - Logical operators only rely on the truthiness of operands
- A couple operators do not support BigInt at all:
  - Urary plus (`+`)
  - Unsigned right shift (`>>>`)
- Special cases:
  - Addition (`+`) involving a string and a BigInt returns a string.
  - Division (`/`) truncates fractional components towards zero, since BigInt is unable to represent fractional quantities.

## Comparisons

- BigInt is not strictly equal to a Number value, but it is _loosely_ so:

```js
0n === 0; // false
0n == 0; // true
```

- A Number value and a BigInt value may be compared as usual:

```js
1n < 2; // true
2n > 1; // true
2 > 2; // false
2n > 2; // false
2n >= 2; // true
```

BigInt values and Number values may be mixed in arrays and sorted:

```js
const mixed = [4n, 6, -12n, 10, 4, 0, 0n];
// [4n, 6, -12n, 10, 4, 0, 0n]

mixed.sort(); // default sorting behavior
// [ -12n, 0, 0n, 10, 4n, 4, 6 ]

mixed.sort((a, b) => a - b);
// won't work since subtraction will not work with mixed types
// TypeError: can't convert BigInt value to Number value

// sort with an appropriate numeric comparator
mixed.sort((a, b) => (a < b ? -1 : a > b ? 1 : 0));
// [ -12n, 0, 0n, 4n, 4, 6, 10 ]
```

## Conditionals

- BigInt value follows the same conversion rules as Numbers when:
  - converted to a `Boolean` via the `Boolean` function
  - when used with logical operators `||`, `&&`, `!`; or
  - within a conditional test like an `if` statement
- Only `On` is falsy; everything else is truthy
