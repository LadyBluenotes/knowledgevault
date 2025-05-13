- Mainly used when adding a package or dependency as part of a specific project being worked on
- Package would be installed (with its dependencies) in `node_modules` folder **under your project**
- In `package.json`, there will be a _new line_ added for the installed dependency under the label `dependencies`
- Can install packages and dependencies globally or local to your project

## Global

- when a dependency is installed in a system path
- Makes the dependency available to any program being run on _that specific computer_
- Often used for installing **command line tools**

```bash
npm install -g <package_name>
```

## Local

- Install locally when you want to depend on a package from your own module
- Default `npm install` behaviour

### Unscoped package

- Are always public which means they can be searched for, downloaded, and installed by _anyone_

```shell
npm install <package_name>
```

- Command will create the `node_modules` directory in your current directory (if one does not yet exist) and will download the package to that directory

> If no `package.json` file in local directory, latest version of the package is installed.
>
> If a `package.json` is present, npm installs the _latest version_ that satisfies the semver rule declared in `package.json`

### Publicly scoped packages

- Scoped public packages can be downloaded and installed by _anyone_, as long as the scope name is referenced during installation

```bash
npm install @scope/package-name
```

### Private package

- Private packages can only be downloaded and installed by those who have been granted read access to the package
- Since private packages are always scoped, reference the scope name during installation

```bash
npm install @scope/private-package-name
```

### Testing package installation

- To confirm `npm install` has worked, in the module directory check that a `node_modules` directory exists and that it contains a directory for the package(s) you installed

```bash
ls node_modules
```

### Installed package version

- if there is a `package.json` file in the directory in which `npm install` is run, npm installs the _latest_ version of the package that satisfies the semantic versioning rule declared in `package.json`
- If there is no `package.json` file, the latest version is installed

### Installing a package with dist-tags

- Similar to `npm publish`, `npm install <package-name>` will use the `latest` tag by default
- To override, use `npm install <package-name>@<tag>`

```bash
npm install example-package@beta
```
