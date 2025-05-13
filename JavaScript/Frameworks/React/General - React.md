---
title: React
date created: Tuesday, April 22nd 2025, 10:52:51 am
date modified: Tuesday, April 22nd 2025, 11:28:48 am
---

# React

## HTML & DOM

- DOM object representation of HTML elements - Acts as the bridge between code and UI - Tree-like structure with parent-child relationships - DOM methods and JS to listen for events and manipulate the dom (adding, selecting, updating, deleting) - DOM manipulation allows for targeting specific elements as well as changing style and content
  -HTML represents initial page content
- DOM represents _updated_ page content
  - Changed via JS
  - With vanilla JS, it's powerful but verbose to use
  - Easier to show **what you want to show** and **how** to update the DOM
- Imperative vs declarative programming
  - Imperative: **how** user interface should be updated
    - Eg. recipe for pizza
  - Need to be aware of the process
  - Declarative: declare **what** they want to show
    - Faster for development process
    - Don't have to write DOM methods
    - Eg. ordering pizza
  - Unconcerned with the process

## General

- Declarative library
- `react` - core React library
- `react-dom` - DOM-specific methods that enable use of React with DOM
- Uses JSX
  - Requires 3 things different than HTML
    - Returns a single root element in a component
  - Need to be wrapped in a single parent tag
    - Close all tags
    - camelCase most things
  - Need a JSX compiler to transform JSX into regular JS
    - Common - Babel
- The compiler with react helps cut down on repetitive code
  - React contains reusable snippets of code that perform tasks on your behalf (eg. updating UI)
- Server and client components require a framework

### Babel

- Used to convert ECMAScript 2015+ code into a backwards compatible version of JS in current or older browser environments
- It can:
  - Transform syntax
  - Polyfill features that are missing in your target environment
    - Provide modern functionality on older browsers that do not natively support it
  - Source code transformations
  - etc.
- Import into HTML file using script tag with the type attribute `type="text/jsx"`

## JavaScript

- JS topics related to React
  - Functions & arrow functions
  - Objects
  - Arrays and array methods
  - Destructuring
  - Template literals
  - Ternary operators
  - ES Modules and Import / Export Syntax

## Core Concepts

### Components

- Self-contained, reusable snippets of code, like LEGO bricks
- Can be used and combined with other components to form a larger structure
  - Lets updating of the specific component vs the entire page
- Modularity allows code to be more maintainable as it grows
  - Lets you add, update, or delete components without touching the rest of the application
- Component is a function that returns UI elements (written using JSX)
  - Should be capitalized to distinguish from HTML and JS
  - Require angle brackets (`<>`)
- Nest components inside one another similar to HTML
  - Creates **component trees**

### Props

- Props are what you pass React components
  - Contain pieces of info that change the component's behaviour or what is shown when rendered on the screen
- Can be passed from parent to child
- Data flows down a component tree (**one-way data flow**)
- includes [state](#state)
- Props return an object where the prop name (eg. `title`) is the key and what was passed to the component (eg. `Welcome to my site`) is the value
  - Can be _destructured_ to explicitly name the props within your function

```jsx
function Header({ title }) {
  console.log(title); // "React"
  return <h1>Develop. Preview. Ship</h1>;
}
```

- To use variables within JSX, you must add curly braces (`<h1>{title}</h1>`)
  - Curly braces allow **any** JS expression (that evaluates to a single value) inside curly braces:
    - Examples
  - Object property with dot notation (`<h1>{props.title}</h1>`)
  - Template literal (`<h1>{`Cool ${props.title}`}</h1>`)
  - Ternary operators (`<h1>{title ? title : 'Default Title'}</h1>`)
  - The returned value of a function

```jsx
function createTitle(title) {
  if (title) {
    return title;
  } else {
    return "Default title";
  }
}

function Header({ title }) {
  return <h1>{createTitle(title)}</h1>;
}
```

- Can use array methods to manipulate data and generate UI elements that are identical in style but hold different pieces of info
  - React requies keys to identify items in an array to know which element to update in the DOM

```jsx
<ul>
  {names.map((name) => (
    <li key={name}>{name}</li>
  ))}
</ul>
```

### State

- State is any information in UI that changes over time
  - Usually triggered by user interaction
    -Eg. store and increment a number when a button is pressed
- Adds interactivity and event handlers
- Event names are cameCased (eg. `onChange`, `onSubmit`)
- Can define a function to "handle" events when triggered that is then called when the event is triggered

```jsx
function handleClick() {
  console.log("increment like count");
}

<button onClick={handleClick}>Like</button>;
```

- State is initiated and stored _within_ a component
- Can pass state info to children, but logic for updating should be kept within the component where the state was intially created

#### Hooks

- Hooks allow you to add additional logic (such as `state` to your components)
- `useState`
  - used to show/ store a value
  - returns an array
    - First item in the array is the **value**, which can be named anything
    - Second item is used to **update** the value
    - Can add an initial value to the state by putting something in the parenthesis
    - eg. `const [value, setValue] = useState(0)`

```jsx
const [likes, setLikes] = React.useState(0);

function handleClick() {
  setLikes(likes + 1);
}

return (
  <div>
    {/* ... */}
    <button onClick={handleClick}>Likes ({likes})</button>
  </div>
);
```

#### Managing State

- Shouldn't contain redundant or duplicated info
- To share state between two components, make sure it is in the closest common parent and pass it down via props (called **lifting state up**)
- React, by default, preserves the parts of the tree that "match up" with previously rendered tree
  - Can force a component to reset state by passing it a different key
    - Says that a component needs to be re-created from scratch with new data
- For state that spreads across many event handlers, you can use `useReducer` - event handlers become concise because they only specify the user "actions" - At the bottom of the file, reducer function specifies how the state should update in response to each action -`useContext` lets parent components make some info available to component tree below, no mater how deep, without explicitly using props
- Reducers let you consolidate component state update logic while context lets you pass info deep down to other components
  - Can both be combined to manage state of a complex screen
  - Parent with complex state, manages it with a reducer while other components deep within the tree can read it via context
    - Can also dispatch actions to update state
