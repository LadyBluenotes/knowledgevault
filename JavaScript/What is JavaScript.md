---
title: What is JavaScript
date created: Saturday, April 26th 2025, 5:42:48 pm
date modified: Saturday, April 26th 2025, 6:56:34 pm
---

# What is JavaScript

- Lightweight interpreted programming language with first-class functions
- Prototype-based, multi-paradigm, single-threaded, dynamic-typed language
- Supports functional programming styles (object-orientated, imperative, and declarative)
- Programs in this language are called _scripts_ when used within a browser
  - Can be written right in the web page's HTML and runs automatically on page load
  - Provided and executed as plain text (do not need special prep or compilation to run)
- Can be used in non-browser environments, such as servers or other devices) using a JavaScript engine
  - Browsers have an embedded engine sometimes called "JavaScript virtual machine"
    - Chrome, Opera, Edge - [V8](<https://en.wikipedia.org/wiki/V8_(JavaScript_engine)>)
    - FireFox - [SpiderMonkey](https://en.wikipedia.org/wiki/SpiderMonkey)
    - Internet Explorer - Chakra
    - Safari - JavaScriptCore, Nitro, SquirrelFish
    - … etc

## Browser environments

- Does not provide low-level access to memory or CPU (browsers don't require it)
- Can do everything related to webpage manipulation, interaction with the user, and the webserver. Example:
  - Add new HTML to a page, change existing content, modify styles
  - React to user actions, run on mouse clicks, pointer movements, key presses
  - Send requests over the network to remote servers, download and upload files
  - Get and set cookies, show messages
  - Remember data on client-side ("local storage")

### What JS cannot do in browsers

- Actions are limited to protect user safety
  - Prevent webpages from accessing private information or harming user's data
- Examples of restrictions:
  - Cannot read/write arbitrary files on hard disk, copy them, or execute programs
    - No direct access to OS functions
  - Modern browsers may allow it to work with browsers, but access is limited to provide user to only do certain actions (eg. dropping a file into a browser window or selecting it via an input tag)
  - Cannot access other pages if they come from different sites from a different domain, protocol, or port
    - Called "Same Origin Policy"
  - To work around, _both pages_ must agree to data exchange
  - Requires special code that handles it
  - Ability to receive data from other sites/domains is crippled but through HTTP headers (ie. an explicit agreement on the remote side), they can share information
    - Limitations are not present outside the browser (eg. server)
    - Modern browsers allow for plugins/extensions which can ask for extended permissions

## Transpiled JavaScript

- Modern tooling makes it possible for new languages to quickly be transpiled (converted) to JavaScript before they’re run in the browser
- Examples: [CoffeeScript](https://coffeescript.org/), [TypeScript](https://www.typescriptlang.org/), [Flow](https://flow.org/), [Dark](https://www.dartlang.org/), [Brython](https://brython.info/), [Kotlin](https://kotlinlang.org/docs/reference/js-overview.html)

Resources:

- https://developer.mozilla.org/en-US/docs/Web/JavaScript
- https://javascript.info/intro
