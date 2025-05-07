- aka global objects
  - can be accessed using the `this` operator in the _global scope_
- Global scopes are created by the user script or provided by the host application
- Built into the language specs
  - Including methods and properties

## Value properties

- Return a simple value
- Do not have properties or methods

- [`globalThis`]([[globalThis]])
- [`Infinity`]([[Overview - Data Types#Numbers]])
- [`NaN`]([[Overview - Data Types#Numbers]])
- [`undefined`]([[Undefined]])

## Function properties

- Global functions that directly return their results to the caller

- [`eval()`](<[[eval()]]>)
- [`isFinite()`](<[[isFinite()]]>)
- [`isNaN()`](<[[isNaN()]]>)
- [`parseFloat()`](<[[parseFloat()]]>)
- [`parseInt()`](<[[parseInt()]]>)
- [`decodeURI()`](<[[decodeURI()]]>)
- [`decodeURIComponent()`](<[[decodeURIComponent()]]>)
- [`encodeURI()`](<[[encodeURI()]]>)
- [`encodeURIComponent()`](<[[encodeURIComponent()]]>)

## Fundamental objects

- objects that represent fundamental language constructs

- [[Object]]
- [[Function]]
- [[JavaScript/Objects/Built-in Objects/Boolean|Boolean]]
- [[Symbol]]

## Error objects

- Special type of fundamental object
- Includes basic `Error` type as well as several specialized error types

- [[Error]]
- [[AggregateError]]
- [[EvalError]]
- [[RangeError]]
- [[ReferenceError]]
- [[SyntaxError]]
- [[TypeError]]
- [[URIError]]

## Numbers and dates

- Base objects representing numbers, dates, and mathematical calculations

- [[JavaScript/Objects/Built-in Objects/Number|Number]]
- [[BigInt]]
- [[Date]]
- [[Math]]
- [[Temporal]]

## Text processing

- Represent strings and support manipulating them

- [[String]]
- [[RegExp]]

## Indexed collections

- Represent collections of data which are ordered by index value
- Includes (typed) arrays and array-like constructs

- [[Arrays]]
- [[TypedArray]]
- [[Int8Array]]
- [[Uint8Clampedarray]]
- [[Int16Array]]
- [[Uint16Array]]
- [[Int32Array]]
- [[Uint32Array]]
- [[BigInt64Array]]
- [[BigUint64Array]]
- [[Float16Array]]
- [[Float32Array]]
- [[Float64Array]]

## Keyed collections

- Objects represent collections which use keys
- Iterable collections (Map and Set) contain elements which are easily iterated in the order of insertion

- [[Map]]
- [[Set]]
- [[WeakMap]]
- [[WeakSet]]

## Structured data

- Represent and interact with structured data buffers and data coded using JSON

- [[ArrayBuffer]]
- [[SharedArrayBuffer]]
- [[DataView]]
- [[Atomics]]
- [[JSON]]

## Managing memory

- Interact with the garbage collection mechanism

- [[WeakRef]]
- [[FinalizationRegistry]]

## Control abstraction objects

- Help structure code, especially async code

- [[Iterator]]
- [[AsyncIterator]]
- [[Promise]]
- [[GeneratorFunction]]
- [[AsyncGeneratorFunction]]
- [[Generator]]
- [[AsyncGenerator]]
- [[AsyncFunction]]

## Reflection

- [[Reflect]]
- [[Proxy]]

## Internationalization

- Additions to ECMAScript core for language-sensitive functionalities

- [[Intl]]
- [[Intl.Collator]]
- [[Intl.DateTimeFormat]]
- [[Intl.DisplayNames]]
- [[Intl.DurationFormat]]
- [[Intl.ListFormat]]
- [[Intl.Locale]]
- [[Intl.NumberFormat]]
- [[Intl.PluralRules]]
- [[Intl.RelativeTimeFormat]]
- [[Intl.Segmenter]]
