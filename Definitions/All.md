---
# heap

A tree-based data structure that satisfies the heap property, meaning that a parent node's value is always greater than or equal to its children's value (in a max-heap) or less than or equal to (in a min-heal).

Often used in priority queues and is also the basis for the heapsort algorithm.
---

# stack

A linear data structure that follows LIFO (Last In First Out) Principle, the last element inserted is the first to be popped out.

---

# first-class functions

When functions in a language are treated like any other variable.

For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable.

---

# Prototype-based

Simplified: Allows for the creation of an object without first defining its class.

Style of object-orientated programming in which classes are not explicitly defined, but derived by adding properties and methods to an instance of another class or, less frequently, adding them to an empty object.

---

# single-threaded

Executes only one instruction at a time

---

# dynamic-typed

Interpreter assigns variables a type at runtime based on the variable's value at the time.

---
# camelCase

The practice of writing phrases without spaces or punctuation and with capitalized words. The format indicates the first word starting with either case, then the following words having an initial uppercase letter.

---
# block scope

*block scopes, block-scope, block-scoped*

The area within curly braces `{ }`. 

Variables that are declared within a block scope are only accessible within that specific block of code, not outside of it.

---
# function-scoped

Variables defined inside a function cannot be accessed from anywhere outside the function.

The function scope inherits from all upper scopes. For example, a function defined in the global scope can access all variables in the global scope.

---
# global-scoped

In a programming environment, global scope is the scope that contains, and is visible in, all other scopes. 

This means that globally-scoped variables can be accessed from anywhere in a JavaScript program.

---
# hoisting

*hoistings, hoisted, hoist*

Refers to the process where an interpreter appears to move the declaration of functions, variables, classes, or imports to the top of their scope, prior to the execution of the code.

---
# temporal dead zone

The period between entering a scope and the actual declaration of a variable using let or const. During this period, the variable is in an "uninitialized" state and accessing it will result in a `ReferenceError`.

---
# syntactic sugar

Syntax with a programming language that is designed to make things easier to read or express. This can include things being expressed more clearly, more concisely, or in an alternative style that some may prefer.

Usually shorthand for a common operation that could be expressed in an alternative, more verbose form.

---
# global object

In JavaScript, is an object which represents global scope.

---
# Global functions

*global function*

Functions which are called globally, rather than on an object.

---
# radix

Base in mathematical numeral systems

---
# URI

Unicode Resource Identifier

 A unique sequence of characters that identifies an abstract or physical resource, such as resources on a webpage, mail address, phone number, books, real-world objects such as people and places, concepts

---
# UTF-8

A character encoding standard used for electronic communicate. 

Is a variable-length character encoding (1 to 4 bytes long).

Is backwards compatible with ASCII and the preferred encoding for e-mail and web pages.

---
# lone surrogate

A 16-bit code unit satisfying one of the descriptions below:

- In the range of `0xD800`–`0xDBFF`, inclusive (ie. is a leading surrogate), but it is the last code unit in the string, or the next code unit is not a trailing surrogate.
- It is in the range of `0xDC00`–`0xDFFF`, inclusive (ie. a trailing surrogate), but it is the first code unit in the string, or the previous code unit is not a leading surrogate

Do not represent any Unicode character.

---
# enumerable

Properties whose internal enumerable flag is set to `true`, which is the default for properties created via simple assignment or via a property initializer. 

Properties defined via `Object.defineProperty` and such are not enumerable by default.

Most iteration means only visit enumerable keys (eg. `for..in` and `Object.keys`)

---
# deep cloning

*deep clone*

A copy of an object whose properties do not share the same references (point to the same underlying values) as those of the source object from which the copy was made. As a result, when you change either the source or the copy, you can be assured you're not causing the other object to change too.

---
# JSON

*JavaScript Object Notation*

An open standard file format and data interchange format that uses human-readable text to store and transmit data objects consisting of name–value pairs and arrays. It is a commonly used data format with diverse uses in electronic data interchange, including that of web applications with servers.
