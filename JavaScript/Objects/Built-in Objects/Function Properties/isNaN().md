> `Number.isNaN()` is a more reliable way to test whether a value is the number value `NaN` or not.

- Function to determine whether a value is `NaN`
  - Answers the question “is the input functionally equivalent to `NaN` when used in a number context”
    - If `false`, can use to make an arithmetic expression as if it’s a valid number
- Value is first coerced to a number and then compared against `NaN`
- Non-numeric arguments can create confusion:
  - Empty strings are coerced to `0`
  - Boolean is coerced to `0` or `1`

```js
isNaN(value);
```

`value` - value to be tested

Returns `true` if `NaN` after being converted to a number, otherwise `false`
