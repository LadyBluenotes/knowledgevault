- Simple data type that can hold one of two values: `true` or `false`
- Represent logical states and are essential in controlling the flow of a program
  - Commonly used in conditional statements (`if`, `else`, `while`, etc.) to determine whether a block of code should execute
- Produced by relational operators, equality operators, and logical NOT (`!`)
  - Can also be produced by functions that represent conditions (eg. `Array.isArray()`)
- JavaScript automatically converts something to a boolean context
  - Typically do not need to convert something to a boolean value

## Boolean primitives & Boolean objects

- To convert non-boolean to boolean, use `Boolean` as a function or use the double NOT operator

```js
Boolean(expression);
!!expression;
```
