---
title: Basics
date created: Thursday, May 8th 2025, 9:17:59 am
date modified: Thursday, May 8th 2025, 1:35:38 pm
---

# Basics

- Components are the building blocks of React applications
- Splits UI into independent, reusable pieces
  - Each piece can be in isolation

## Element vs Component

- **Component** is the declaration of a component
  - Is only declared once but can be used multiple times as a **React element** in JSX

```jsx
const App = () => {
  return <p>Hello React</p>;
};
```

- The above code is a [function component](General%20-%20Types%20of%20React%20Components.md#React%20Fuction%20Components) but it can be [any other kind of React component](General%20-%20Types%20of%20React%20Components.md)
- Function components are declared as JS functions and return React's JSX
- when used, becomes an instance of the component and lives in the React's component tree
- **React element** is when you are rendering a component within another component with the use of angle brackets

```jsx {8-9}
const Greeting = ({ text }) => {
  return <p>{text}</p>;
};

const App = () => {
  return (
    <>
      <Greeting text="Hello Instance 1 of Greeting" />
      <Greeting text="Hello Instance 2 of Greeting" />
    </>
  );
};
```

## React elements

- When a React component gets called or rendered, React calls `React.createElement()` method internally

```js
const App = () => {
  return <p>Hello React</p>;
};

console.log(App());

// {
//   $$typeof: Symbol(react.element)
//   "type": "p",
//   "key": null,
//   "ref": null,
//   "props": {
//     "children": "Hello React"
//   },
//   "_owner": null,
//   "_store": {}
// }
```

- While the type represents the **actual HTML element**, props are all HTML attributes (plus the inner content (children)), which are passed to this HTML element
- React treats children as pseudo HTML attributes whereas children represents everything that's rendered between the HTML tag

```js {2, 14}
const App = () => {
  return <p className="danger">Hello React</p>;
};

console.log(App());

//
//   $$typeof: Symbol(react.element)
//   "type": "p",
//   "key": null,
//   "ref": null,
//   "props": {
//     "children": "Hello React",
//     "className": "danger"
//   },
//   "_owner": null,
//   "_store": {}
// }
```

- React essentially translates all HTML attributes to React props \*in addition\_ to adding inner content as `children` property
- `createElement` can, in theory, be used as a replacement for the returned JSX
  - Takes the props, type, and children as arguments
  - Give `p` as the first argument, the `props` as an object with the `className` as second argument and `children` as the third

```jsx add={4-8} del={2}
const App = () => {
  return <p className="danger">Hello React</p>;

  return React.createElement("p", { className: "danger" }, "Hello React");
};
```

- `children` are provided separately as an argument and they can also be passed in the second argument

```jsx {6}
const App = () => {
  return React.createElement("p", {
    className: "danger",
    children: "Hello React",
  });
};
```

- As default. `children` are used as a third argument

```jsx {14, 18-19, 22, 25-28, 34, 37-40, 44}
const App = () => {
  return (
    <div className="container">
      <p className="danger">Hello React</p>
      <p className="info">You rock, React!</p>
    </div>
  );
};

console.log(App());

// {
//   $$typeof: Symbol(react.element)
//   "type": "div",
//   "key": null,
//   "ref": null,
//   "props": {
//     "className": "container",
//     "children": [
//       {
//         $$typeof: Symbol(react.element)
//         "type": "p",
//         "key": null,
//         "ref": null,
//         "props": {
//           "className": "danger",
//           "children": "Hello React"
//         },
//         "_owner": null,
//         "_store": {}
//       },
//       {
//         $$typeof: Symbol(react.element)
//         "type": "p",
//         "key": null,
//         "ref": null,
//         "props": {
//           className: "info",
//           children: "You rock, React!"
//         },
//         "_owner": null,
//         "_store": {}
//       }
//     ]
//   },
//   "_owner": null,
//   "_store": {}
// }
```

// continue here : https://www.robinwieruch.de/react-element-component/
