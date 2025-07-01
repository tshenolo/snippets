# React Cheatsheet

React is a JavaScript library for building user interfaces. This cheatsheet covers core concepts like JSX, components, props, state, lifecycle methods (with a focus on hooks), event handling, conditional rendering, lists, forms, and common hooks.

## Core Concepts

*   **Components**: Reusable, self-contained pieces of UI. Can be JavaScript functions (Functional Components) or ES6 classes (Class Components). Functional Components with Hooks are the modern standard.
*   **JSX (JavaScript XML)**: A syntax extension for JavaScript that looks like HTML. It's used to describe what the UI should look like. JSX compiles to `React.createElement()` calls.
*   **Virtual DOM**: React keeps a lightweight representation of the actual DOM in memory. When state changes, React updates the Virtual DOM first, then efficiently updates only the necessary parts of the real DOM.
*   **Unidirectional Data Flow**: Data typically flows down from parent components to child components via props.

## Setup

*   **Create React App (Recommended for beginners)**:
    ```bash
    npx create-react-app my-react-app
    cd my-react-app
    npm start # or yarn start
    ```
*   **Vite (Faster alternative)**:
    ```bash
    npm create vite@latest my-vite-app -- --template react
    # or
    # yarn create vite my-vite-app --template react
    cd my-vite-app
    npm install
    npm run dev # or yarn dev
    ```
*   **Include React via CDN (for simple projects or testing)**:
    ```html
    <!-- In your HTML file -->
    <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
    <!-- Load Babel to transpile JSX in the browser (slow, for development only) -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

    <div id="root"></div>

    <script type="text/babel"> // Notice type="text/babel"
      // Your React code here
      function MyApp() {
        return <h1>Hello from CDN React!</h1>;
      }
      const container = document.getElementById('root');
      const root = ReactDOM.createRoot(container);
      root.render(<MyApp />);
    </script>
    ```

## JSX (JavaScript XML)

*   **Embedding Expressions**: Use curly braces `{}`.
    ```jsx
    const name = "Alice";
    const element = <h1>Hello, {name}!</h1>; // Renders "Hello, Alice!"
    ```
*   **Attributes**: Use camelCase for HTML attributes (e.g., `className` for `class`, `htmlFor` for `for`).
    ```jsx
    const element = <div className="container" tabIndex="0">Content</div>;
    const imgElement = <img src={user.avatarUrl} alt="User Avatar" />;
    ```
*   **Boolean Attributes**: `true` can be omitted. `false` should be `{false}`.
    ```jsx
    <button disabled>Click Me</button> // disabled={true}
    <button disabled={false}>Click Me</button>
    ```
*   **Children**: Tags can have children, just like HTML.
    ```jsx
    const element = (
      <div>
        <h1>Welcome!</h1>
        <p>This is a paragraph.</p>
      </div>
    );
    ```
*   **Fragments**: Group multiple elements without adding an extra node to the DOM.
    ```jsx
    // Short syntax (needs Babel 7+)
    // <>
    //   <td>Hello</td>
    //   <td>World</td>
    // </>

    // Older syntax
    // <React.Fragment>
    //   <td>Hello</td>
    //   <td>World</td>
    // </React.Fragment>
    ```
*   **Comments in JSX**:
    ```jsx
    const element = (
      <div>
        {/* This is a comment in JSX */}
        <h1>Title</h1>
        {// Another comment style
        }
      </div>
    );
    ```
*   **JavaScript expressions as children**:
    ```jsx
    function ItemList({ items }) {
      return (
        <ul>
          {items.map(item => <li key={item.id}>{item.name}</li>)}
        </ul>
      );
    }
    ```

## Components

*   **Functional Components (Recommended)**: Simple JavaScript functions that accept `props` as an argument and return JSX.
    ```jsx
    // Greeting.js
    import React from 'react';

    function Greeting(props) {
      return <h1>Hello, {props.name}!</h1>;
    }
    // Or using arrow function and destructuring props:
    // const Greeting = ({ name }) => {
    //   return <h1>Hello, {name}!</h1>;
    // };

    export default Greeting;

    // App.js
    // import Greeting from './Greeting';
    // function App() {
    //   return <Greeting name="World" />;
    // }
    ```
*   **Class Components (Older, still supported)**: ES6 classes that extend `React.Component`. Must have a `render()` method.
    ```jsx
    // Welcome.js
    import React from 'react';

    class Welcome extends React.Component {
      constructor(props) {
        super(props); // Always call super(props) in constructor
        // Initialize state here if needed (older way)
        // this.state = { message: "Initial message" };
      }

      render() {
        return <h1>Hello, {this.props.name}. Welcome to Class Components!</h1>;
      }
    }
    export default Welcome;
    ```

