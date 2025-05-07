---
title: isFinite()
date created: Thursday, April 24th 2025, 12:04:23 pm
date modified: Tuesday, May 6th 2025, 11:50:05 am
---

# isFinite()

> `Number.isFinite()` is more reliable to test whether a value is finite, because it returns `false` for any **non-number** input

- function that determines whether a value is finite
- value is coerced to a number and is compared against `NaN` and +/- Infinity

```js
isFinite(value);
```

`value` - to be tested

- returns `false` if given `NaN`, `Infinity`, or `-Infinity` after being converted to a number
  - otherwise `true`

```js
isFinite(Infinity); // false
isFinite(NaN); // false
isFinite(-Infinity); // false

isFinite(0); // true
isFinite(2e64); // true
isFinite(910); // true
```
