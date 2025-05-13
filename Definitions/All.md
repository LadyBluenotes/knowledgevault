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

---
# module graph

A directed graph where each node represents a JavaScript module (file), and each edge represents an import or dependency between modules.

Components:
- **Nodes**: individual JS modules or files
- **Edges**: import/export relationships (`import`/`require` statements)
- **Root Node**: Usually the application's entry point (eg. `index.html`, `index.js`
- **Leaf Nodes**: Modules that do _not_ import any others

---
# factory function

A function that returns an object. 

A way of creating and returning objects in a more controlled and customized manner. Form a design patter that enables the creation of objects with specific properties and behaviours.

---
# side-effects

Occurs when a function or expression modifies some state outside its local scope or interacts with the external world in addition to returning a value.

Happen with impure functions when they may depend on external state, produce different outputs for the same input, modifies external state (I/O, globals, etc.), and can be harder to reason about due to hidden dependencies.

---
# array destructuring

Syntax that allows you to unpack values from an array into distinct variables.

```js

const [a,b] = [1,2] // a = 1, b = 2

```

---
# callback functions

*callback function*

Function passed as an argument to another function, executed later.

---
#  I/O

Input/Output

The communication between a computer program and the external world, typically involving the transfer of data into (input) and out of (output) a system.

Input refers to data received by the program (e.g., from a user, file, or device), while output refers to data sent from the program (e.g., to a display, file, or another system). I/O is fundamental to program interaction and system functionality.

---
# symlinks

Type of file in a filesystem that points to another file or directory. Acts as a shortcut or reference to another location in the filesystem, rather than holding the actual data itself.

Used for creating shortcuts, organizing files, and simplifying complex directory structures

Can be used to make packages, files, or directories accessible from different locations in the filesystem without duplicating the data.

Allow for flexible dependency management in software systems, as in the case of Node.js resolving module dependencies.

Two main types:
1. **Soft (symbolic link):** Points to a file or directory by name and path. If target file or directory is moved or deleted, symlink becomes broken (ie. no longer points to a valid location
2. **Hard:** Points directly to data blocks on the disk. More like an alias for original file and remains valid even if original file is renamed or moved (though not across different filesystems)

---
# semver rule

*semantic versioning*

Used to keep the JS ecosystem healthy, reliable, and secure.

When there are significant updates to an npm package, it is recommended to publish a new version of the package with an updated version number in the `package.json` file that follows the semantic versioning spec. Following this, helps other developers who depend on your code understand the extent of the changes in a given version, and adjust their own code if necessary.

If there is a change that breaks a package dependency, it is strongly recommended incrementing the version **major number**.