## Props (Properties)

Data passed from a parent component to a child component. Props are read-only in the child component.
```jsx
function UserProfile(props) {
  return (
    <div>
      <h2>{props.username}</h2>
      <p>Email: {props.email}</p>
      <img src={props.avatarUrl} alt={`${props.username}'s avatar`} />
    </div>
  );
}

// Usage:
// <UserProfile username="jdoe" email="jdoe@example.com" avatarUrl="/path/to/avatar.png" />

// Destructuring props:
function UserCard({ username, email, children }) { // 'children' is a special prop
  return (
    <div className="card">
      <h3>{username}</h3>
      <p>{email}</p>
      <div>{children}</div> {/* Renders content passed between <UserCard> tags */}
    </div>
  );
}
// <UserCard username="Alice" email="alice@example.com">
//   <p>This is child content.</p>
// </UserCard>

// Default Prop Values
// UserProfile.defaultProps = {
//   avatarUrl: '/default-avatar.png'
// };
```

## State

Data that is managed within a component. When state changes, the component re-renders.

*   **`useState` Hook (for Functional Components)**:
    ```jsx
    import React, { useState } from 'react';

    function Counter() {
      // useState returns an array: [currentState, stateUpdaterFunction]
      const [count, setCount] = useState(0); // 0 is the initial state

      const increment = () => {
        setCount(count + 1);
      };
      const decrement = () => {
        setCount(prevCount => prevCount - 1); // Using previous state for updater
      };

      return (
        <div>
          <p>Count: {count}</p>
          <button onClick={increment}>Increment</button>
          <button onClick={decrement}>Decrement</button>
        </div>
      );
    }
    export default Counter;
    ```
    *   State updates may be asynchronous.
    *   If new state depends on the previous state, use the functional update form: `setCount(prevCount => prevCount + 1)`.
*   **`this.state` and `this.setState` (for Class Components)**:
    ```jsx
    class Timer extends React.Component {
      constructor(props) {
        super(props);
        this.state = { seconds: 0 };
      }

      componentDidMount() { // Lifecycle method
        this.intervalId = setInterval(() => {
          this.setState(prevState => ({
            seconds: prevState.seconds + 1
          }));
        }, 1000);
      }

      componentWillUnmount() { // Lifecycle method
        clearInterval(this.intervalId);
      }

      render() {
        return <p>Seconds Elapsed: {this.state.seconds}</p>;
      }
    }
    ```

## Lifecycle Methods & Hooks

*   **Functional Components with Hooks**:
    *   **`useEffect(callbackFn, dependencyArray)`**: For side effects (data fetching, subscriptions, manually changing DOM).
        *   Runs after every render by default if no dependency array.
        *   `dependencyArray`:
            *   `[]` (empty array): Runs only once after the initial render (like `componentDidMount`).
            *   `[var1, var2]`: Runs after initial render AND whenever `var1` or `var2` changes.
            *   Return a cleanup function: Runs before the component unmounts or before the effect runs again (like `componentWillUnmount`).
        ```jsx
        import React, { useState, useEffect } from 'react';

        function DataFetcher({ userId }) {
          const [data, setData] = useState(null);
          const [loading, setLoading] = useState(true);

          useEffect(() => {
            console.log("Effect triggered due to userId change:", userId);
            setLoading(true);
            fetch(`https://api.example.com/users/${userId}`)
              .then(response => response.json())
              .then(userData => {
                setData(userData);
                setLoading(false);
              })
              .catch(error => {
                console.error("Failed to fetch user data:", error);
                setLoading(false);
              });

            // Cleanup function (optional)
            return () => {
              console.log("Cleanup for userId:", userId);
              // e.g., abort fetch request, remove event listener
            };
          }, [userId]); // Re-run effect if userId changes

          if (loading) return <p>Loading data...</p>;
          if (!data) return <p>No data found.</p>;

          return <div>User Name: {data.name}</div>;
        }
        export default DataFetcher;
        ```
*   **Class Component Lifecycle Methods (Common Ones)**:
    *   `constructor(props)`: Initialize state, bind methods.
    *   `render()`: Returns JSX. Required.
    *   `componentDidMount()`: Called once after the component is mounted to the DOM. Good for API calls, subscriptions.
    *   `componentDidUpdate(prevProps, prevState)`: Called after component updates (props or state change). Not called on initial render.
    *   `componentWillUnmount()`: Called just before component is unmounted and destroyed. Good for cleanup (timers, subscriptions).
    *   `shouldComponentUpdate(nextProps, nextState)`: Performance optimization. Return `false` to prevent re-render.
    *   `getDerivedStateFromError(error)` and `componentDidCatch(error, info)`: For error boundaries.

## Event Handling

Handle events using camelCase event names (e.g., `onClick`, `onChange`, `onSubmit`). Event handlers are typically functions.
```jsx
function MyForm() {
  const [inputValue, setInputValue] = useState('');

  const handleChange = (event) => {
    // event.target refers to the DOM element that triggered the event
    setInputValue(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault(); // Prevent default form submission (page reload)
    alert(`Form submitted with value: ${inputValue}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={inputValue} onChange={handleChange} />
      </label>
      <button type="submit">Submit</button>
      <p>Current Value: {inputValue}</p>
    </form>
  );
}
```

## Conditional Rendering

*   **If Statements**:
    ```jsx
    function UserGreeting(props) {
      if (props.isLoggedIn) {
        return <h1>Welcome back!</h1>;
      }
      return <h1>Please sign up.</h1>;
    }
    ```
*   **Ternary Operator (`condition ? exprIfTrue : exprIfFalse`)**:
    ```jsx
    function LoginStatus({ isLoggedIn }) {
      return (
        <div>
          {isLoggedIn ? <p>You are logged in.</p> : <button>Login</button>}
        </div>
      );
    }
    ```
*   **Logical `&&` Operator (Short-circuiting)**: If condition is true, element after `&&` is rendered.
    ```jsx
    function Mailbox({ unreadMessages }) {
      return (
        <div>
          <h1>Hello!</h1>
          {unreadMessages.length > 0 &&
            <h2>You have {unreadMessages.length} unread messages.</h2>
          }
        </div>
      );
    }
    ```
*   **Preventing Component from Rendering**: Return `null`.
    ```jsx
    function WarningBanner(props) {
      if (!props.warn) {
        return null; // Component will not render
      }
      return <div className="warning">Warning!</div>;
    }
    ```

## Lists and Keys

Render collections of items using `map()`. Each list item needs a unique `key` prop.
Keys help React identify which items have changed, are added, or are removed. Keys should be stable, unique among siblings, and ideally a string ID from your data.
```jsx
function TodoList({ todos }) {
  // todos is an array like: [{ id: 1, text: 'Learn React' }, { id: 2, text: 'Build App' }]
  const listItems = todos.map((todo) =>
    <li key={todo.id.toString()}> {/* Key must be a string or number */}
      {todo.text}
    </li>
  );
  return <ul>{listItems}</ul>;
}
// Or inline:
// function TodoList({ todos }) {
//   return (
//     <ul>
//       {todos.map(todo => <li key={todo.id}>{todo.text}</li>)}
//     </ul>
//   );
// }
```

## Forms

HTML form elements work a bit differently in React. Typically, form state is handled by the component (Controlled Components).

*   **Controlled Components**: Form input values are controlled by React state.
    ```jsx
    function NameForm() {
      const [name, setName] = useState('');

      const handleChange = (event) => {
        setName(event.target.value.toUpperCase()); // Example: transform input
      };

      const handleSubmit = (event) => {
        alert('A name was submitted: ' + name);
        event.preventDefault();
      };

      return (
        <form onSubmit={handleSubmit}>
          <label>
            Name:
            <input type="text" value={name} onChange={handleChange} />
          </label>
          <button type="submit">Submit</button>
        </form>
      );
    }
    ```
    *   For `<textarea>`, use `value` prop.
    *   For `<select>`, use `value` prop on the `select` tag. Multiple selections use an array for `value`.
    *   For `checkbox` and `radio` inputs, use `checked` prop and `onChange`.

## Hooks (Common Built-in Hooks)

*   **`useState(initialState)`**: Manages state in functional components. Returns `[state, setStateFn]`.
*   **`useEffect(didUpdateCallback, dependencyArray?)`**: Handles side effects.
*   **`useContext(MyContext)`**: Accesses value from a React Context.
    ```jsx
    // MyContext.js
    // const MyThemeContext = React.createContext('light'); // Default value

    // ComponentUsingContext.js
    // import React, { useContext } from 'react';
    // import MyThemeContext from './MyContext';
    // function ComponentUsingContext() {
    //   const theme = useContext(MyThemeContext);
    //   return <div style={{ background: theme === 'dark' ? '#333' : '#FFF' }}>Theme is {theme}</div>;
    // }
    ```
*   **`useReducer(reducerFn, initialState, initFn?)`**: Alternative to `useState` for more complex state logic or when next state depends on previous one in a more involved way.
    ```jsx
    // const initialState = {count: 0};
    // function reducer(state, action) {
    //   switch (action.type) {
    //     case 'increment': return {count: state.count + 1};
    //     case 'decrement': return {count: state.count - 1};
    //     default: throw new Error();
    //   }
    // }
    // function CounterWithReducer() {
    //   const [state, dispatch] = useReducer(reducer, initialState);
    //   return (
    //     <>
    //       Count: {state.count}
    //       <button onClick={() => dispatch({type: 'decrement'})}>-</button>
    //       <button onClick={() => dispatch({type: 'increment'})}>+</button>
    //     </>
    //   );
    // }
    ```
*   **`useCallback(fn, deps)`**: Returns a memoized version of the callback function that only changes if one of the dependencies (`deps`) has changed. Useful for performance optimization, especially when passing callbacks to optimized child components that rely on reference equality.
*   **`useMemo(createFn, deps)`**: Returns a memoized value. `createFn` is only recomputed when one of the dependencies (`deps`) has changed. Useful for expensive calculations.
*   **`useRef(initialValue)`**: Returns a mutable ref object whose `.current` property is initialized to the passed argument. Can hold a reference to a DOM element or any mutable value that persists across renders without causing re-renders.
    ```jsx
    // function TextInputWithFocusButton() {
    //   const inputEl = useRef(null);
    //   const onButtonClick = () => {
    //     // `current` points to the mounted text input element
    //     inputEl.current.focus();
    //   };
    //   return (
    //     <>
    //       <input ref={inputEl} type="text" />
    //       <button onClick={onButtonClick}>Focus the input</button>
    //     </>
    //   );
    // }
    ```

## Context API

Provides a way to pass data through the component tree without having to pass props down manually at every level.
```jsx
// 1. Create Context
// const ThemeContext = React.createContext('light'); // 'light' is the default value

// App.js (Provider)
// function App() {
//   const [theme, setTheme] = useState('dark');
//   return (
//     <ThemeContext.Provider value={theme}> {/* Pass current theme down */}
//       <Toolbar />
//       <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>Toggle Theme</button>
//     </ThemeContext.Provider>
//   );
// }

// Toolbar.js (Intermediate component, doesn't need to know about theme)
// function Toolbar() { return <ThemedButton />; }

// ThemedButton.js (Consumer)
// import React, { useContext } from 'react';
// import ThemeContext from './ThemeContext'; // Assuming context is in its own file
// function ThemedButton() {
//   const theme = useContext(ThemeContext); // Consume the context value
//   return <button style={{ background: theme === 'dark' ? '#555' : '#EEE', color: theme === 'dark' ? 'white' : 'black' }}>
//            I am styled by theme context!
//          </button>;
// }
```

## Routing (using React Router - most popular library)

Install: `npm install react-router-dom`
```jsx
// App.js
// import React from "react";
// import { BrowserRouter as Router, Routes, Route, Link } from "react-router-dom";

// function Home() { return <h2>Home</h2>; }
// function About() { return <h2>About</h2>; }
// function Users() { return <h2>Users</h2>; }

// export default function App() {
//   return (
//     <Router>
//       <div>
//         <nav>
//           <ul>
//             <li><Link to="/">Home</Link></li>
//             <li><Link to="/about">About</Link></li>
//             <li><Link to="/users">Users</Link></li>
//           </ul>
//         </nav>
//         <Routes> {/* Replaces Switch in v6 */}
//           <Route path="/about" element={<About />} />
//           <Route path="/users" element={<Users />} />
//           <Route path="/" element={<Home />} />
//         </Routes>
//       </div>
//     </Router>
//   );
// }
```

This provides a comprehensive React cheatsheet with actionable examples. I'll proceed with `vuejs.md`.The `react.md` cheatsheet has been successfully updated with detailed code snippets and explanations for core React concepts, JSX, components, props, state (with `useState`), lifecycle (with `useEffect`), event handling, conditional rendering, lists, forms, common hooks, Context API, and a basic example for React Router.

Next, I will enhance `vuejs.md`, focusing on its template syntax, directives, reactivity, computed properties, watchers, components, props, events, slots, lifecycle hooks, and an introduction to the Composition API.
