---
title: Running scripts
date created: Tuesday, May 13th 2025, 10:56:01 am
date modified: Tuesday, May 13th 2025, 11:08:38 am
---

# Running scripts

- npm scripts are used for the purpose of:
  - initiating a server
  - starting the build of a project
  - running tests
- are defined in the `package.json` file
- can split large scripts into many smaller parts if needed

`"scripts"` property is part of `package.json` and supports a number of built-in scripts and their preset life cycle events as well as arbitrary scripts

- can be executed by running `npm run-script <stage>` or `npm run <stage>`
- pre and post commands with matching names will be run for those as well (eg. `premyscript`, `myscript`, `postmyscript`)
- scripts from dependencies can be run with `npm explore <package> -- npm run <stage>`

## Pre and post scripts

- To create "pre" and "post" scripts for any scripts defined in the `"scripts"` section, simply create another script with a _matching name_ and add "pre" or "post" to the beginning of them

```json
{
  "scripts": {
    "precompress": "{{ executes BEFORE `compress` script }}",
    "compress": "{{ run command to compress files }}",
    "postcompress": "{{ executes AFTER `compress` script }}"
  }
}
```

## Life cycle scripts

- Some special life cycle scripts only happen in certain situations
- Can happen in addition to `pre<event>`, `post<event>`, and `<event>` scripts

### `prepare`

