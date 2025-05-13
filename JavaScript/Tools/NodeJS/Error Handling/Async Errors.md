- Asynchronous syntax and patterns are focused on callback’s, Promise abstractions and the `async/await` syntax
- There are three ways to handle errors in async:
  - Rejection
  - Try/Catch
  - Propagation

## Rejection

- Errors are often represented by **Promise rejections**
- Promises are said to be rejected when an operation fails
  - Either explicitly using `reject(reason)` or by throwing an error _inside_ the async function

```js
const fail = () => Promise.reject(new Error("Something went wrong"));
```

- Throwing an error has the same effect in `async` functions

```js
async function fail() {
  throw new Error("Something went wrong");
}
```

## Propagation

- Errors in promises or async functions **propogate** through `.then()` and `.catch()` or through `await`
- If an error isn’t caught, it bubbles up the call chain until it is handled or causes an unhandled rejection

```js
async function outer() {
  await inner(); // if inner throws, outer also rejects
}

async function inner() {
  throw new Error("Oops");
}
```

- `.catch()` or `try/catch` blocks can stop propagation

## Try/Catch

> Only works for awaited calls. If `await` is forgotten, errors will not be caught

- Inside `async` functions, `try/catch` blocks can be used to handle errors from `await`

```js
async function fetchData() {
  try {
    const res = await fetch('/data');
    const data = await res.json();
    return data;
  } catch (err) {
    console.error("Fetch failed:", err);
  }
}
```
