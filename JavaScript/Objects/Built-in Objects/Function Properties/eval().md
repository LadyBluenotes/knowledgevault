> Executing JS from a string is a _enormous_ security risk. It is too easy for a bad actor to run arbitrary code when you use `eval()`

- A function that evaluates JS code represented as a string and returns a completion value
  - Parsed as a **script**
- Argument is a string
	- Will evaluate source string as a script body, which means both statements and expressions are allowed
		- Expressions - value the expression evaluates to is returned
- In strict mode, declaring a variable named `eval` or re-assigning `eval` is a `SyntaxError`

```js
eval(script);
```

- **`script`** - a string that represents a JS expression, statement, or sequence of statements
	- Can include variables and properties of existing objects
	- Will be parsed as a script so `import` declarations cannot be used (they only exist in modules)

- Return value is the completion value of evaluating the code 
	- If empty, `undefined` is returned
	- If `script` is not a primitive, `eval()` returns the argument *unchanged*

- Throws any exception that occurs during the evaluation of the code, including `SyntaxError`, if `script` fails to be parsed as a script

## Two modes

### Direct eval
- Refers to directly calling the global `eval` with `eval(...)`
- inherits strictness from invoking context
- if in a strict mode context or if the source string is in strict mode, `var` and function declarations do not “leak” into surrounding scope

 ***Never use*** because:
 - `eval()` executes code passed with the privileges of the caller
	 - Can be affected by a malicious party and you may end up running malicious code on the user’s machine with the permissions of your webpage/extension
	 - Third-party code accessing the scope in which `eval()` is invoked can lead to possible attacks that read or change local variables
- slower than alternatives 
	- has to invoke JS interpreter
- Modern interpreters convert JS to machine code
	- any use of `eval()` will force the browser to do long, expensive variable name lookups to figure out where the variable exists in the machine code and set its value
	- new things can be introduced to that variable through `eval()`, such as changing the type of the variable, forcing the browser to re-evaluate all of the generated machine code to compensate
- Minifiers give up on minification if scope is depended on `eval()`

### Indirect eval
- When invoking it via an aliased variable
	- Via a member access or other expression or through optional chaining (`?.`) operator
- seen as if code is evaluated within a separate `script` tag
	- means that:
		- works in global scope rather than local
			- code being evaluated doesn’t have access to local variables within scope it’s being called
		- does not inherit strictness of the surrounding context, is only in strict mode if source string itself has `"use strict"` directive
		- `var`-declared variables and function declarations would go into surrounding scope if source string is not interpreted in strict mode and become global variables