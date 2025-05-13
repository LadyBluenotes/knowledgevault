- Module system allows for code to be split and include code as well as import code written by other developers when required
- Has many built-in modules that are part of the platform:
  - HTTP
  - fs
  - Path
  - & more
- Node has 2 module systems [CommonJS](CommonJS.md) and [ECMAScript modules](#ESM.md)

- Modules let you group related code together in separate files, making a project more organized and manageable
- Each module acts as a self-contained unit so you can hide certain parts of the code and only expose _what you want others to use_
- Can easily reuse modules in different parts of your project, reducing code duplication and promoting more efficient development processes
- Modules help you handle dependencies between different parts of the project
  - Makes it easier to keep track of how everything fits together

## Differences between CommonJS modules and ES Modules

| Aspect                     | CommonJS (`require`)                                                          | ES Modules (`import`)                                                        |
|----------------------------|--------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **File Extension**         | Uses `.js` by default                                                         | Uses `.mjs`, or `.js` if `type: "module"` is set in `package.json`           |
| **Import Syntax**          | `const module = require('module')`                                            | `import module from 'module'`                                               |
| **Export Syntax**          | `module.exports = value`                                                      | `export default value` or `export { value }`                                |
| **Static vs Dynamic**      | Dynamic — resolved at runtime                                                 | Static — resolved at parse time (hoisted)                                   |
| **Import Location**        | Can be used anywhere in the code                                              | Must be at the top level of the file                                        |
| **Interoperability**       | Can import CommonJS modules only                                              | Can import both ES Modules and CommonJS modules                             |
| **Project Configuration**  | No configuration needed                                                       | May require `.mjs` or `"type": "module"` in `package.json`                  |
| **Tooling Support**        | Widely supported, legacy-compatible                                           | Modern tooling supports it well; better static analysis and tree-shaking     |
| **When to Use**            | Best for existing or legacy projects                                          | Recommended for new projects                                                |
| **Migration Strategy**     | Continue using as-is; optionally migrate using Babel/TypeScript                | Use directly or transition from CommonJS gradually                          |

## `global` keyword

- Top-level scope 
- Global object is called the `window` object
- Within the **browser**, `var something` will define a new global variable *inside* the `window` object
- In Node, this is different - the top-level scope is **not** the global scope and `var something` inside a node module will be *local to that module*