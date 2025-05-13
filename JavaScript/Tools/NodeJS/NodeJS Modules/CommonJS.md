- Original way to package JS code for Node
- Supports the ECMAScript modules used by browsers and other JS runtimes

- Each file is treated as a separate module
- Functions and objects are added to the root of a module by specifying additional properties on the `export` object
- Variables local to the module will be private because module is [wrapped by a function by node](#Module%20wrapper%20function)

## Module wrapper function

- Before executing a module, Node wraps all the code inside that module with a function wrapper

```js
(function (exports, require, module, __filename, __dirname) {
  // Module code
});
```

- In doing this, node achieves the following:
  - Top level variables (`var`, `let`, `const`) are scoped to the **module** instead of the global object
  - Make _module-specific_ variables like global variables
    - Eg. `module` and `exports`
- Notice that the `exports` object references the `module.exports`

```js
console.log(module.exports === exports); // true
```

## Importing core NodeJS modules

- Node has built-in modules you can use without writing or installing any module

```js
const http = require("http");

const server = http.createServer(function (_req, res) {
  res.writeHead(200);
  res.end("Hello, World!");
});
server.listen(8080);
```

- The `http` module can be imported to create a simple Node server
  - Is identified by the `require()` via the string `"http"` which always points to the **Node internal module**
  - `require("http")` is handled like every other function invocation

## Importing NPM dependencies

- Similar to how you import and use modules from NPM packages
  - Require you to install via your package manager (eg. `npm install`, `pnpm add`)

```js
const chalk = require("chalk");

console.log(chalk.blue("Hello world printed in blue"));
```

## Exporting

- `export` keyword is fundamental part of module system
  - Allows the exposure of _specific_ parts of your code to be used in other files
    - Can expose functions or classes
- In using `export`, you can make this code available to other parts of your application or even in entirely separate files
  - Enables encapsulation within its own module, promoting code modularity and prevent unwanted access to internal functionalities

### Exporting own code

- To import code, CommonJS first needs to be told which parts of the code should be accessible to other modules

```js
// logger.js
const chalk = require("chalk");

exports.logInfo = function (message) {
  console.log(chalk.blue(message));
};

exports.logError = function logError(message) {
  console.log(chalk.red(message));
};

exports.defaultMessage = "Hello World";
```

- `logInfo()` and `logError()` are added to the `exports` object and `defaultMessage` is an example of how [default exports](#Default%20exports) can be combined

- To use the exports in another file, you just need to add the `require`
  - Uses a relative file path and returns whatever was put into the `exports` object

```js
// index.js
const logger = require("./logger");

logger.logInfo(`${logger.defaultMessage} printed in blue`);
logger.logError("some error message printed in red");
```

### `module.exports` vs `exports`

- `exports` is read-only
  - will always remain the same object instance and _cannot be overwritten_
  - only a shortcut to `exports` property of the `module` object

```js
// logger.js
const chalk = require("chalk");

function info(message) {
  console.log(chalk.blue(message));
}

function error(message) {
  console.log(chalk.red(message));
}

const defaultMessage = "Hello World";

module.exports = {
  logInfo: info,
  logError: error,
  defaultMessage,
};

// can also be

const chalk = require("chalk");

exports.logInfo = function (message) {
  console.log(chalk.blue(message));
};

exports.logError = function logError(message) {
  console.log(chalk.red(message));
};

exports.defaultMessage = "Hello World";
```

- rather than assigning functions _directly to an object_, they can be first declared and then another object can be created and assigned to `module.exports`
- exports don’t always have to be objects, they can also be **classes**

```js
// logger.js
const chalk = require("chalk");

class Logger {
  static defaultMessage = "Hello World";

  static info(message) {
    console.log(chalk.blue(message));
  }

  static error(message) {
    console.log(chalk.red(message));
  }
}

module.exports = Logger;
```

### Default exports

- Allow for a **single value** per file
- Done using the `export default` syntax
- This means, when you import from that file in another part of your code, you **do not** need curly braces `{ }` around the import statement
  - Can give it any name you want during import, making it more convenient to use

```js wrap
// 📂 math.js
const add = (a, b) => a + b;
export default add;

// 📂 main.js
import myAddFunction from "./math.js";
const result = myAddFunction(5, 10); // This will call the add function from math.js and store the result in the 'result' variable.
```

### Named exports

- Allow for _multiple_ exports per file
  - Name can be specified for each part individually
- Gives more control over the parts of code you want to share with other modules
  - Must use _exact_ names that were used during the export, ensuring that you can access and use the specific functions from the source file

```js
// 📂 math.js
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

// 📂 main.js
import { add, subtract } from "./math.js";

const result1 = add(5, 3); // result1 will be 8
const result2 = subtract(10, 4); // result2 will be 6
```

### Named vs default

| Feature                | Named Exports                                           | Default Export                                                |
| ---------------------- | ------------------------------------------------------- | ------------------------------------------------------------- |
| **Number of exports**  | Can export multiple values, functions, or classes       | Can only export one main value, function, or class            |
| **Import syntax**      | Use curly braces `{}` and must use exact exported names | No curly braces needed; can name the import whatever you like |
| **Use case**           | Best for exporting multiple distinct things             | Best for highlighting a single primary export                 |
| **Naming flexibility** | Must use the same names as exported                     | Can rename during import                                      |

### How to combine

- You can export _one_ main thing using `export default` while also exporting _multiple additional values_ using `export`
- Flexibility allows efficient organization and easier access and use of exported functionalities

## Importing

### Specific properties

- Since certain aspects of the code imported is needed in some cases, JS’s destructuring feature comes in handy

```js
// index.js
const { logError } = require("./logger");

logError("some error message printed in red");
```

## Importing specific properties

- Since only certain aspects of code may need to be imported,
