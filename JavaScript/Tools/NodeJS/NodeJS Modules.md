- Module system allows for code to be split and include code as well as import code written by other developers when required
- Has many built-in modules that are part of the platform:
  - HTTP
  - fs
  - Path
  - & more
- Node has 2 module systems [CommonJS](#CommonJS%20modules) and ECMAScript modules

## Module wrapper

- Before a module is executed, Node will wrap it with a function wrapper that looks like the following:

```js
(function (exports, require, module, __filename, __dirname) {
  // Module code actually lives in here
});
```

By doing this, Node achieves a few things:

- Keeps top-level variables (`let`, `var`, `const`) scoped to the module vs global object
- Helps provide some global-looking variables that are specific to the module
  - `module` and `exports` objects that the implementor can use to export values from the module
  - Convenience variables `__filename` and `__dirname` containing the module’s absolute filename and directory path

## CommonJS modules

- Original way to package JS code for Node
- Supports the ECMAScript modules used by browsers and other JS runtimes

- Each file is treated as a separate module
- Functions and objects are added to the root of a module by specifying additional properties on the `export` object
- Variables local to the module will be private because module is [wrapped by a function by node](#Module%20wrapper)

### Enabling

- By default, NodeJS will treat the following as CommonJS modules:
  - Files with `.cjs` extension
  - Files with a `.js` extension when the nearest parent `package.json` contains a top-level field `"type"` with a value of `"commonjs"`
  - Files with a `.js` extension or without an extension, when the nearest parent `package.json` file doesn't contain a top-level field `"type"` or there is no `package.json` in any parent folder (unless the file contains syntax that errors unless it is evaluated as an ES module)
    - Package authors should include the `"type"` field, even in packages where all sources are CommonJS
    - Being explicit about the `type` of the package will make things easier for build tools and loaders to determine how the files in the package should be interpreted
  - Files with an extension that is not `.mjs`, `.cjs`, `.json`, `.node`, or `.js` (when the nearest parent `package.json` file contains a top-level field `"type"` with a value of `"module"`
    - files will be recognized as CommonJS modules only if they are being included via `require()`, not when used as the command-line entry point of the program

### Accessing main module

- When a file is run directly from Node.js, `require.main` is set to its `module`
  - Means that it is possible to determine whether a file has been run directly by testing `require.main === module`
- When the entry point is not a CommonJS module, `require.main` is `undefined`, and
- main module is out of reach

### Package manager tips

- `require()` was designed to be general enough to support reasonable directory structures

- **Directory Structure:**
  - `/usr/lib/node/<package>/<version>/` holds the contents of a specific package version.
    - Example: `/usr/lib/node/foo/1.2.3/` for the `foo` package, version 1.2.3.
  - Dependencies of packages (e.g., `foo` depends on `bar`) are placed in respective directories.
    - `/usr/lib/node/foo/1.2.3/node_modules/bar` is a symbolic link to the real location of `bar` (e.g., `/usr/lib/node/bar/4.3.2/`).
  - Dependencies of `bar` are linked in `/usr/lib/node/bar/4.3.2/node_modules/*`.
- **Package Dependencies & Cyclic Dependencies:**
  - Packages can depend on others (e.g., `foo` depends on `bar`).
    - Dependencies may have their own dependencies, and cyclic dependencies can occur.
      - Node.js resolves these dependencies through symlinks to the appropriate package versions.
- **Optimization:**
  - Instead of placing packages directly in `/usr/lib/node`, use `/usr/lib/node_modules/<name>/<version>` for module storage.
  - This prevents Node.js from looking in unnecessary locations like `/usr/node_modules` or `/node_modules`.
- **REPL Integration:**
  - To make modules available in the Node.js REPL, add `/usr/lib/node_modules` to the `$NODE_PATH` environment variable.
- **Module Lookup Process:**
  - Node.js uses the realpath of files and checks relative `node_modules` folders for dependencies.
  - Packages and their dependencies can be located anywhere, as long as the symlinks are set correctly.

### Loading ECMAScript modules using require()

- **.mjs Extension**:
  - Reserved for **ECMAScript Modules (ESM)**.
  - Files with `.mjs` are parsed as ESM.
- **require() with ECMAScript Modules**:
  - **Synchronous loading** (no top-level `await`).
  - Conditions to load an ESM with `require()`:
    1. File has `.mjs` extension.
    2. File has `.js` extension and `package.json` contains `"type": "module"`.
    3. File has `.js` extension, no `"type": "commonjs"` in `package.json`, and contains ESM syntax.
- **Interoperability**:
  - For tools converting ES Modules to CommonJS, the returned namespace contains `__esModule: true` if the module has a default export.
  - This property is **experimental** and should not be relied on in CommonJS code directly.
- **Named Exports & Default Export**:
  - When an ESM has both named and default exports:
    - `require()` returns the module namespace object.
    - Default export is in `.default` property (like `import()`).
    - CommonJS consumers can access named exports via the default export.
- **Top-Level Await**:
  - If an ESM contains top-level `await` or the module graph includes it, **ERR_REQUIRE_ASYNC_MODULE** is thrown.
  - Users should use `import()` for such modules.
  - `--experimental-print-required-tla` option allows Node.js to print top-level await locations.
- **Experimental Feature**:
  - ES Module loading via `require()` is **experimental**.
  - Can be disabled with `--no-experimental-require-module`.
  - To trace the usage of this feature, use `--trace-require-module`.
  - Can be detected by checking if `process.features.require_module` is `true`.
