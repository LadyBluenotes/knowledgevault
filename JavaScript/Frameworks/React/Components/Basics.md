- Components are the building blocks of React applications
- Splits UI into independent, reusable pieces
  - Each piece can be in isolation

## Element vs Component

- **Component** is the declaration of a component

```jsx
const App = () => {
  return <p>Hello React</p>;
};
```

- The above code is a [function component]([[Overview of the Types of React Components#React Function Components]]) but it can be [any other kind of React component]([[Overview of the Types of React Components]])
- Function components are declared as JS functions and return React’s JSX
