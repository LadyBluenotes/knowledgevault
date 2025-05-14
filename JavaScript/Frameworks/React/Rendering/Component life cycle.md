- React components go through **three lifecycle phases**:
  1. **Mounting** – Inserting elements into the DOM
  2. **Updating** – Updating elements already in the DOM
  3. **Unmounting** – Removing elements from the DOM
- Lifecycle methods are easier to manage with **class components** by extending `React.Component`.
- With the advent of **hooks (React 16.8+)**, similar capabilities are now available in **functional components**.

  - Not recommended to use lifecycle methods manually
    - Use [useEffect](Hooks.md#useEffect)

- **React is not deprecating class components**, so continue using them if comfortable.
- Hooks simplify React development for many use cases, but **understanding both paradigms** provides maximum flexibility.
- Understanding the lifecycle is key to mastering DOM manipulation, performance tuning, and side-effect handling.

![](react-lifecycle-1536x625.avif)

## Lifecycle Phases Overview

React components go through three main lifecycle phases:
![](react-lifecycle-1536x625.avif)

### A. Mounting

Occurs when a component is being inserted into the DOM.

Key methods:

- `constructor(props)`
- `static getDerivedStateFromProps(props, state)`
- `render()`
- `componentDidMount()`

### B. Updating

Occurs when a component is re-rendered due to changes in props or state.

Key methods:

- `static getDerivedStateFromProps(props, state)`
- `shouldComponentUpdate(nextProps, nextState)`
- `render()`
- `getSnapshotBeforeUpdate(prevProps, prevState)`
- `componentDidUpdate(prevProps, prevState, snapshot)`

### C. Unmounting

Occurs when a component is removed from the DOM.

Key method:

- `componentWillUnmount()`

## Detailed Explanation of Lifecycle Methods

### constructor(props)

Used for initializing state and binding methods. Avoid side effects; don’t call `setState()` here.

```jsx
constructor(props) {
  super(props);
  this.state = { count: 0 };
}
```

### static getDerivedStateFromProps(props, state)

Called before every render (on both mounting and updating). Used to update state based on props. Must return an object to update state, or `null` to do nothing.

```jsx
static getDerivedStateFromProps(nextProps, prevState) {
  if (nextProps.value !== prevState.value) {
    return { value: nextProps.value };
  }
  return null;
}
```

### render()

A required method that returns JSX or `null`. It must be pure—shouldn’t modify state or interact with the DOM.

```jsx
render() {
  return <div>{this.state.count}</div>;
}
```

### componentDidMount()

Called once after the initial render. Ideal for side effects like data fetching, subscriptions, or setting up timers.

```jsx
componentDidMount() {
  this.fetchData();
}
```

### shouldComponentUpdate(nextProps, nextState)

Determines whether the component should re-render. Useful for performance optimization. Defaults to `true`.

```jsx
shouldComponentUpdate(nextProps, nextState) {
  return nextState.count !== this.state.count;
}
```

### getSnapshotBeforeUpdate(prevProps, prevState)

Called right before the DOM is updated. Allows capturing information (e.g., scroll position) before changes are made.

```jsx
getSnapshotBeforeUpdate(prevProps, prevState) {
  return window.scrollY;
}
```

### componentDidUpdate(prevProps, prevState, snapshot)

Called after updates are flushed to the DOM. Safe for working with the DOM, network requests, or comparing previous and current props/state.

```jsx
componentDidUpdate(prevProps, prevState, snapshot) {
  if (this.props.id !== prevProps.id) {
    this.fetchNewData();
  }
}
```

### componentWillUnmount()

Cleanup method called before a component is removed from the DOM. Used to cancel timers, remove listeners, or abort requests.

```jsx
componentWillUnmount() {
  clearInterval(this.timerID);
}
```

## Lifecycle Equivalents in Functional Components with Hooks

With React 16.8+, hooks offer a functional approach to managing lifecycle behavior.

| Class Component Method     | Equivalent in Functional Component                                 |
| -------------------------- | ------------------------------------------------------------------ |
| `componentDidMount`        | `useEffect(() => { ... }, [])`                                     |
| `componentDidUpdate`       | `useEffect(() => { ... }, [deps])`                                 |
| `componentWillUnmount`     | `useEffect(() => { return () => {...} }, [])`                      |
| `getDerivedStateFromProps` | Derived logic using props inside `useEffect` or manually in render |
| `shouldComponentUpdate`    | `React.memo()` or `useMemo()` / `useCallback()`                    |

## Best Practices

- Use `componentDidMount` and `useEffect` for side effects such as API calls.
- Always clean up listeners or timers in `componentWillUnmount` or the cleanup function in `useEffect`.
- Avoid performing side effects in `render()`.
- Optimize performance using `shouldComponentUpdate`, `React.PureComponent`, or `React.memo()`.
- Prefer functional components with hooks for new codebases.
