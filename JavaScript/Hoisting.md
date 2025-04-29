- The process whereby the interpreter appears to move the declaration of functions, variables, classes, or imports to the top of their scope prior to the execution of the code
- Any of the following behaviours may be regarded as type-1 hoisting behaviour:
  - Being able to use a variable’s value in its scope before the line it is declared (“Value hoisting”)
  - Being able to reference a variable in its scope before the line it is declared. without throwing a `ReferenceError`, but the value is always `undefined` (“Declaration hoisting)
  - The declaration of the variable causes behaviour changes in its scope before the line in which it is declared
  - The side effects of a declaration are produced before evaluating the rest of the code that contains it
- Type-2 hoisting behaviour is `var`
- Type-3 hoisting behaviour is `let`, `const`, and `class`
	- Some prefer to see `let`, `const`, and `class` (lexical declarations) as non-hoisting 
		- Due to temporal dead zone which strictly forbids any use of the variable before its declaration
			- Can cause other observable changes in its scope to suggest some form of hoisting
- `import` declarations are hoisted with type 1 and type 4 behaviour

Resources:

- https://developer.mozilla.org/en-US/docs/Glossary/Hoisting
