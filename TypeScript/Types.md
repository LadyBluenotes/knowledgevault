---
title: Types
date created: Tuesday, April 22nd 2025, 11:06:54 am
date modified: Tuesday, April 22nd 2025, 11:28:48 am
---

# Types

- **Inferred type:** the ability of a compiler or interpreter to automatically determine the type based on usage and context _without_ explicit type annotations
- Accept a small set of primitive types available in JS: `boolean`, `bigint`, `null`, `number`, `string`, `symbol`, and `undefined` (can be used in interfaces)
  - TS adds:
    - `any` - allows anything
    - `unknown` - ensure someone using this declares what the type is
    - `never` - not possible that this type could happen
    - `void` - function which returns `undefined` or has no return value
- **`typeof`**: creates a type that represents the type of a value or an expression; Often used with variables or values to capture their type

```ts
typeof "string"; // returns "string"
```

- **`keyof`**: used to get the names of all properties (keys) in an object type

```ts
type Person = {
  name: string;
  age: number;
  address: string;
};

type PersonKeys = keyof Person;
// PersonKeys is now "name" | "age" | "address"
```

- Type checking focuses on the _shape_ that the values have
  - Eg. if two objects have the same shape or same set of properties with compatible types, they are considered to have the same type even if not explicitly stated

## Type alias

- Similar to variables - used to provide names to type literals
- Defines the shape of the data

```ts
type User = {
  id: number;
  name: string;
  email: string;
};
```

## Interface

- _Preferred_ way of typing - provides better error messages
- Explicitly describes an object's shape

```ts
interface User {
  name: string;
  id: number;
}
```

- This will then declare that a JS object conforms to the shape of the interface by using `: TypeName` syntax after the variable declaration:

```ts
const user: User = {
  name: "Hayes",
  id: 0,
};
```

- Are _opened_ and can therefore be _extended_
  - Allows you to inherit the types of the interface that's been extended

```ts
interface Admin extends User {
  admin: boolean;
}

// equivalent to

interface Admin {
  name: string;
  id: number;
  admin: boolean;
}
```

## Class

- So you can express relationships between classes and other types

```ts
class UserAccount {
  name: string;
  id: number;
  constructor(name: string, id: number) {
    this.name = name;
    this.id = id;
  }
}

const user: User = new UserAccount("Murphy", 1);
```

# Composing types

- Can create complex types by combining simple ones

## Unions

- Describe values that can be one of several types and create unions of various primitive, literal or complex types:

```ts
type MyBool = true | false;
type WindowStates = "open" | "closed" | "minimized";
type LockStates = "locked" | "unlocked";
type PositiveOddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;
```

- Can also be used as a way to handle different types:

```ts
function getLength(obj: string | string[]) {
  return obj.length;
}
```

## Generics

- Allows you to pass in various types of data and create reusable code to handle different inputs
- Provide the ability to define placeholder types which are replaced when the code is executed with the actual types passed in

```ts
// We define a generic value called T with <T>
function getFirstElement<T>(arr: T[]): T {
  return arr[0];
}

const numberArray: number[] = [1, 2, 3, 4, 5];
const stringArray: string[] = ["apple", "banana", "orange"];

// Note the generic values being passed in <number> & <string>
const firstNumber = getFirstElement<number>(numberArray);
const firstString = getFirstElement<string>(stringArray);
```

- Provides _type safety_ and _error detection_
- Improves code _reusability_ and _flexibility_
- Can also be used with interfaces, types, and classes to define custom types

```ts
interface Person<T> {
  id: number;
  name: string;
  age: number;
  metadata: T;
}

type Person<T> = {
  id: number;
  name: string;
  age: number;
  metadata: T;
};
```

- Multiple generics can be used:

```ts
function mergeArrays<T, K>(arr1: T[], arr2: K[]): (T | K)[] {
  return [...arr1, ...arr2];
}
```
