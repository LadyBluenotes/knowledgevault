- Used by JavaScript to inform developers about various issues in the script being executed
- Issues can be syntax error where the wrong syntax was used or due to a wrong input, etc

- Six types of errors that may occur during execution of a script:

| Error           | Description                                                               |
| --------------- | ------------------------------------------------------------------------- |
| EvalError       | Represents an error related to the `eval()` function (rarely used today). |
| RangeError      | Indicates a value that is out of an allowable range.                      |
| ReferenceError  | Occurs when referencing a variable that hasn't been declared.             |
| SyntaxError     | Thrown when code contains invalid syntax and can't be parsed.             |
| TypeError       | Indicates that a value is not of the expected type.                       |
| URIError        | Thrown when malformed parameters are passed to URI-handling functions.    |
| AggregateError  | Represents multiple errors wrapped together, often from `Promise.any()`.  |
| InternalError\* | Represents an error internal to the JavaScript engine (non-standard).     |
