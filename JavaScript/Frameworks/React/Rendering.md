- React follows a declarative approach to rendering components
	- Developers must specify what a component should look like and React takes care of rendering the component to the screen 
- Process of requesting and serving UI:
	1. Triggering a render
	2. Rendering a component
	3. Committing to the DOM

## VDOM
- A lightweight in-memory representation of the DOM
- Used to optimize rendering of components in a React application

## Trigger a render

Two reasons a component will render:
1. It’s the components *initial* render
2. The component’s (or an ancestor) has had their state *updated*

### Initial render

- 
