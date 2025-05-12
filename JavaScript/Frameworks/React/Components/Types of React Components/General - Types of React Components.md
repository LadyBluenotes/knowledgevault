## createClass (deprecated)

> Deprecated in version 15.5 (April 2017). Class Components were recommended instead

- Defining components as a factory function to create React Class Components without needed JavaScript class
- Was the standard before ES6 (in 2015), because JS lacked the native class syntax

```jsx
import createClass from "create-react-class";

const CreateClassComponent = createClass({
  getInitialState: function () {
    return {
      text: "",
    };
  },

  handleChangeText: function (event) {
    this.setState({ text: event.target.value });
  },

  render: function () {
    return (
      <div>
        <p>Text: {this.state.text}</p>
        <input
          type="text"
          value={this.state.text}
          onChange={this.handleChangeText}
        />
      </div>
    );
  },
});

export default CreateClassComponent;
```

- above code is a factory method that takes an object that defines methods for a React component

  - `getInitialState()` is used to initialize component’s state
  - `render()` handles displaying output using JSX

- lifecycle methods for side-effects were available
  - to write when `text` value form state to browser’s local storage, can make `componentDidUpdate()` lifecycle method
  - value can also be read from local storage when component receives initial state

```jsx add={10-12} {6}
import createClass from "create-react-class";

const CreateClassComponent = createClass({
  getInitialState: function () {
    return {
      text: localStorage.getItem("text") || "",
    };
  },

  componentDidUpdate: function () {
    localStorage.setItem("text", this.state.text);
  },

  handleChangeText: function (event) {
    this.setState({ text: event.target.value });
  },

  render: function () {
    return (
      <div>
        <p>Text: {this.state.text}</p>
        <input
          type="text"
          value={this.state.text}
          onChange={this.handleChangeText}
        />
      </div>
    );
  },
});

export default CreateClassComponent;
```

- to use need the node package [create-react-class](https://www.npmjs.com/package/create-react-class)

## React Mixins (deprecated)

> Not used anymore, because they came with several [drawbacks](https://legacy.reactjs.org/blog/2016/07/13/mixins-considered-harmful.html) and were only used within `createClass` components

- React’s first pattern for reusable component logic
- made it possible to extract logic from a React component as a standalone object
- When using, all features from the Mixin are introduced to the component

```jsx add={3-8,16}
import createClass from "create-react-class";

const LocalStorageMixin = {
  getInitialState: function () {
    return {
      text: localStorage.getItem("text") || "",
    };
  },

  componentDidUpdate: function () {
    localStorage.setItem("text", this.state.text);
  },
};

const CreateClassWithMixinComponent = createClass({
  mixins: [LocalStorageMixin],
  handleChangeText: function (event) {
    this.setState({ text: event.target.value });
  },

  render: function () {
    return (
      <div>
        <p>Text: {this.state.text}</p>
        <input
          type="text"
          value={this.state.text}
          onChange={this.handleChangeText}
        />
      </div>
    );
  },
});

export default CreateClassWithMixinComponent;
```

- `LocalStorageMixin` encapsulates logic for managing the `text` state within local storage, initializing the `text` in `getInitialState` and updating it in `componentDidUpdate`
  - By adding Mixin to the `mixins` array, component can reuse shared functionality _without_ duplicating code

## React Class Components

> ***Not Recommended***

> Introduced as a way to use JavaScript classes (due to ES6 release in 2015), when JS classes were made available to the language.

> With the release of React hooks in version 16.8 (Feb 2019), function components with hooks became industry standard, rendering React Class Components somewhat obsolete. Class Components and Function Components coexisted since Function Components lacked the ability to manage state and handle side effects without the use of hooks.

- Introduced in version 0.13, released in March 2015
  - Prior to, `createClass` was used to define components

```jsx
import React from "react";

class ClassComponent extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      text: "",
    };

    this.handleChangeText = this.handleChangeText.bind(this);
  }

  handleChangeText(event) {
    this.setState({ text: event.target.value });
  }

  render() {
    return (
      <div>
        <p>Text: {this.state.text}</p>
        <input
          type="text"
          value={this.state.text}
          onChange={this.handleChangeText}
        />
      </div>
    );
  }
}

export default ClassComponent;
```

- React Component written with a JS class comes with methods like the class constructor
  - Primarily used in React to **set initial state** or to **bind methods**
  - Also had the _mandatory_ render method to return JSX as an output
- All internal React Component logic comes from the object-orientated inheritance

  - Never recommended to use inheritance for more than that (use composition over inheritance)

- Alternative syntax for JS classes used in React components allow for autobinding methods through the use of ES6 arrow functions

```jsx {11-12, 15}
import React from "react";

class ClassComponent extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      text: "",
    };

    // not needed if using arrow function for handleChangeText
    // this.handleChangeText = this.handleChangeText.bind(this);
  }

  handleChangeText = (event) => {
    this.setState({ text: event.target.value });
  };

  render() {
    return (
      <div>
        <p>Text: {this.state.text}</p>
        <input
          type="text"
          value={this.state.text}
          onChange={this.handleChangeText}
        />
      </div>
    );
  }
}

export default ClassComponent;
```

- Offer several lifecycle methods for the mounting, updating and unmounting of the component

```jsx {8} add={14-16}
import React from "react";

class ClassComponent extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      text: localStorage.getItem("text") || "",
    };

    this.handleChangeText = this.handleChangeText.bind(this);
  }

  componentDidUpdate() {
    localStorage.setItem("text", this.state.text);
  }

  handleChangeText(event) {
    this.setState({ text: event.target.value });
  }

  render() {
    return (
      <div>
        <p>Text: {this.state.text}</p>
        <input
          type="text"
          value={this.state.text}
          onChange={this.handleChangeText}
        />
      </div>
    );
  }
}

export default ClassComponent;
```

## React Higher-Order Components

> Not recommended anymore
> 
> Is a pattern

- React Higher-Order Components (HOCs) have been a popular advanced React pattern for reusable logic across React components
- HOCs are a component which takes a component as an input and returns he component as an output with extended functionalities

```jsx {3-31, 37, 40-41}
import React from "react";

const withLocalStorage = (storageKey) => (Component) => {
  return class extends React.Component {
    constructor(props) {
      super(props);

      this.state = {
        value: localStorage.getItem(storageKey) || "",
      };
    }

    componentDidUpdate() {
      localStorage.setItem(storageKey, this.state.value);
    }

    onChangeValue = (event) => {
      this.setState({ value: event.target.value });
    };

    render() {
      return (
        <Component
          value={this.state.value}
          onChangeValue={this.onChangeValue}
          {...this.props}
        />
      );
    }
  };
};

class ClassComponent extends React.Component {
  render() {
    return (
      <div>
        <p>Text: {this.props.value}</p>
        <input
          type="text"
          value={this.props.value}
          onChange={this.props.onChangeValue}
        />
      </div>
    );
  }
}

export default withLocalStorage("text")(ClassComponent);
```

- Another popular advanced React pattern are **React Render Prop Components**, which are often used as alternatives to React HOCs
  - Can both be used for [Class Components](#React%20Class%20Components) and [Function Components](#React%20Function%20Components)
  - Both are not much used in **modern** React applications - React function components with React Hooks are more normal for sharing logic across components

## React Function Components

> Sometimes called **functional components**

- Used as a replacement for React Class Components
- Expressed as functions instead of classes
- When it wasn’t possible to use state or side effects in FCs, they were also called **Functional Stateless Components**

  - Not the case anymore due to React Hooks which re-branded them to Function Components

- React Hooks brought state and side-effects to Function Components which make them these days the _industry standard_ for modern React Applications
- React comes with a variety of [React hooks](Hooks.md), but also the ability to create custom hooks

```jsx
import { useState } from "react";

const FunctionComponent = () => {
  const [text, setText] = useState("");

  const handleChangeText = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <p>Text: {text}</p>
      <input type="text" value={text} onChange={handleChangeText} />
    </div>
  );
};

export default FunctionComponent;
```

- [`useState`]([[Hooks#useState]]) is used for managing state
- [`useEffect`]([[Hooks#useEffect]]) is executed every time the value of the state changes

```jsx add={6-8} {4}
import { useEffect, useState } from "react";

const FunctionComponent = () => {
  const [text, setText] = useState(localStorage.getItem("text") || "");

  useEffect(() => {
    localStorage.setItem("text", text);
  }, [text]);

  const handleChangeText = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <p>Text: {text}</p>
      <input type="text" value={text} onChange={handleChangeText} />
    </div>
  );
};

export default FunctionComponent;
```

- Can extract both hooks as one encapsulated custom hook, which makes sure to synchronize the component state
  - Will end up returning the necessary value and setter function to be used in the Function Component

```jsx {3-11} add={14}
import { useEffect, useState } from "react";

const useLocalStorage = (storageKey) => {
  const [value, setValue] = useState(localStorage.getItem(storageKey) || "");

  useEffect(() => {
    localStorage.setItem(storageKey, value);
  }, [storageKey, value]);

  return [value, setValue];
};

const FunctionComponent = () => {
  const [text, setText] = useLocalStorage("text");

  const handleChangeText = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <p>Text: {text}</p>
      <input type="text" value={text} onChange={handleChangeText} />
    </div>
  );
};

export default FunctionComponent;
```

- Allows for the reuse in other components (abstraction)
- HOCs and Render Prop Components are used for both Class and Function Components
  - Recommended way to share logic across components is to use Custom Hooks

## React Server Components

> Most recent addition from 2023

- Allow developers to execute components on the server
- **Main benefit** is that only HTML is sent to the client and the component is allowed to access server-side resources
- Because the execute on the server, they serve a different use case from the above examples
  - RSCs can fetch data from a server-side resource (ie. database) before sending the JSX as rendered HTML to the client

```jsx
const ReactServerComponent = async () => {
  const posts = await db.query("SELECT * FROM posts");

  return (
    <div>
      <ul>
        {posts?.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
};

export default ReactServerComponent;
```

- **Client components** were also introduced
  - Traditional React Components that run on the Client-Side with JavaScript
- React only provides underlying specification and building blocks for RSC's
  - Relies on React frameworks to implement them (eg. NextJS)

## Async Components

> Only supported in RSCs, but are expected to be supported for Client Components in the future

- If a component is marked as async, it can perform asynchronous operations (eg. fetching data)
- At the moment, only JavaScript promises can be passed to a Client Component
  - In the future, it’s likely that React will support async components for Client Components, enabling you to fetch data within a Client Component before rendering it

```jsx
import { Suspense } from "react";

const ReactServerComponent = () => {
  const postsPromise = db.query("SELECT * FROM posts");

  return (
    <div>
      <Suspense>
        <ReactClientComponent promisedPosts={postsPromise} />
      </Suspense>
    </div>
  );
};
```

- It must be resolved with React’s `use` API in the client component

```jsx
"use client";

import { use } from "react";

const ReactClientComponent = ({ promisedPosts }) => {
  const posts = use(promisedPosts);

  return (
    <ul>
      {posts?.map((post) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
};

export { ReactClientComponent };
```
