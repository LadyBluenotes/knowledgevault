- converts its first argument to a string, parses that string as a decimal number literal, then returns a `number` or `NaN`
- does not support non-decimal literals with `0x`, `0b`, `0o`
  - Is more lenient with than `Number()` because it ignores trailing characters that would cause `Number()` to return `NaN`
- May not return number exactly equal to number represented by the string, due to floating point range and inaccuracy

  - For numbers outside the `-1.7976931348623158e+308` – `1.7976931348623158e+308` range, `-Infinity` or `Infinity` is returned

- Number syntax it accepts:
  - characters accepted are plus sign (`+`), minus sign (`-` U+002D HYPHEN-MINUS), decimal digits (`0` – `9`), decimal point (`.`), exponent indicator (`e` or `E`), and the `"Infinity"` literal.
    - `+`/`-` signs can only appear strictly at the beginning of the string or immediately `e`/`E` character
    - decimal point can only appear once, and only before the `e`/`E` character
    - `e`/`E` character can only appear once, and only if there is at least one digit before it
  - Leading spaces in the argument are trimmed and ignored
  - `Infinity` or `-Infinity` if the string starts with `"Infinity"` or `"-Infinity"` preceded by none or more white spaces
  - picks the longest substring starting from the beginning that generates a valid number literal
    - if an invalid character is encountered. returns number represented up to that point, ignoring invalid character and everything following it
  - returns `NaN` if the arguments first character cannot start a legal number literal based on syntax above

```js
parseFloat(string);
```

`string` - value to parse, coerced to a string.

- Leading whitespace is ignored

Returns a floating point number parsed from the given `string` or `NaN` when the first non-whitespace character cannot be converted to a number
