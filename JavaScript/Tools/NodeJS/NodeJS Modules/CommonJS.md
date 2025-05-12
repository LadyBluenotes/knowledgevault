- Original way to package JS code for Node
- Supports the ECMAScript modules used by browsers and other JS runtimes

- Each file is treated as a separate module
- Functions and objects are added to the root of a module by specifying additional properties on the `export` object
- Variables local to the module will be private because module is [wrapped by a function by node](#Module%20wrapper)

## Enabling

- By default, NodeJS will treat the following as CommonJS modules:
  - Files with `.cjs` extension
  - Files with a `.js` extension when the nearest parent `package.json` contains a top-level field `"type"` with a value of `"commonjs"`
  - Files with a `.js` extension or without an extension, when the nearest parent `package.json` file doesn't contain a top-level field `"type"` or there is no `package.json` in any parent folder (unless the file contains syntax that errors unless it is evaluated as an ES module)
    - Package authors should include the `"type"` field, even in packages where all sources are CommonJS
    - Being explicit about the `type` of the package will make things easier for build tools and loaders to determine how the files in the package should be interpreted
  - Files with an extension that is not `.mjs`, `.cjs`, `.json`, `.node`, or `.js` (when the nearest parent `package.json` file contains a top-level field `"type"` with a value of `"module"`
    - files will be recognized as CommonJS modules only if they are being included via `require()`, not when used as the command-line entry point of the program

## Accessing main module

- When a file is run directly from Node.js, `require.main` is set to its `module`
  - Means that it is possible to determine whether a file has been run directly by testing `require.main === module`
- When the entry point is not a CommonJS module, `require.main` is `undefined`, and
- main module is out of reach

## Package manager tips

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

## Loading ECMAScript modules using require()

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

## Caching

- Modules are **cached** after being loaded the first time.
- Multiple calls to `require('foo')` return the **same object** if the file path resolves identically.
- Module code is **not re-executed** on subsequent `require()` calls (unless `require.cache` is modified).
- This allows:
  - Reuse of loaded modules.
  - Support for **cyclic dependencies** by returning partially constructed exports.
- To execute module code multiple times:
  - **Export a function**.
  - **Call the function** each time execution is needed.

### Module caching caveats

- Modules are **cached based on their resolved filename**.
- `require('foo')` may return **different objects** if the resolution leads to **different files** (e.g., due to different calling module locations).
- On **case-insensitive file systems** (e.g., Windows/macOS), filenames like `'./foo'` and `'./FOO'` may refer to the **same file**, but:
  - Node treats them as **different modules**.
  - They are **cached separately** and **executed separately**.

## Built-in modules

- Node.js includes **built-in modules** compiled into the binary, located in the `lib/` folder of the source.
- Built-in modules can be loaded using the **`node:` prefix** (e.g., `require('node:http')`), which **bypasses the require cache**.
- Some built-in modules are **always loaded preferentially**, even if a file with the same name exists (e.g., `require('http')` loads the built-in module, not a local file).
- A list of all built-in modules is available via `module.builtinModules`.
  - The list **excludes the `node:` prefix**, except for modules that **require it explicitly**.

### Built-in modules with mandatory `node:` prefix

- Some built-in modules **must be required using the `node:` prefix** (e.g., `require('node:test')`).
- This requirement avoids **conflicts with user-installed packages** that may use the same names.
- Currently, the modules that require the `node:` prefix are:
  - [`node:sea`](https://nodejs.org/api/single-executable-applications.html#single-executable-application-api)
  - [`node:sqlite`](https://nodejs.org/api/sqlite.html)
  - [`node:test`](https://nodejs.org/api/test.html)
  - [`node:test/reporters`](https://nodejs.org/api/test.html#test-reporters)
- These modules appear in [`module.builtinModules`](https://nodejs.org/api/module.html#modulebuiltinmodules) **with the `node:` prefix included**.

## Cycles

- When circular `require()` calls occur, a module may be **incomplete** when it's returned to another module.
- For example, if **Module A requires Module B**, and **Module B requires Module A** in return:
  - Node.js avoids an infinite loop by returning a **partially completed export** of Module A to Module B.
- This allows both modules to finish loading, but each must handle the possibility of **incomplete data** during the process.
- Once all modules are fully loaded, their exports are complete and consistent.
- **Careful design** is needed to ensure cyclic dependencies work properly without causing unexpected behavior.

## File modules

- If the exact filename isn't found, Node.js tries adding extensions in this order: **`.js` → `.json` → `.node`**.
- For files with **non-standard extensions** (e.g., `.cjs`), the **full filename with extension** must be provided.
- File types are handled as follows:
  - `.json`: Parsed as JSON text.
  - `.node`: Treated as compiled addons via `process.dlopen()`.
  - Others/no extension: Parsed as JavaScript.
- Path rules for `require()`:
  - `'/'` prefix: Treated as an **absolute path**.
  - `'./'` or `'../'`: Treated as **relative to the calling file**.
  - No prefix: Treated as a **core module** or **resolved from `node_modules`**.
- If the module path is invalid or not found, a **`MODULE_NOT_FOUND` error** is thrown.

## Folders as modules

- A folder can be passed to `require()` in three ways:
  1. **With a `package.json` file**: If the folder contains a `package.json` with a "main" entry, Node.js will attempt to load the specified main module.
  2. **Without a `package.json` file**: If there's no `package.json`, Node.js will try loading `index.js` or `index.node` from the directory.
  3. **If neither option works**: Node.js will throw a `MODULE_NOT_FOUND` error.
- For `import()` calls, using folders as modules results in an **`ERR_UNSUPPORTED_DIR_IMPORT`** error.
- **Package subpath exports or subpath imports** can provide similar functionality, allowing better organization while supporting both `require()` and `import()`.

## Loading from `node_modules` folders

- If the module identifier does not:
  1. Belong to a built-in module, and
  2. Start with `'/'`, `'../'`, or `'./'`,
     Then Node.js starts from the current module's directory and looks for the module in the `/node_modules` folder.
- If not found there, it moves up to the parent directory and continues searching until it reaches the root of the filesystem.
- Example resolution path order:
  - `/home/ry/projects/node_modules/bar.js`
  - `/home/ry/node_modules/bar.js`
  - `/home/node_modules/bar.js`
  - `/node_modules/bar.js`
- This behavior allows **localizing dependencies** to avoid conflicts.
- To require specific files or submodules in a module, a **path suffix** can be used (e.g., `require('example-module/path/to/file')`), and it follows the same resolution rules.

## Loading from the global folders

- The **`NODE_PATH`** environment variable allows Node.js to search additional **absolute paths** for modules if they are not found in the default locations.
  - On **Windows**, paths are delimited by semicolons (`;`).
  - **`NODE_PATH`** is less necessary now due to the established module resolution system, but still supported.
  - Issues can arise when the **`NODE_PATH`** isn't set correctly, leading to loading unexpected versions or modules.
- In addition to `NODE_PATH`, Node.js searches these **global folders** for modules:
  1. `$HOME/.node_modules`
  2. `$HOME/.node_libraries`
  3. `$PREFIX/lib/node`
  - `$HOME` refers to the user's home directory, and `$PREFIX` is the configured Node.js installation prefix.
- It's **recommended** to place dependencies in the **local `node_modules` folder** for faster and more reliable module loading.
