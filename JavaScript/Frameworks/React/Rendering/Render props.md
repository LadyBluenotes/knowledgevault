- Props are used to pass data from a parent component to a child component.
- They can hold any type of JavaScript value (objects, arrays, functions, etc.).
- Props are similar to HTML attributes but more flexible.

**Passing Props**:

- In a parent component, you can pass props to a child component by including them in the JSX tag.

**Reading Props**:

- To access props inside a component, destructure them from the function parameter:  
   `function Avatar({ person, size }) { }`

**Default Values for Props**:

- You can specify default values for props using destructuring:  
   `function Avatar({ person, size = 100 }) { }`
- Default values are only used if the prop is `undefined` or missing.
- **Note**: `null` or `0` will **not** trigger the default value.

**Forwarding Props**:

- Use the JSX spread syntax (`{...props}`) to forward all props to child components:  
   `<Avatar {...props} />`
- This is useful for passing down all props without listing them individually but should be used judiciously.

**Passing JSX as Children**:

- Nested JSX components (like `<Card><Avatar /></Card>`) are passed as a special `children` prop.
- The parent component doesn’t need to know the details of the child content.

**Props and Re-rendering**:

- Props are immutable. A component can’t change its own props.
- If props need to change, the parent component must update and pass new props.
- Props are snapshots of data and are recalculated with each render, which means they can change over time.

**Avoiding Common Pitfalls**:

- **Destructuring**: Ensure proper use of `{}` for destructuring props.
- **Spread Syntax**: Avoid overusing the JSX spread syntax, as it can lead to confusion about which props are passed to a component.

**Props in Components with Children**:

- Components like `<Card>{children}</Card>` receive nested JSX content as the `children` prop.
- This pattern is useful for creating reusable wrapper components (e.g., for UI grids, panels).

**Immutability of Props**:

- Props are **read-only** and cannot be changed directly by a component.
- To modify the behavior of a component (e.g., based on user input), **state** should be used instead of changing props.
