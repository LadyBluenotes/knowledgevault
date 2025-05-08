- Build tool
  - Aims for faster / leaner development experience for modern web projects
- Consists of 2 parts:
  - Dev server that provides feature enhancements over native ES modules
  - Build command that bundles your code with [[Rollup]], pre-configured to output optimized static assets for production
- Is opinionated
- Supports frameworks or integration with other tools through plugins
- Config allows for adaptation for projects, as needed
- Written in Go

## Features
- Automatic CSS code-splitting
	- Only loads CSS needed for part of the application you are using
- Async chunk loading
- Automatic dynamic import polyfill
	- Fixes disparity on modern browsers with ESM dynamic imports and ESM via script tags
- Legacy mode plugin
	- For browsers that do not support native ES modules (internet explorer)
- Faster dependency pre-building
- Monorepo support
- Faster dependency pre-building
	- ESBuild instead of rollup
- CSS Pre-processor support

## How to use

### Templates

- Has [community maintained templates](https://github.com/vitejs/awesome-vite#templates)
- Include other tools and frameworks

```bash
npx degit user/project#main my-project
cd my-project

npm install
npm run dev
```

### Manual installation

**CLI**

```bash
npm install -D vite
pnpm add -D vite
```

- Once an `index.html` page is created, you can run the appropriate CLI command in your terminal

```bash
npx vite
pnpm vite
```

## Project structure

- `index.html` should _not_ be put inside `public`
  - Is a server during development and `index.html` is the entry point for the application
  - Vite treats `index.html` as source code and part of the module graph
    - Resolves `<script type="module" src="...">` that references JS code
- Inline `<script type="module">` and CSS referenced via `<link href>` also enjoy Vite-specific features
- URLs inside `index.html` are automatically rebased so there is no need for special `%PUBLIC_URL%` placeholders

## How it works
1. Starts server
2. Takes dependencies that do not change often and bundles them using [[ESBuild]]
3. Uses route-based code splitting to figure out what parts of the code need to be loaded
4. Delivers code via native ES module support in modern browsers