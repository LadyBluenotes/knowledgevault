- Used to trace the active stack frames at a particular instance during the execution of a program
- Useful while debugging code as it shows the _exact_ point that has caused an error

## Using `try...catch`

- Catches runtime exceptions and logs stack

```js
try {
  throw new Error("Custom Error");
} catch (error) {
  console.log(error.stack);
}
```

## Using `.stack` property

- Directly creates an `Error` object and accesses its `.stack` property

```js
console.log(new Error("custom error").stack);
```

## Using `console.trace()`

- Logs a stack trace at the point it’s called

```js
console.trace("Trace Message");
```

## Using `process.on('unhandledRejection')`

- Handles and logs unhandled promise rejections

```js
process.on("unhandledRejection", (err, promise) => {
  console.error("Unhandled rejection", err.stack);
});
```

## Using `Error.captureStackTrace()`

- Adds `.stack()` property to an object _manually_

```js
const obj = {};
Error.captureStackTrace(obj);
console.log(obj.stack);
```
