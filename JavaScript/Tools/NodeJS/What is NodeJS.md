> Used in server-side programming and primarily for deploying non-blocking, event-driven servers, such as traditional websites and back-end API services.
> 
> Originally designed in mind for push-based architectures.
> 
> NodeJS is built on Google Chrome’s V8 JavaScript engine

- An open-source, cross-platform **JavaScript Runtime**
- Runs the v8 JavaScript engine, Google Chrome’s core, outside the browser
- Runs in a single process, without creating a new thread for every request
- Provides a set of asynchronous I/O primitives in its standard library that prevent JavaScript code from blocking (when the execution of additional JavaScript in Node must wait until a non-JavaScript operation completes)
  - Asynchronous I/O primitives = low-level system tools that let programs perform input/output operations without blocking, using mechanisms like callbacks, futures, or event loops
  - Libraries in Node are written using non-blocking paradigms, making blocking behaviour the exception rather than the norm
- When Node performs an I/O operation, such as reading from the network, adding a DB or a filesystem, instead of blocking the thread and wasting CPU cycles waiting, Node will resume operations _when the response comes back_
  - Allows node to handle thousands of concurrent connections with a single server without the burden of managing thread concurrency (can be the source of bugs)

## Why Use Node

- Allows reducing the entire server-side application startup
- Can be used not only for server-side applications and web development, but because of its modularity, scalability, and accessibility via CLI there are more use cases
- Cross-platform support allows for creation of all kinds of applications: desktop apps, SaaS, mobile apps
- Good for data-intensive and real-time applications since it uses event-drive, non-blocking I/O model, making it lightweight and efficient
- Has a large community

### API

- Can write real-time applications while providing scope for mobile app development in JS
- Most popular type of application (API services) expose JSON objects with a REST API for client to consume

### Streaming web applications

- Has built-in streams which allow it to transmit large amounts of data in chunks, sequentially
- Great for use with listening to music or watching videos without the need to download

### Real-time web applications

- Event loop API and WebSockets make it possible to build real-time web applications (eg. chat, video conference, collaboration tools)

### Microservices

- Can be used to help build microservices
  - Applications as a collection of small services working independently

## Node vs Browser


| **Aspect**                      | **Browser JavaScript**                                                                 | **Node.js**                                                                                     | **Common Features (Both)**                                                                 |
|-------------------------------|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| **Environment**                | Runs in the web browser                                                               | Runs in a server-side environment                                                               | Both use the JavaScript language                                                           |
| **Access to APIs**            | Has access to Web APIs (DOM, `window`, `document`, `fetch`, `localStorage`, etc.)     | Has access to Node APIs (`fs`, `http`, `path`, etc.), but no DOM or `window`                    | Can work with APIs relevant to their environment                                           |
| **Module System**             | Uses ES Modules (`import`)                                                             | Supports both CommonJS (`require`) and ES Modules (`import`)                                   | Both use modules to organize code                                                          |
| **Language Compatibility**    | Often must support older JS versions (ES5+) for browser compatibility                 | Can use modern JavaScript features (ES6/ES2015+) if supported by the targeted Node version     | Both support modern JS with appropriate tools or environments                              |
| **Environment Control**       | No control over user's browser version                                                 | Full control over Node.js runtime version                                                      | Can define and control project dependencies via package managers (e.g., npm)               |
| **Global Objects**            | `window`, `document`, `navigator`, etc.                                                | `global`, `process`, `__dirname`, `__filename`                                                  | Both provide their own set of global objects                                               |
| **File System Access**        | Limited (only via user interaction like uploads/downloads)                            | Full access to file system through `fs` module                                                  | Both can work with data, but file handling is native only in Node                          |
| **Use Case**                  | UI rendering, event handling, animations, form interactions                           | Backend logic, server creation, API handling, database operations                              | Full-stack apps use both for frontend and backend logic                                    |
| **Tooling and Build Tools**   | Often requires transpilation (Babel) and bundling (Webpack, Vite)                     | Typically doesn't need transpilation unless targeting specific features                        | Can share tools like linters, formatters, and test libraries (e.g., ESLint, Jest)          |
| **Networking Capabilities**   | Limited to AJAX/fetch; no server-side socket handling directly                        | Native networking capabilities via `http`, `net`, and other core modules                       | Both can make HTTP requests (browser: `fetch`, Node: `http` or libraries like `axios`)     |