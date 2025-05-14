- Use the `key` prop to specify a unique key for each item
- Key is used to identify which item to update when you want to update an item

- React uses list rendering to dynamically create UI elements based on arrays. This is commonly done with the `.map()` method.

## Role of `key` Prop

- The `key` prop is a **special attribute** used by React to identify which items have changed, been added, or removed.
- Keys help **optimize re-rendering** by allowing React to maintain element identity between renders.

### Key requirements

- **Uniqueness**: Keys must be **unique among siblings**.
- **Stability**: Use a **stable identifier** (like an ID from data) rather than the array index if the list can change (e.g. items added/removed/reordered).
- Using `index` as a key is acceptable **only when**:
  - The list is static.
  - Items do not have unique IDs.
  - Order and content will never change.

## Common Pitfalls

- **Using array index as key in dynamic lists** can cause:
  - Unexpected component state retention.
  - Inefficient DOM updates.
- **Missing keys** will cause a React warning and inefficient diffing.

## Nested Lists

- Each level of a nested list must have its **own unique keys**.

## Key best practices

- Prefer database IDs or unique strings.
- Avoid relying on values that may change over time.
