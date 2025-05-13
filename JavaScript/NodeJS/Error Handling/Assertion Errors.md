- `AssertionError` is thrown when the `assert` module determines that a given expression is not truthy
- `assert` module is built-in nodeJS module that provides a simple set of assertion tests that can be used to test the behaviour of your code

## Class: `assert.assertionError`

- Indicates the failure of an assertion
- All errors thrown by the `node:assert` module will be instances of the `AssertionError` class

#### `new assert.AssertionError(options)`

- `options` `<Object>`
    - `message` `<string>` If provided, the error message is set to this value.
    - `actual` `<any>` The `actual` property on the error instance.
    - `expected` `<any>` The `expected` property on the error instance.
    - `operator` `<string>` The `operator` property on the error instance.
    - `stackStartFn` `<Function>` If provided, the generated stack trace omits frames before this function.

A subclass of `<Error>` that indicates the failure of an assertion.

All instances contain the built-in Error properties (message and name) and:

- `real` `<any>` Set to the `actual` argument for methods such as `assert.strictEqual()`.
- `expected` `<any>` Set to the `expected` value for methods such as `assert.strictEqual()`.
- `generatedMessage` `<boolean>` Indicates if the message was auto-generated (`true`) or not.
- `code` `<string>` Value is always `ERR_ASSERTION` to show that the error is an assertion error.
- `operator` `<string>` Set to the passed in operator value.