- A **Promise** is an object representing the **eventual completion (fulfillment) or failure (rejection)** of an asynchronous operation.
- It acts as a **proxy** for a value not necessarily known when the promise is created.
- Allows async functions to return values like synchronous ones — via `then()` chaining.
- JavaScript is **single-threaded**; promises appear concurrent due to **event loop scheduling**
- For **true parallelism**, use **Web Workers** or other threading mechanisms.
- Promises represent **ongoing processes**, not lazily-started computations. For lazy evaluation, use functions:

```js
const f = () => expression;
f(); // triggers **evaluation**
```

## Promise states

- `pending`: initial state, neither fulfilled nor rejected.
- `fulfilled`: operation completed successfully.
- `rejected`: operation failed.
- A promise is **settled** when it is either fulfilled or rejected.
- **Resolved**: The promise is "locked-in" to a state (can still be pending, fulfilled, or rejected depending on what it's resolved with).

## State transitions

- `pending` → `fulfilled` or `rejected`.
- Once settled, the state is **immutable**.
- If resolved with another promise, it will follow the eventual state of that promise.

## Handlers

- `then(onFulfilled, onRejected)`: attaches fulfillment and rejection handlers.
- `catch(onRejected)`: shorthand for `then(undefined, onRejected)`.
- `finally(callback)`: runs regardless of fulfillment or rejection.

### Chaining promises

- `then()` returns a **new promise**.
- Outcome of the handler affects the next promise:
  - Returns a thenable → follows that promise's state.
  - Returns a value → fulfilled with that value.
  - Throws an error → rejected with that error.
- Error handling:
  - If no rejection handler is provided, the rejection propagates down the chain.
  - To maintain the error state after handling, rethrow the error in the rejection handler.

```js
Initial Promise → then() → then() → catch()
```

- Promises are queued jobs.
- Each handler is executed asynchronously in the job queue after current synchronous code completes.

### Async behaviour

- All handlers (`then`, `catch`, etc.) are **executed asynchronously**.
- Even if a promise is already settled, handlers will run **after** current execution completes (next tick).

### Multiple handlers on one promise

- A single promise can be used in **multiple chains**.
- Each `then()` on the same promise registers an independent job.

## Thenables

- Any object with a `.then()` method is a **thenable**.
- JavaScript promises can interoperate with thenables (from other libraries or custom objects).
- `Promise.resolve(thenable)` will follow the thenable's behavior.

## Promise concurrency

| Method                 | Behavior                                                                     |
| ---------------------- | ---------------------------------------------------------------------------- |
| `Promise.all()`        | Fulfills when **all** promises fulfill, rejects on the **first** rejection.  |
| `Promise.allSettled()` | Fulfills when **all** promises settle (fulfilled or rejected).               |
| `Promise.any()`        | Fulfills on the **first** fulfilled promise, rejects only if **all** reject. |
| `Promise.race()`       | Settles on the **first** promise to settle (fulfill or reject).              |

- All methods accept an **iterable of promises/thenables**.
- These methods support **subclassing** if custom promises are used.

## Cancellations

- Native `Promise` does **not** support cancellation.
- You can cancel underlying operations using tools like **`AbortController`**.
