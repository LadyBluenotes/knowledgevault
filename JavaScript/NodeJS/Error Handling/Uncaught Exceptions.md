---
title: Uncaught Exceptions
date created: Tuesday, May 13th 2025, 11:51:21 am
date modified: Tuesday, May 13th 2025, 11:58:57 am
---

# Uncaught Exceptions

- When a JS error is not properly handled, an `uncaughtException` is emitted
  - Suggests there is an error and it should be treated as high priority
- Correct use of `uncaughtException` is to perform a _synchronous cleanup_ of allocated resources (eg. file descriptors, handles, etc) before shutting down the process
- **Not safe** to resume normal operation after because system becomes _corrupted_
- Best way is to let application crash, log the error, and restart the process

## The problem

- Since node runs on a _single process_, uncaught exceptions are an issue to be aware of
- Node follows a callback pattern when an error object is the first argument and data is the second argument
  - Not uncommon to see examples in documentation where an error is thrown if an error is returned by the callback

```js
var fs = require("fs");

fs.readFile("somefile.txt", function (err, data) {
  if (err) throw err;
  console.log(data);
});

// throws an error:
// Error: ENOENT, open 'somefile.txt'
```

- This will crash the process and bring down the whole application
  - By _design_
  - Node does not separate your application from the server

## Process behaviour and exit handling

- Node.js processes are **lightweight** with a **small memory footprint**
- Goal: keep **startup lean** for quick restarts after crashes
  - Avoid **CPU-intensive** or **synchronous** operations during startup
- Strategy: **prebuild** data/assets during deployment instead of at runtime
  - May increase deployment time, but reduces downtime during restarts

### Terminating a Node.js Process

- `process.exit(code)`
  - Exits the process; `0` = success, non-zero = error (e.g., `1`)
- `process.abort()`
  - Immediate termination; may produce a **core dump** (useful for debugging)

### Exit Events

- `beforeExit`
  - Emitted **before** the process exits
  - Allows **asynchronous operations**
  - Not triggered by `process.exit()` or `uncaughtException`
- `exit`
  - Emitted only when `process.exit()` is called
  - Only **synchronous** code can run here

### OS Signal Events

- Signals are sent by the OS to the Node.js process
- `SIGTERM`: sent by process managers (e.g., systemd) to request graceful shutdown
- `SIGINT`: triggered by Ctrl-C; can be captured to perform cleanup before exit
