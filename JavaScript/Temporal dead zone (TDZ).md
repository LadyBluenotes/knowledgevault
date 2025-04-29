- Variable declared with `let`, `const`, or `class` is said to be in a TDZ from the start of the block until code execution reaches the place where the variable is declared and initialized
- The TDZ is a period between entering a scope and the actual declaration of a variable using `let` or `const`. During this period, the variable is in an "uninitialized" state and accessing it will result in a `ReferenceError`.
- Variable is initialized when execution reaches place in code where it was declared

  - If no initial value is specified with variable declaration, initialized with a value of `undefined`

- Term `temporal` is used because the zone depends on order of execution vs order in which code is written

Resources:

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz
