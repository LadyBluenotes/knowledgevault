> Status quo for modern React applications

- Are essentially just JavaScript functions being React components which return JSX (React’s template syntax)
- React components can be rendered inside a function component
  - Essentially a child component
  - Can decide where to render a component and how

```jsx {4}
import React from "react";

function App() {
  return <Headline />;
}

function Headline() {
  const greeting = "Hello Function Component!";

  return <h1>{greeting}</h1>;
}

export default App;
```

## Props

- Props are used to pass information from component to component
- Always passed _down_ the component tree

```jsx {4, 6, 9-10}
import React from "react";

function App() {
  const greeting = "Hello Function Component!";

  return <Headline value={greeting} />;
}

function Headline(props) {
  return <h1>{props.value}</h1>;
}

export default App;
```

- Are the React function component’s parameters
- Components can stay generic and from the outside it can be decided what it should render or how it should behave
- Props can be passed as HTML attributes to a component which then makes it available as an argument in the function signature

- Props always come from an **object** which means JS object desctructing is possible

```jsx {9-10}
import React from "react";

function App() {
  const greeting = "Hello Function Component!";

  return <Headline value={greeting} />;
}

function Headline({ value }) {
  return <h1>{value}</h1>;
}

export default App;
```

> If trying to access props from the function signature like `function Headline(value1,value2) {...}` you may see `props undefined` since props are always accessible as the _first argument_ and can be destructured from there: `function Headline({ value1, value2 }) {...}`

## Arrow function component

- ES6 introduced new concepts to JS, such as functions that can be expressed as lambda (arrow function)
  - Why sometimes React function components are called **Arrow Function Components** or **Arrow Function Expression components** (rarely Lambda Function Component)
- Do not change how props are used or accessed

```jsx {3, 9}
import React from "react";

const App = () => {
  const greeting = "Hello Function Component!";

  return <Headline value={greeting} />;
};

const Headline = ({ value }) => {
  return <h1>{value}</h1>;
};

export default App;
```

- You can simplify arrow functions to be more lightweight and concise if they only return the output of the component without doing something else in between

```jsx {9-10}
import React from "react";

const App = () => {
  const greeting = "Hello Function Component!";

  return <Headline value={greeting} />;
};

const Headline = ({ value }) => <h1>{value}</h1>;

export default App;
```

> A “React Component Arrow Function Unexpected Token” error may mean that you are using ES5

## Stateless Function component

- All the components above can be called **stateless function components** since they just receive inputs as props and return an output as JSX: `(props) => JSX`
  - Called this because they are stateless and expressed by a function
- The input, only if available in the form of props, shapes the rendered outputs
- These kinds of components _do not_ manage state and _do not_ have side-effects

## State

- React hooks made it possible to use state (and side-effects)
- Allows for a level of interaction with the application
- uses the [`useState`]([[Hooks#useState]]) hook

```jsx {8-10, 15-19}
import React, { useState } from "react";

const App = () => {
  return <Headline />;
};

const Headline = () => {
  const [greeting, setGreeting] = useState("Hello Function Component!");

  return (
    <div>
      <h1>{greeting}</h1>
      <input
        type="text"
        value={greeting}
        onChange={(event) => setGreeting(event.target.value)}
      />
    </div>
  );
};

export default App;
```

- Event handlers in the input field allow for callback functions when the input field receives its value
  - Argument of the callback function receives a synthetic React event, which holds the current value of the input field and this value is used to set the new state for the function component with an inline arrow function

## Event handler

- in addition to `onChange`, other event handlers can be used with form elements:
  - `onClick`
  - `onMouseDown`
  - `onBlur`
- Can extract arrow functions from inline event handling to a standalone function that can be used inside the component

```jsx {17} add={12}
import React, { useState } from "react";

const App = () => {
  return <Headline />;
};

const Headline = () => {
  const [greeting, setGreeting] = useState("Hello Function Component!");

  const handleChange = (event) => setGreeting(event.target.value);

  return (
    <div>
      <h1>{greeting}</h1>
      <input type="text" value={greeting} onChange={handleChange} />
    </div>
  );
};

export default App;
```

- This way of defining functions within a component is similar to how they are defined within [React Class Components]([[Overview of the Types of React Components#React Class Components (not recommended)]])

## Callback function

- it is possible to pass a function to a component prop

```jsx {4-6, 8, 11, 15, 18}
import React, { useState } from "react";

const App = () => {
  const [greeting, setGreeting] = useState("Hello Function Component!");

  const handleChange = (event) => setGreeting(event.target.value);

  return <Headline headline={greeting} onChangeHeadline={handleChange} />;
};

const Headline = ({ headline, onChangeHeadline }) => (
  <div>
    <h1>{headline}</h1>
    <input type="text" value={headline} onChange={onChangeHeadline} />
  </div>
);

export default App;
```

- changes can be made in between parent and child components

```jsx {12, 13-15} add={22, 24-29}
import React, { useState } from "react";

const App = () => {
  const [greeting, setGreeting] = useState("Hello Function Component!");

  const handleChange = (event) => setGreeting(event.target.value);

  return (
    <div>
      <Headline headline={greeting} />
      <Input value={greeting} onChangeInput={handleChange}>
        Set Greeting:
      </Input>
    </div>
  );
};

const Headline = ({ headline }) => <h1>{headline}</h1>;

const Input = ({ value, onChangeInput, children }) => (
  <label>
    {children}
    <input type="text" value={value} onChange={onChangeInput} />
  </label>
);

export default App;
```

### Overriding a components function

- To override a passed prop to a component, give it a default value

```jsx {12}
import React from "react";

const App = () => {
  const sayHello = () => console.log("Hello");

  return <Button handleClick={sayHello} />;
};

const Button = ({ handleClick }) => {
  const sayDefault = () => console.log("Default");

  const onClick = handleClick || sayDefault;

  return (
    <button type="button" onClick={onClick}>
      Button
    </button>
  );
};

export default App;
```

- Default value can also be assigned in the function signature for destructuring, as well

```jsx {9}
import React from "react";

const App = () => {
  const sayHello = () => console.log("Hello");

  return <Button handleClick={sayHello} />;
};

const Button = ({ handleClick = () => console.log("Default") }) => (
  <button type="button" onClick={handleClick}>
    Button
  </button>
);

export default App;
```

### Async function

- Functions can be synchronously executed or not

```jsx {5}
import React from "react";

const App = () => {
  const sayHello = () => setTimeout(() => console.log("Hello"), 1000);

  return <Button handleClick={sayHello} />;
};

const Button = ({ handleClick }) => (
  <button type="button" onClick={handleClick}>
    Button
  </button>
);

export default App;
```

- Component will also rerender asynchronously in case props or state have changed

```jsx
import React, { useState } from "react";

const App = () => {
  const [count, setCount] = useState(0);

  const handleIncrement = () =>
    setTimeout(() => setCount((currentCount) => currentCount + 1), 1000);

  const handleDecrement = () =>
    setTimeout(() => setCount((currentCount) => currentCount - 1), 1000);

  return (
    <div>
      <h1>{count}</h1>
      <Button handleClick={handleIncrement}>Increment</Button>
      <Button handleClick={handleDecrement}>Decrement</Button>
    </div>
  );
};

const Button = ({ handleClick, children }) => (
  <button type="button" onClick={handleClick}>
    {children}
  </button>
);

export default App;
```

## Component Lifecycles

- contains no constructor similar to what is used in [React Class Components]([[Overview of the Types of React Components#React Class Components (not recommended)]]) to allocate initial state
- functions can be setup on top of initial states in the `useState` hook

```jsx {6-7, 9-10}
import React, { useState } from "react";

const App = () => {
  const [count, setCount] = useState(0);

  const handleIncrement = () => setCount((currentCount) => currentCount + 1);

  const handleDecrement = () => setCount((currentCount) => currentCount - 1);

  return (
    <div>
      <h1>{count}</h1>
      <button type="button" onClick={handleIncrement}>
        Increment
      </button>
      <button type="button" onClick={handleDecrement}>
        Decrement
      </button>
    </div>
  );
};

export default App;
```

### Mount

- There is a mounting lifecycle for React components when they are rendered _the first time_
- To execute something when a function component **did mount**, the [[Hooks#useEffect]] hook can be used

```jsx {12}
import React, { useState, useEffect } from "react";

const App = () => {
  const [count, setCount] = useState(0);

  const handleIncrement = () => setCount((currentCount) => currentCount + 1);

  const handleDecrement = () => setCount((currentCount) => currentCount - 1);

  useEffect(() => setCount((currentCount) => currentCount + 1), []);

  return (
    <div>
      <h1>{count}</h1>
      <button type="button" onClick={handleIncrement}>
        Increment
      </button>
      <button type="button" onClick={handleDecrement}>
        Decrement
      </button>
    </div>
  );
};

export default App;
```

- This example will have count `0` then `1` shortly displayed after one another
  - First render of the component shows the count `0` from the initial state
  - After component is mounted, useEffect will run to set a new state of 1

### Update

- Every time incoming props or state of the component change, the component triggers a _rerender_ to display the latest status quo which is often derived form the props and state
  - A render executes _everything_ within the Function Component’s body
- To act upon a rerender, you can use the useEffect hook again to do something after the component updates

```jsx {4,5, 13}
import React, { useState, useEffect } from "react";

const App = () => {
  const initialCount = +localStorage.getItem("storageCount") || 0;
  const [count, setCount] = useState(initialCount);

  const handleIncrement = () => setCount((currentCount) => currentCount + 1);

  const handleDecrement = () => setCount((currentCount) => currentCount - 1);

  useEffect(() => localStorage.setItem("storageCount", count));

  return (
    <div>
      <h1>{count}</h1>
      <button type="button" onClick={handleIncrement}>
        Increment
      </button>
      <button type="button" onClick={handleDecrement}>
        Decrement
      </button>
    </div>
  );
};

export default App;
```

## Pure React function component

- [React class components]([[Overview of the Types of React Components#React Class Components (not recommended)]]) offered the possibility to decide whether a component has to rerender or not
  - Was achieved by using the PureComponent or `shouldComponentUpdate` to avoid performance bottlenecks in React by preventing rerenders

```jsx {4, 17, 29-33}
import React, { useState } from "react";

const App = () => {
  const [greeting, setGreeting] = useState("Hello React!");
  const [count, setCount] = useState(0);

  const handleIncrement = () => setCount((currentCount) => currentCount + 1);

  const handleDecrement = () => setCount((currentCount) => currentCount - 1);

  const handleChange = (event) => setGreeting(event.target.value);

  return (
    <div>
      <input type="text" onChange={handleChange} />
      <Count count={count} />
      <button type="button" onClick={handleIncrement}>
        Increment
      </button>
      <button type="button" onClick={handleDecrement}>
        Decrement
      </button>
    </div>
  );
};

const Count = ({ count }) => {
  console.log("Does it (re)render?");

  return <h1>{count}</h1>;
};

export default App;
```

- In this case, everytime something is typed into the input field, the `App` component updates its state, rerenders, and rerenders the Count component as well
- [useMemo]([[Hooks#useMemo]]) can be used to prevent a rerender when the incoming props of a component _haven’t changed_

```jsx {1} add={29-33}
import React, { useState, memo } from "react";

const App = () => {
  const [greeting, setGreeting] = useState("Hello React!");
  const [count, setCount] = useState(0);

  const handleIncrement = () => setCount((currentCount) => currentCount + 1);

  const handleDecrement = () => setCount((currentCount) => currentCount - 1);

  const handleChange = (event) => setGreeting(event.target.value);

  return (
    <div>
      <input type="text" onChange={handleChange} />
      <Count count={count} />
      <button type="button" onClick={handleIncrement}>
        Increment
      </button>
      <button type="button" onClick={handleDecrement}>
        Decrement
      </button>
    </div>
  );
};

const Count = memo(({ count }) => {
  console.log("Does it (re)render?");

  return <h1>{count}</h1>;
});

export default App;
```

- this means that a component wont update when a user types and only App will rerender

## Import and Export

- Import and export statements can be used when components are separated into their own files

```jsx title="src/components/Headline.js"
import React from "react";

const Headline = (props) => {
  return <h1>{props.value}</h1>;
};

export default Headline;
```

```jsx title="src/components/App.js"
import React from "react";
import Headline from "./Headline.js";

const App = () => {
  const greeting = "Hello Function Component!";

  return <Headline value={greeting} />;
};

export default App;
```

## Ref

- Should only be used in rare cases such as accessing / manipulating the DOM manually (eg. focus element), animations, and integrating third-party DOM libraries (eg. D3)

```jsx {1} add={16, 18, 25}
import React, { useState, useEffect, useRef } from "react";

const App = () => {
  const [greeting, setGreeting] = useState("Hello React!");
  const handleChange = (event) => setGreeting(event.target.value);

  return (
    <div>
      <h1>{greeting}</h1>
      <Input value={greeting} handleChange={handleChange} />
    </div>
  );
};

const Input = ({ value, handleChange }) => {
  const ref = useRef();

  useEffect(() => ref.current.focus(), []);

  return <input type="text" value={value} onChange={handleChange} ref={ref} />;
};

export default App;
```

- Function components cannot be **given** refs. This will be assigned to the *component instance* and not the actual DOM node

```jsx {17, 23}
// wil not work 

import React, { useState, useEffect, useRef } from "react";

const App = () => {
  const [greeting, setGreeting] = useState("Hello React!");

  const handleChange = (event) => setGreeting(event.target.value);

  const ref = useRef();

  useEffect(() => ref.current.focus(), []);

  return (
    <div>
      <h1>{greeting}</h1>
      <Input value={greeting} handleChange={handleChange} ref={ref} />
    </div>
  );
};

const Input = ({ value, handleChange, ref }) => (
  <input type="text" value={value} onChange={handleChange} ref={ref} />
);

export default App;
```

- If a function component needs to be passed a ref (note: it is not recommended) you can use `forwardRef` to forward the ref

```jsx add={7, 27}
// Does work!

import React, {
  useState,
  useEffect,
  useRef,
  forwardRef,
} from 'react';

const App = () => {
  const [greeting, setGreeting] = useState('Hello React!');

  const handleChange = event => setGreeting(event.target.value);

  const ref = useRef();

  useEffect(() => ref.current.focus(), []);

  return (
    <div>
      <h1>{greeting}</h1>
      <Input value={greeting} handleChange={handleChange} ref={ref} />
    </div>
  );
};

const Input = forwardRef(({ value, handleChange }, ref) => (
  <input
    type="text"
    value={value}
    onChange={handleChange}
    ref={ref}
  />
));

export default App;
```

## Proptypes

> [React prop-types](https://github.com/facebook/prop-types) must be installed as it was removed from the React core library. It is recommended to use TypeScript over prop-types.

- Once a component is defined, it can be assigned PropTypes to validate the incoming props of a component

```jsx add={2, 14-16}
import React from 'react';
import PropTypes from 'prop-types';

const App = () => {
  const greeting = 'Hello Function Component!';

  return <Headline value={greeting} />;
};

const Headline = ({ value }) => {
  return <h1>{value}</h1>;
};

Headline.propTypes = {
  value: PropTypes.string.isRequired,
};

export default App;
```

## TypeScript

- It is more recommended to use TypeScript as a type system
- Benefits the developer by creating a more robust codebase
- Only defines incoming props as types
	- Most type inference comes out-of-the-box