- Enables programs to start potentially long-running tasks rather than having to wait until the task is finished
  - Once task is finished, program can present result
- Async code means that things can happen _independently_ of the main program flow
- Async functions in JS are processed in the _background_ without **blocking** other requests
  - Ensures non-blocking code execution
- Executes without having any dependency and no order
- Improves system efficiency and throughput

- Many functions provided by browsers can potentially take time and are, therefore, async
  - Examples include:
    - HTTP requests using `fetch()`
    - Accessing user’s camera or microphone using `getUserMedia()`
    - Asking a user to select files using `showOpenFilePicker()`

## Synchronous programming

- When code is executed in the order that it is written
- When browser waits for a line to finish its work, before going to the next line
  - Done this way because each line **depends** on the work done on the preceding lines

### Problems with long-running synchronous functions

- JavaScript is single-threaded, meaning a program consists of a single thread and can only do one thing at a time
- What is instead needed is:
  1. Start a long-running operation by calling a function
  2. Have that function start the operation and return immediately, so program can still be responsive to other events
  3. Have the function execute the operation in a way that does not block the main thread (eg. by starting new thread)
  4. Notify when the result eventually completes

## Event handlers

- A form of async programming: you provide a function (event handler) that will be called, not right away, but whenever the event happens
- The [XMLHttpRequest](XMLHttprequest.md) API enables the ability to make HTTP requests to a remote server using JS
  - Can take a long time and thus you will get notified about the progress and eventual completion of a request by attaching event listeners to the `XMLHttpRequest` object

## Callbacks

> Promises are used more than these in modern programming.

- An event handler is a particular type of callback
- Callback is a function that’s passed into another function
- Used to be the main way for async functions to be implemented
- Does make code hard to understand since the callback itself has to call functions that accept callbacks
  - Makes it harder to read and debug
  - Creates “callback hell” or the “pyramid of doom” (because the indentation looks like a pyramid on its size)
  - When nested, it also makes it more difficult to handle errors, since you have to handle errors at _each level_ instead of only error handling once at the top level
