---
title: Turborepo
date created: Tuesday, April 22nd 2025, 11:14:15 am
date modified: Tuesday, April 22nd 2025, 11:28:48 am
---

# Turborepo

- Build system for JS and TS codebases
- Designed for scaling monorepos and making single-package workspaces faster

## How it Works

- [Remote cache](https://turbo.build/repo/docs/core-concepts/remote-caching) stores results of tasks, meaning CI doesn't need to do the same work twice.
- Task scheduling for maximum speed, parallelizing work across all cores
- Uses `package.json` scripts already written, with existing dependencies, and a single `turbo.json` file
  - Can be used with any package manager (`npm`, `yarn`, `pnpm`) since it leans on conventions of npm ecosystem

## How to Use

- Installing `turbo` globally lets you run commands in your terminal from anywhere in repo

```bash
pnpm install turbo --global
```

### Start Fresh

#### Single-package

- A single package is what you get after running `npm create solid`
- Doesn't require any additional configuration

#### Multi-package Workspace (monorepo)

- `turbo` is built on top of [Workspaces](https://docs.npmjs.com/cli/v7/using-npm/workspaces)

1. Add to repo

```
pnpm i --save-dev turbo
```

1. Add a `turbo.json` file
   - In root of repo

```

```

#### Template

```bash
npx create-turbo@latest
```

- Starters have:
  - Two deployable applications
  - Three shared libraries for use in the rest of the monorepo
- Offers many different templates:
  - [basic](https://github.com/vercel/turborepo/tree/main/examples/basic)
  - [with-solid](https://github.com/vercel/turborepo/tree/main/examples/with-solid)
  - [with-vite](https://github.com/vercel/turborepo/tree/main/examples/with-vite)
- See [other examples](https://turbo.build/repo/docs/getting-started/examples)

### Add to Existing

https://turbo.build/repo/docs/getting-started/add-to-existing-repository

### Commands

- `turbo build`: Run `build` scripts following your repository's dependency graph
- `turbo build --filter=[something] --dry`: Quickly print an outline of `build` for `[something]` package **without running it**
- `turbo generate`: Run Generators to add new code to repo
  - Generate new source code for packages, modules, and individual UI components in a structured way that integrates with repo
- `cd [path] && turbo build`: Run the `build` script in the `[path]` package and its dependencies

#### `turbo run`

- Reference docs: <https://turbo.build/repo/docs/reference/run>
- Run tasks specified in `turbo.json`

```
turbo run [tasks] [options] [-- [args passed to tasks]]
```

- `[tasks]`: can run one or more tasks at the same time.
- `[options]`: used to control behaviour of `turbo run` command
- `[--[args passed to tasks]]`: Pass arguments to underlying scripts. All arguments will be passed to all tasks that are named in the run command

> [!Good to know] > `turbo run` is aliased to `turbo`. This means `turbo run build lint check-types` is the same as `turbo build lint check-types`. Use `turbo run` in ci piplines and `turbo`locally with global turbo for ease of use

- If no tasks are provided, `turbo` will display what tasks are available for packages in repo

## `turbo.json`

- Info: <https://turbo.build/repo/docs/reference/configuration>

| Option               | Description                                                                                                                                                              | Location | Example                                           |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | ------------------------------------------------- |
| `extends`            | Extend from root `turbo.json` to create specific configu for a package using [package configurations](#package-configurations). Will be ignored in the root `turbo.json` | package  | `"extends": ["//"]`                               |
| `globalDependencies` | List of globs to include in all task hashes. If any file matching these change, all tasks will miss cache. Are relative to the location of `turbo.json`                  | root     | `"globalDependencies": [".env", "tsconfig.json"]` |
| `tasks`              | Each key is the name of the task that can be executed by `turbo.run`. Will search packages for scripts in `package.json` with the name of the task.                      |          |                                                   |

### Task Options

#### `dependsOn`

- List of tasks that are required to complete before task begins running

##### Dependency Relationships

- Prefixing a string in `dependsOn` with `^` tells `turbo` that the task must _wait_ for tasks in package's dependencies to complete first.

```json
// ./turbo.json
{
  "tasks": {
    "build": {
      "dependsOn": ["^build"]
    }
  }
}
```

- `turbo` starts at the "bottom" of the package graph and recursively visits each package until it finds a package with no dependencies. Will then run `build` task at the end of dependency chain first, then work its way back to the "top" until all `build` tasks are completed in order

##### Same Package Relationships

- Task names _without_ `^`, describe a task that depends on a different task within the same package

```json
{
  "tasks": {
    "test": {
      "dependsOn": ["lint", "build"]
    }
  }
}
```

- Task will only run after `lint` and `build` tasks have completed in **the same package**

##### Arbitrary Task Relationships

Specify a task dependency between specific package tasks.

```json
{
  "tasks": {
    "web#lint": {
      "dependsOn": ["utils#build"]
    }
  }
}
```

#### `env`

- List of environment variables a task depends on

```json
{
  "tasks": {
    "build": {
      "env": ["DATABASE_URL"] // Impacts hash of all build tasks
    },
    "web#build": {
      "env": ["API_SERVICE_KEY"] // Impacts hash of web's build task
    }
  }
}
```

- Wildcards for environment variables can be used to account for all with a given prefix

```json
{
  "tasks": {
    "build": {
      "env": ["MY_API_*"]
    }
  }
}
```

- Using `!` means the entire pattern with bee negated

```json
{
  "tasks": {
    "build": {
      "env": ["!MY_API_URL"]
    }
  }
}
```

#### `outputs`

- List of glob patterns relative to the package's `package.json` when the task is successfully completed

```json
{
  "tasks": {
    "build": {
      // Cache all files emitted to the packages's `dist` directory
      "outputs": ["dist/**"]
    }
  }
}
```

#### `cache`

- Defines if task outputs should be cached
- Setting to false is helpful for long-running **development tasks** that a task always runs when it is in the task's execution graph

```json
{
  "tasks": {
    "build": {
      "outputs": [".svelte-kit/**", "dist/**"] // File outputs will be cached
    },
    "dev": {
      "cache": false, // No outputs will be cached
      "persistent": true
    }
  }
}
```

#### `inputs`

- All files in the package that are checked into source control
- List of file glob patterns relative to package's `package.json` to consider when determining if a package has changed

```json
{
  "tasks": {
    "test": {
      "inputs": ["src/**/*.ts", "src/**/*.tsx", "test/**/*.ts"]
    }
  }
}
```

#### `persistent`

- A task should be labeled `persistent` to prevent other tasks from depending on long-running processes

```json
{
  "tasks": {
    "dev": {
      "persistent": true
    }
  }
}
```

## Package Configurations

- Turborepo enables you to extend root config with a `turbo.json` in any package
  - Enables more diverse apps and packages to co-exist in a Workspace
  - Allow package owners to maintain specialized tasks and configuration without affecting other apps and packages of monorepo
- To **override** config for any task in the **root** `turbo.json`, add a `turbo.json` file in any package of your monorepo with a top-level `extends` key

```json
// ./apps/my-app/turbo.json
{
  "extends": ["//"], // identifies root directory of monorepo
  "tasks": {
    "build": {
      // Custom configuration for the build task in this package
    },
    "special-task": {} // New task specific to this package
  }
}
```

### Different Frameworks in One Workspace

#### Root `turbo.json`

```json
// ./turbo.json
{
  "tasks": {
    "build": {
      "outputs": [".next/**", "!.next/cache/**", ".svelte-kit/**"]
    }
  }
}
```

#### Custom Configuration

- To run these tasks, you can add a custom configuration in the package

```json
// apps/my-svelte-kit-app/turbo.json
{
  "extends": ["//"],
  "tasks": {
    "build": {
      "outputs": [".svelte-kit/**"]
    }
  }
}
```

Then you can remove the framework-specific `outputs` from the root config:

```json
// ./turbo.json
{
  "tasks": {
    "build": {
      "outputs": [".next/**", "!.next/cache/**"]
    }
  }
}
```

- Makes configs easier to read, and puts configs closer to where they are used

#### Comparison to Package-specific Tasks

- When you declare a package-specific task in the root `package.json`, it is **completely overwrites** the baseline task config. With a package config, task configurations are merged instead

```json
// ./turbo.json
{
  "tasks": {
    "build": {
      "outputLogs": "hash-only",
      "inputs": ["src/**"],
      "outputs": [".next/**", "!.next/cache/**"]
    },
    "my-sveltekit-app#build": {
      "outputLogs": "hash-only", // must duplicate this
      "inputs": ["src/**"], // must duplicate this
      "outputs": [".svelte-kit/**"]
    }
  }
}
```

- In this example, `my-sveltkit-app#build` completely overwrites `build` for the Sveltekit app so `outputLogs` and `inputs` also need to be duplicated
- With package configs, `outputLogs` and `inputs` are inherited, you don't need to duplicate them, you only need to override `outputs` in `my-sveltekit-app` config

## Running Tasks

- Optimizes developer workflows in repo by automatically parallelizing and caching tasks

### Using `scripts` in `package.json`

- For tasks run frequently, can write `turbo` commands directly into **root** `package.json`

```json
{
  "scripts": {
    "dev": "turbo run dev",
    "build": "turbo run build",
    "test": "turbo run test",
    "lint": "turbo run lint"
  }
}
```

- Package manager can then be used to run these scripts
- Only write `turbo` commands in the root `package.json`. If in any packages, can lead to recursively calling `turbo`

## Generating Code

```
turbo gen workspace
```

- All options: <https://turbo.build/repo/docs/reference/generate#workspace>

### Copy Existing Package

- Use existing workspace as a template for new app or package
- `turbo gen workspace --copy`: create a new package by copying an existing package in repo
- `turbo gen workspace --copy [GitHub URL]`: create a new workspace in monorepo by copying from a remote package
- Can [create your own custom generators](https://turbo.build/repo/docs/guides/generating-code#custom-generators)

## Task Graph

- In the `turbo.json` you can express how tasks relate to each other
  - Thought of as dependencies between tasks
- Turbo uses the [directed acyclic graph(DAG)](https://en.wikipedia.org/wiki/Directed_acyclic_graph) to understand a repo and its tasks. Made up of "nodes" and "edges" - Nodes are tasks - Edges are dependencies between tasks - "Directed" graph indicates the edges connecting each node have a direction
  **NEED TO BETTER UNDERSTAND**

## Using Filters

- Filtering tasks lets you run only a subset of tasks in [the task graph](#task-graph)

| Microsyntax           | Description                                                                                                                                                                          |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `!`                   | negate targets from selection                                                                                                                                                        |
| `…` using packages    | Select all packages in package graph relative to target. Using _before_ package name will select **dependents**. Using _after_ package name, will select **dependencies of target**. |
| `…` using git commits | Select a range using `[<from commit>]…[<to commit>]`                                                                                                                                 |
| `^`                   | Omit target from selection when using `…`                                                                                                                                            |

- Turbo reference for `--filter`: <https://turbo.build/repo/docs/reference/run#--filter-string>

### Filtering by Package

- Simple way to run tasks for the packages you're currently working on

```bash
turbo build --filter=[package]
```

- Can run a filter to a specific task for package you're in via CLI without using `--filter`

```
turbo run [package]#[task]
```

- Can run multiple

```
turbo run web#build docs#lint
```

### Filtering to Include Dependents

- When you want to run tasks for the package and its dependents
- Using `…` microsyntax is useful when you're making changes to a package and want to ensure changes don't break any dependents

```
turbo build --filter= ... ui
```

### Filtering to Include Dependencies

- To limit scope to a package and its dependencies, append `…` to the package name
- This runs task for specified package and all packages it depends on

```
turbo dev --filter=web...
```

### Filtering by Source Control Changes

- Using filters to run tasks based on changes in source control to run tasks only for the packages that are affected by your changes
- Source control filters must be wrapped in `[]`
  - Comparing to the previous commit: `turbo build --filter=[HEAD^1]`
  - Comparing to main branch: `turbo build --filter=[main…my-feature]`
  - Comparing specific commits using SHAs: `turbo build --filter=[a1b2c3d…e4f5g6h]`
  - Comparing specific commits using branch names: `turbo build --filter=[your-feature…my-feature]`

### Combining Filters

- For more specificity, you can combine filters to further refine entry points into task graph

```
turbo build --filter=...ui --filter={./packages/*} --filter=[HEAD^1]
```

- Are combined as a union
  - will include tasks that match **any** of the filters

## Automatic Package Scoping

- Turbo will automatically scope commands to the [package graph](https://turbo.build/repo/docs/core-concepts/package-and-task-graph#package-graph) for that package
  - This means you can write commands without having to [write filters](#using-filters) for the package

```
cd apps/docs
turbo build
```

- Would run the `build` task for the `docs` package using the `build` task registered in `turbo.json`

## Managing dependencies

- External dependencies - come from npm registry
- Internal dependencies - share functionality within **your** repo, improving discoverability and usability of shared code

### Best practices

1. Install dependencies where they're used. Benefits:
   - Know which package depends on what dependency
   - Keep track of the versions required for each dependency
   - Avoid too many dependencies in root of repo
     - Prevents you from changing workspace root whenever a dependency is added, updated, or deleted
2. Few dependencies in root
   - Only dependencies that belong in workspace root are **tools for managing the repo**.
   - Building applications and library dependencies should be in their respective packages