- Run **BEFORE** package is packed (ie. during `npm publish` and `npm pack`)
- Runs on local `npm install` without any arguments
- Runs **AFTER** `prepublish` but **BEFORE** [`prepublishOnly`](#`prepublishOnly`)

### `prepublish` (depreciated)

> To read why it was deprecated, see [this issue](https://github.com/npm/npm/issues/10074) or [this section of the npm docs](https://docs.npmjs.com/cli/v11/using-npm/scripts#prepare-and-prepublish)

- Does not run during `npm publish`, but does run during `npm ci` and `npm install`

### `prepublishOnly`

- Runs **BEFORE** the package is prepared and packed, ONLY on `npm publish`.

### `prepack`

> "`npm run pack`" is **NOT** the same as "`npm pack`". "`npm run pack`" is an arbitrary user defined script name, where as, "`npm pack`" is a CLI defined command.

- Runs **BEFORE** a tarball is packed (on "`npm pack`", "`npm publish`", and when installing a git dependency).

### `postpack`

- Runs **AFTER** the tarball has been generated but before it is moved to its final destination (if at all, publish does not save the tarball locally)

### `dependencies`

- Run any time an `npm` command causes changes to the `node_modules` directory
- Run **AFTER** the changes have been applied and the `package.json` and `package-lock.json` files have been updated
- Does **NOT** run in global mode

## Life cycle operation order

[`npm cache add`](https://docs.npmjs.com/cli/v11/commands/npm-cache)

1. `prepare`

[`npm ci`](https://docs.npmjs.com/cli/v11/commands/npm-ci)

These all run after the actual installation of modules into `node_modules`, in order, with no internal actions happening in between

1. `preinstall`
2. `install`
3. `postinstall`
4. `prepublish`
5. `preprepare`
6. `prepare`
7. `postprepare`

[`npm diff`](https://docs.npmjs.com/cli/v11/commands/npm-diff)

1. `prepare`

[`npm install`](https://docs.npmjs.com/cli/v11/commands/npm-install)

also run when you run `npm install -g <pkg-name>`
If there is a `binding.gyp` file in the root of your package and you haven't defined your own `install` or `preinstall` scripts, npm will default the `install` command to compile using node-gyp via `node-gyp rebuild`
are run from the scripts of `<pkg-name>`

1. `preinstall`
2. `install`
3. `postinstall`
4. `prepublish`
5. `preprepare`
6. `prepare`
7. `postprepare`

[`npm pack`](https://docs.npmjs.com/cli/v11/commands/npm-pack)

1. `prepack`
2. `prepare`
3. `postpack`

[`npm publish`](https://docs.npmjs.com/cli/v11/commands/npm-publish)

1. `prepublishOnly`
2. `prepack`
3. `prepare`
4. `postpack`
5. `publish`
6. `postpublish`

[`npm rebuild`](https://docs.npmjs.com/cli/v11/commands/npm-rebuild)

`prepare` is only run if the current directory is a symlink (e.g. with linked packages)

1. `preinstall`
2. `install`
3. `postinstall`
4. `prepare`

[`npm restart`](https://docs.npmjs.com/cli/v11/commands/npm-restart)

If there is a `restart` script defined, these events are run, otherwise `stop` and `start` are both run if present, including their `pre` and `post` iterations)

1. `prerestart`
2. `restart`
3. `postrestart`

[`npm run <user defined>`](https://docs.npmjs.com/cli/v11/commands/npm-run-script)

1. `pre<user-defined>`
2. `<user-defined>`
3. `post<user-defined>`

[`npm start`](https://docs.npmjs.com/cli/v11/commands/npm-start)

If there is a `server.js` file in the root of your package, then npm will default the `start` command to `node server.js`. `prestart` and `poststart` will still run in this case.

1. `prestart`
2. `start`
3. `poststart`

[`npm stop`](https://docs.npmjs.com/cli/v11/commands/npm-stop)

1. `prestop`
2. `stop`
3. `poststop`

[`npm test`](https://docs.npmjs.com/cli/v11/commands/npm-test)

1. `pretest`
2. `test`
3. `posttest`

[`npm version`](https://docs.npmjs.com/cli/v11/commands/npm-version)

1. `preversion`
2. `version`
3. `postversion`

## User

- when npm is run as root, scripts are always run with the effective uid and gid of the working directory owner

## Environment

- package scripts run in an environment where many pieces of info are made available regarding setup of npm and current state of process

### path

- If modules define executable scripts (like test suites), then those executables will be added to the `PATH` for executing scripts

```json
{
  "name": "foo",

  "dependencies": {
    "bar": "0.1.x"
  },

  "scripts": {
    "start": "bar ./test"
  }
}
```

### package.json vars

- tacked onto `npm_package_` prefix
  - if `{"name": "foo", "version":"1.2.5"}` in your `package.json`, packages scripts would have the `npm_package_name` env variable set to “foo” and the `npm_package_version` set to `"1.2.5"`
  - Can be accessed with `process.env.npm_package_name` and `process.env.npm_package_version`, etc. for toher fields

### current lifecycle event

- `npm_lifecycle_event` env variable set to whichever stage the cycle is beinge xecuted
  - Single script can be used for different parts of the process which switches based on what’s currently happening
- Objects are flattened following this format
  - `{"scripts": "install":"foo.js"}` would be `process.env.npm_package_scripts_install === foo.js`

## Exiting

> These script files don’t have to be NodeJS or even JS programs. Just need an executable file

- Scripts are run by passing the line as a script argument to `sh`
- If a script exits with a code other than 0, then this will abort the process

## Best practices

- Don’t exit with an non-zero code
  - If failure is minor or will prevent some optional features, better to just print a warning and exit successfully
- Try not to use scripts to do what npm can
  - [`package.json`](https://docs.npmjs.com/cli/v11/configuring-npm/package-json) docs can show the things that you can specify and enable by simply describing your package appropriately
    - leads to more robust and consistent state
- Inspect env to determine where to put things
- Don’t prefix script commands with `sudo`
  - If root permissions are required for some reason, it’ll fail with that error and the user will sudo the npm command in question
- Don’t use `install`
  - Use a `.gyp` file for compilation
  - Use [`prepare`](#`prepare`) for anything else
  - Should almost never have to explicitly set a preinstall or install script
    - Only valid use for `install` and `preinstall` is compilation which must be done on the _target infra_
- Scripts are run from the _root_ of the package folder regardless of current working directory where `npm` is invoked
  - If you want a script to use different behaviour based on subdirectory used, use `INIT_CWD` env variable, which holds full path you were in when you ran `npm run`
