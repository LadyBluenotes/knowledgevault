## useState

- declares a state variable

```jsx
const [something, setSomething] = useState("Hello World");
```

### Initial state

- is **ignored** after the initial render
  - is treated as an _initializer function_ and should be pure, take no arguments, and return a value of **any type**
- can be allocated _within_ `useState`

### Returns

Returns an array with exactly two values:

1. the current state - during first render, will match the initial state passed
2. the `set` function that lets you update to a different value and trigger a re-render

JavaScript array destructuring is used to access both items with a shorthand expression and also allows for the naming of the variables

### Setters

- lets state be updated to a different value and trigger a re-render
  - State can be passed directly or a function that calculates it from previous state
- are executed asynchronously by nature so it is important to make sure state changes are on current states and not stale ones
- the next state value that you want can be of any type
  - If a function is passes ad the next state, it will be treated as an _updater function_
    - **must be pure** and should only take the **pending state** as its only argument and it should _return the next state_
    - will be put in a queue and re-render after your component
      - During the next render, it will calculate the next state and apply all queued updaters to the previous state
- does _not_ have a return value

### Setter caveats

- Only updates the state variable for the _next_ render
  - If state is read after calling the setter, old value will be called
- If the new value is identical to the _current_ state (as determined by `Object.is`), a re-render will be skipped for the component _and_ the children
- Since React batches state updates, screen is updated **after** all event handlers have run and called their setter functions
  - Prevents multiple re-renders during a singular event
  - To render a screen earlier, `flushSync` can be used
- Has a stable identity, so will often be omitted from useEffect dependencies but using it will _not_ cause the effect to fire
  - If linter lets you omit a dependency without errors, it is safe to do so
- In Strict mode, updater function will be called twice to find accidental impurities
  - Development-only behaviour and does not affect production
  - If initializer function is pure (as it should be), this should not affect behaviour

### useState Caveats

- A hook and therefore must be called at the **top level** of your component or custom hooks
  - Cannot be called inside loops or conditions
    - If needed, extract a new component and move the state into it

## useEffect

- lets you synchronize a component with an external system

```js
useEffect(setup, dependencies?)
```

- every time a _variable_ changes in this case, the useEffect will run
- this means you can choose when it runs:
  - every time (no argument)
    - Note: An infinite loop can happen as this runs after state has changed and that means that if an effect hook triggers a state change, it will run again and again
  - only on mount and unmount (`[]` argument)
  - only when certain variables change (eg. `[state]` argument)

### Parameters

`setup` - function with useEffect’s logic

- May also optionally return a `cleanup` function
- When component is added to the DOM, React will run setup function
- After ever re-render with changed dependencies, React will first run the cleanup function (if provided) with the old values, then run your setup with the _new_ values
- After a component is removed form the DOM, React will run the cleanup function

`dependencies` (optional) - list of all the _reactive_ values inside of the `setup` code

- Include props, state, and all variables and functions declared directly _inside_ the component body
- If linter is configured for react, it will verify that every reactive value is correctly specified as a dependency
- List of dependencies must have a constant number of items and be written inline like `[dep1, dep2, dep3, ...]`

### useEffect Caveats

- Cannot be called inside loops or conditions and must be called at the **top level** of the component
- If synchronization is not needed with an external system, Effect is probably not needed
- When Strict Mode is on, React will run **one extra development-only** setup and cleanup cycle _before_ the first real setup
  - Stress-test to ensure cleanup logic mirrors setup logic and that it stops or undoes what the setup is doing
  - If a problem is caused, a cleanup function is needed
- If a dependency is defined inside the component, ther is a risk that they will cause the Effect to re-run _more times than is needed_
  - To fix, remove any unnecessary object or function dependencies
  - Extract state updates and non-reactive logic _outside_ your effect
- If an effect isn’t caused by an interaction (eg. a click), React will generally let the browser paint the updated screen first before running the effect
  - If the effect is doing something visual and the delay is noticeable (eg. a tooltip flickering), `useEffect` can be replaced by `useLayoutEffect`
- If effect is caused by an interaction, React may **run your effect before the browser paints the updated screen**
  - Ensures result of the effect can be observed by the event system
  - Usually works as expected but if the work needs to be delayed until **after paint** (eg. an alert), you can use `setTimeout`
  - If repainting has to be blocked, `useEffect` may need to be replaced with `useLayoutEffect`
- Only run on the client

## useMemo

- Lets the results of a calculation be cached between re-renders

```js
const cachedValue = useMemo(calculateValue, dependencies);
```

- Must be used at top-level of component to cache calculations between re-renders

### Parameters

`calculateValue` - function that calculates the value that you want to cache

- Should be pure, take no arguments, and return a value of _any type_
- Will be called during initial render and on next renders, same value will be returned again if `dependencies` have not changed since the previous render otherwise will call `calculateValue`then return its result and store it to be reused later

`dependencies` - list all reactive values referenced inside of the `calculateValue` code

- Reactive values include props, state, and all variables and functions declared directly inside your component body
- Linters configured to React will verify that reactive values are correctly specified as a dependency
- Must be written inline like `[dep1, dep2, dep3, ...]`
- Will compare each dependency with the `Object.is` comparison

### Returns

- On initial render, returns the result of calling `calculateValue` with no arguments
- During next render, will either return a stored value form the last render if dependencies ahve not changed, or call `calculateValue` again and return the result

### Caveats

- Can only be called at top level of a component or custom hooks
- Cannot be called inside loops or conditions
- In Strict mode, updater function will be called twice to find accidental impurities
  - Development-only behaviour and does not affect production
  - If initializer function is pure (as it should be), this should not affect behaviour
- Cached values will not be thrown away unless there is a reason to do that
  - examples:
    - In development, ill be thrown away if file of component is edited
    - In development and prod, will be thrown away if component suspends during the initial mount
