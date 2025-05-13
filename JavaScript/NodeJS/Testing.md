- the process of verifying that what we create is doing what we expect it to do
- created to prevent bugs and improve code quality
- most common methods are:
  - unit testing
  - end-to-end (e2e)
- Things to test in a function include:

  - valid inputs
  - edge cases
  - invalid inputs
  - expected outputs

- **Test Pyramid:** Unit tests (base), integration tests (middle), E2E tests (top).
- **Red-Green-Refactor:** TDD practice: fail → pass → clean.
- **Continuous Integration (CI):** Automate running tests on commits.
- **Code coverage isn't everything:** 100% coverage doesn't guarantee bug-free code.

## Unit testing

- Tests individual functions or components **in isolation.**
- Ensures logic correctness at the smallest testable part of an app.
- Fast and cheap to run.
- Key concepts:
  - **Arrange-Act-Assert (AAA) pattern**: setup, execute, verify.
  - **Mocking**: simulate functions, APIs, or modules (e.g., `jest.mock()`).
  - **Spies**: track function calls and arguments.
  - **Test coverage**: measure % of code executed during tests.
  - **Snapshot testing**: useful for React components to detect UI changes.

**Best practices**

- Test one thing per test.
- Avoid external dependencies (network, DBs).
- Keep tests deterministic (same result every run).
- Use descriptive test names.
- Run tests as part of CI/CD pipeline.

**Popular frameworks:**

- **Jest** – most popular, especially for React.
- **Mocha + Chai** – flexible with custom assertion libraries.
- **Vitest** – fast alternative, works well with Vite.

## E2E testing

- Simulates real user interactions from start to finish.
  - Validate the full flow of an app, ensuring that systems integrate and the app works as expected form the users perspective
- Tests the entire app: frontend, backend, databases, APIs, etc.
- Slower but critical for user journey validation.
- Key concepts:
  - **Selectors**: Use `data-testid` or accessible labels.
  - **Setup/teardown**: Manage test state and DB fixtures.
  - **CI integration**: Ensure tests run in pipelines (e.g., GitHub Actions).
  - **Screenshots/videos**: Useful for debugging failures.
- **Flaky tests** are tests that pass or fail randomly.
  - Fix it by using better selectors, managing timing, or improving app stability

**Best Practices:**

- Don't over-test: focus on critical paths (login, checkout, etc.).
- Keep E2E tests independent and stateless.
- Use realistic test data.
- Avoid flaky tests (e.g., through stable selectors and wait strategies).

**Popular Tools:**

- **Cypress** – modern, fast, great DX.
- **Playwright** – supports multiple browsers, powerful.
- **Selenium** – older but still used in enterprise.

## `node:test`

More info: [official docs](https://nodejs.org/en/learn/test-runner/using-test-runner)

- built-in module in Node.js that provides a simple, asynchronous test runner
- designed to make writing tests as straightforward as writing any other code

**Key Features**

- Simplicity: Easy to use and understand.
- Asynchronous Support: Handles asynchronous code gracefully.
- Subtests: Allows for organizing tests into hierarchical structures.
- Hooks: Provides beforeEach and afterEach hooks for setup and teardown.
