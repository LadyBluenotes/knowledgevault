- concept to identify and remove errors from software applications

## Memory leaks

- caused when your node app’s CPU and memory usage increases over time for no apparent reason
  - Aka an orphan block of memory on the Heap that is no longer used by your app because it has not been released by the garbage collector
- Useless block of memory
- Can grow over time and lead to application crashing because it runs out of memory

## `console`

- `console.log()` – For general output. Include variable names & values (`console.log({ myVar })`).
- `console.error()` – Outputs errors with stack traces.
- `console.warn()` – Highlights potential issues without breaking flow.
- `console.table()` – Logs arrays or objects in tabular format (useful for readability).
- `console.group()` / `console.groupEnd()` – Nest related logs for clarity.
- `console.trace()` – Prints stack trace from where it's called.

## Browser DevTools

- **Breakpoints**:
  - Line breakpoints: Click line numbers in the **Sources** panel.
  - Conditional breakpoints: Right-click line number → “Add conditional breakpoint”.
  - DOM breakpoints: Watch for changes to specific elements.
  - Event listener breakpoints: Pause when certain browser events fire.
- **Watch Expressions**: Track the value of variables over time.
- **Call Stack**: Understand the execution path to current point.
- **Scope Panel**: Inspect local, closure, and global scopes during pause.
- **Step Controls**:
  - Step over (`F10`), into (`F11`), and out (`Shift+F11`) to trace execution.

## Handling async code

- Set breakpoints inside `.then()` or `async`/`await` code blocks.
- Use async stack traces (toggle in DevTools) for clearer tracebacks.
- Watch out for silent promise failures – always `.catch()` errors.

## Network and XHR debugging

- **Network Tab**: Monitor API requests, payloads, headers, and responses.
- **XHR/Fetch Breakpoints**: Pause execution when a request is sent.
- Inspect status codes, JSON responses, and request timing.

## Linting and static analysis

- Use ESLint or TypeScript for catching errors early.
- Enable strict mode (`'use strict';`) to catch silent failures like undeclared variables.

## Error handling techniques

- Gracefully handle runtime exceptions:

```js
try {
  riskyOperation();
} catch (err) {
  console.error("Error:", err);
}
```
