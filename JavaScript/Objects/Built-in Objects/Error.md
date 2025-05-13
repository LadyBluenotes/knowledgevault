| Name            | Description                                                                     |
| --------------- | ------------------------------------------------------------------------------- |
| Error           | The base constructor for all error types. Used to create generic error objects. |
| EvalError       | Represents an error related to the `eval()` function (rarely used today).       |
| RangeError      | Indicates a value that is out of an allowable range.                            |
| ReferenceError  | Occurs when referencing a variable that hasn't been declared.                   |
| SyntaxError     | Thrown when code contains invalid syntax and can't be parsed.                   |
| TypeError       | Indicates that a value is not of the expected type.                             |
| URIError        | Thrown when malformed parameters are passed to URI-handling functions.          |
| AggregateError  | Represents multiple errors wrapped together, often from `Promise.any()`.        |
| InternalError\* | Represents an error internal to the JavaScript engine (non-standard).           |

\*Non-standard: `InternalError` is specific to some engines like Firefox and may not be supported in all environments.

## Properties

| Property                                                          | Description                                 |
| ----------------------------------------------------------------- | ------------------------------------------- |
| [name](https://www.w3schools.com/jsref/prop_error_name.asp)       | Sets or returns an error name               |
| [message](https://www.w3schools.com/jsref/prop_error_message.asp) | Sets or returns an error message (a string) |
