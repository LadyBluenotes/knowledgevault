- Standardized module system in JS that allows for organized, maintainable, and reusable structuring of code
- Uses import and export statements for including sharing functions or primitives between files
- Supports static analysis
    - Enables better optimzation and tooling
    - Is always in strict mode to reduce common JS issues
- Node fully supports ESM 
    - Can be used with `.mjs` extensions or configured in the `package.json` for `.js` files
        - Makes it easier to write modular and efficient JS applications

- Rather than `require()` which is used in [CommonJS](CommonJS.md) modules, there is the specific `export` and `import` syntax
    - Rather than a specific `module` object, the `export` keyword should be used

```js
// logger.mjs
import chalk from "chalk";

export class Logger {
  static defaultMessage = "Hello World";

  static info(message) {
    console.log(chalk.blue(message));
  }

  static error(message) {
    console.log(chalk.red(message));
  }
}
```

## Importing

- Slightly different syntax compared
    - To explicitly choose the property needed, use object destructuring

```js
// index.mjs
import { Logger } from "./logger.mjs";

Logger.info(`${Logger.defaultMessage} printed in blue`);
Logger.error("some error message printed in red");
```

### Named imports
- To import everything a module exports, you can give it a namespace

```js
// index.mjs
import * as LoggerModule from "./logger.mjs"

LoggerModule.Logger.info(`${LoggerModule.defaultMessage} printed in blue`);
LoggerModule.Logger.error("some error message printed in red");
```

- This would show that everything from the `"./logger.mjs"` is put into a namespace with the name `LoggerModule`
    - Fallback solution for imports from **non-ES Module files**

#### Named default imports

```js
import Logger from "./logger.mjs";

// is a shortcut for

import { default as Logger } from "./logger.mjs"
```

- Shortcut is a simpler way to read and follow imports

### Importing CommonJS modules

- NodeJS allows importing of CommonJS modules from ES Modules
- In these cases `module.exports` are treated as default exports and are imported as such

```js
// index.mjs
import Logger from "./logger.js";

Logger.info(`${Logger.defaultMessage} printed in blue`);
Logger.error("some error message printed in red");
```

## Exports vs default exports
- `default` keyword behind any `export` to say “treat this as the thing every module gets, if nothing specific is asked for”
    - Can import it by *leaving out the curly braces*

```js
// export
export default class Logger { ... }

// import
import Logger from "./logger.mjs";
```


