> JS does not have the distinction of “floating point numbers” and “integers” at a language level.
>
> [[parseFloat()]] and `parseInt()` only differ in their parsing behaviour, but not necessarily their return values

- converts its first argument to a string, parses it, then returns an integer or `NaN`
- If not `NaN`, value returned will be integer that is first taken as a number in specified `radix`
  - 10 converts from a decimal number
  - `8` converts from an octal
  - `16` from a hexadecimal
- JavaScript assumes the following:
  - If input `string` with leading whitespace and possible `+`/`-`, signs removed, begins with `0x` or `0X`, `radix` is assumed to be `16`
- Only understands `+` and `-`
- First character cannot be converted to a number with the `radix` in use - will return `NaN`
- `NaN` is not a number at any radix

```js
parseInt(string);
parseInt(string, radix);
```

`string`- string starting with an integer

- leading whitespace is ignored
  `radix` - integer between `2` and `36` that represent the radix of the `string`
- converted to a number and if not provided, value becomes `0`, `Infinity`, or `-Infinity` (`undefined` is coerced to `NaN)
- converted to 32-bit integer
- if nonzero and outside the range \[2,36] after conversion, will always return `NaN`
- If `0` or not provided, radix will be inferred based on `string`’s value
- If input `string` with leading whitespace and possible `+`/`-`, signs removed, begins with `0x` or `0X`, `radix` is assumed to be `16` and the rest is parsed as a hexadecimal number
- if input `string` begins with any other value, radix is `10` (decimal)
- number literals (such as`0b`) are treated as normal digits
- if `16`, allows string to be optionally prefixed by `0x` or `0X` after optional sign character
  - `A` through `F` can be used and letters are case-_insensitive_
- if > `10`, letters of the English alphabet indicate numbers greater than `9`

Return is an integer parsed from the given `string` or `NaN` when:

- radix as 32-bit integer is smaller than `2` or bigger than `36`
- First non-leading whitespace character cannot be converted to a number
