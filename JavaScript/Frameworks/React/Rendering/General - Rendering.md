- React follows a declarative approach to rendering components
  - Developers must specify what a component should look like and React takes care of rendering the component to the screen
    - Imperative approach is where developers write code to manually manipulate the DOM to update the UI
- Process of requesting and serving UI:

  1.  Triggering a render - initial update or state update
  2.  Rendering a component - call components to determine UI
  3.  Committing to the DOM - update the DOM

- **React only commits changes** to the DOM when the rendered output differs.
- **Strict Mode** helps detect side effects and non-deterministic behavior.
- **Performance is optimized** by batching updates and only touching DOM when needed.

- Components are written as JS classes or functions that define a render method
  - Render method returns a description of what the component should look like using JSX syntax
  - When a component is rendered, React creates a VDOM representation of the component
    - VDOM is used to optimize rendering of components
  - React compares VDOM representation of component with previous VDOM representation (if it exists)
    - If there are differences between the two VDOMS, React calculates the minimum number of DOM updates needed to bring the actual DOM into line with the new VDOM
  - React updates the actual DOM with the minimum number of DOM updates needed to reflect the changes in the VDOM
    - Process is known as reconciliation and an important aspect of how React works

## VDOM

- A lightweight in-memory representation of the DOM
- Used to optimize rendering of components in a React application

## Step 1: Trigger a render

- Renders happen for two reasons:
  1. **Initial render** – When the app is first loaded.
  2. **Re-render** – When component state or an ancestor’s state updates.
- State updates automatically queue a re-render.
- Updating state (e.g., via `setState` or `useState`) is like a guest changing their order in a restaurant metaphor.
- The initial render is kicked off by `createRoot(...).render(...)`.

## Step 2: Render the components

- React calls the **function component** to generate a virtual representation (JSX) of the UI.
- On **initial render**, React starts with the root component.
- On **re-renders**, React starts with the component whose state changed.
- Rendering is **recursive**:
  - If a component returns child components, React renders those in turn.
  - Continues until all nested components are rendered and a complete tree is built.

### Rendering rules

- Rendering must be **pure**:
  - **Same inputs = same output** (deterministic).
  - **No side effects**: Rendering must not modify external variables or objects.
- React in **Strict Mode** will **invoke component functions twice** (in dev only) to surface impure code or bugs.

## Step 3: Commit phase (DOM update)

- React **applies changes to the DOM**:
  - On **initial render**, DOM nodes are created and appended using `appendChild`.
  - On **re-renders**, React compares new output with the previous and updates only the necessary parts (minimal DOM diffing).
- DOM updates are **selective and efficient**:
  - If a DOM node (like `<input>`) stays in the same place in the JSX, React does not recreate or reset it, preserving user-entered data.

## Browser paint

- After the DOM is updated, the **browser repaints** the screen.
- This browser action is referred to as **“painting”** to distinguish it from React’s rendering.
