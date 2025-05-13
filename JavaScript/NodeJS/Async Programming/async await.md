- a special syntax to work with promises in a more comfortable fashion
- Adding the keyword async before a function ensures that the function returns a promise and the keyword await makes JavaScript wait until that promise settles and returns the result
- Greatly improves **readability** and **maintainability** of complex async flows.

## `async`

- Functions defined with `async` return a **Promise**.
- Enables use of the `await` keyword within the function.

```js
async function fetchDataAndLog() {
  // async operations here
}
```

## `await`

- Pauses execution **until a Promise resolves or rejects**.
- Only usable inside an `async` function.
- Returns the resolved value of the Promise.

```js
async function processData() {
  const result = await fetchData();
  console.log(result);
}
```

## Practical applications

### Asynchronous data fetching

- Ideal for API calls or reading files.
- Simplifies complex async code that interacts with external systems.
- Always wrap `await` calls in `try...catch` if there's any chance of rejection.
- Don't let unhandled rejections crash your app.

### Sequential operations

- Ensures proper order of operations when one async task depends on another.

```js
async function performTasks() {
  let result1 = await task1();
  let result2 = await task2(result1);
  let result3 = await task3(result2);
  return result3;
}
```

### Error handling

- Use standard `try...catch` blocks for clean error management.
- Encourages robust and maintainable error handling patterns.

```js
async function safeFetch() {
  try {
    const data = await fetchData();
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}
```

## Best practices

- Avoid unnecessary `await` if operations can run **in parallel**.

```js
// Slower
const a = await getA();
const b = await getB();

// Faster
const [a, b] = await Promise.all([getA(), getB()]);
```

- Modern browsers support `async/await`, but older ones don’t.
- Use **Babel** or similar tools for transpilation if targeting legacy environments.
- Check compatibility if working in older ecosystems or embedded systems.
