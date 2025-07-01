# React Cheatsheet

*   **Core Concepts**: Components, JSX, Virtual DOM.
*   **Setup**: Create React App, Vite.
*   **JSX**: Syntax, embedding expressions (`{}`), attributes, children.
*   **Components**:
    *   Functional Components: Simple functions returning JSX.
    *   Class Components (less common now): `extends React.Component`, `render()` method.
*   **Props (Properties)**: Passing data from parent to child components, `props` object, `props.children`.
*   **State**: Managing component-specific data that can change over time.
    *   `useState` Hook: For functional components (`const [value, setValue] = useState(initialValue)`).
    *   `this.state` and `this.setState` (for class components).
*   **Lifecycle (Functional Components with Hooks)**:
    *   `useEffect`: For side effects (data fetching, subscriptions, manually changing DOM). Dependencies array. Cleanup function.
*   **Handling Events**: `onClick`, `onChange`, etc., event handlers.
*   **Conditional Rendering**: `if` statements, ternary operator (`{condition ? <True /> : <False />}`), logical `&&` operator.
*   **Lists and Keys**: Rendering collections of items, `map()` function, `key` prop for list items.
*   **Forms**: Controlled components, handling form input and submission.
*   **Hooks (Common)**:
    *   `useState`: Manage state.
    *   `useEffect`: Handle side effects.
    *   `useContext`: Access context API.
    *   `useReducer`: For complex state logic.
    *   `useCallback`, `useMemo`: Performance optimizations.
*   **Component Patterns**: Container/Presentational, Higher-Order Components (HOCs), Render Props (less common with hooks).
*   **Context API**: For global state management or avoiding prop drilling.
*   **Routing**: (e.g., React Router) `BrowserRouter`, `Route`, `Link`, `Switch` (or `Routes` in v6).
