#  Lecture Notes: React Application with Modular & Scoped Styling
This project leverages React alongside modern CSS practices to create a scalable, maintainable single-page application (SPA). The styling strategy combines global CSS, CSS Modules, and optional libraries such as Tailwind CSS and styled-components. These lecture notes from February 4 outline the best practices for naming conventions, file organization, and styling approaches.
CSS & Styling Guidelines
CSS Modules

**File Naming & Importing:**
- Name component-specific CSS files as [componentName].module.css (e.g., button.module.css or header.module.css).
-  When importing, assign the module to a variable (commonly styles):

import styles from './button.module.css';

This approach lets you use generic class names (like .primary) without conflicts, since the names are scoped to the module.

**Naming Conventions:**
- Use clear, descriptive names.
 - Consider BEM conventions (e.g., .btn--primary), or simply use camelCase.
- The goal is consistency and clarity across your project.

**Global CSS**

**Purpose & Usage:**
- Global styles are used to set base rules and shared styles that apply throughout the application. This includes:
- CSS Resets: Reset styles such as box-sizing: border-box, margin: 0, etc.
- Typography & Layout: Define global fonts, line-heights, and layout properties.
- CSS Variables: Set variables (e.g., --primary-color) under the :root selector for consistency.
- Animations: Centralize animations that might be reused in multiple components.

Implementation:
 - Import the global CSS file in your entry point (e.g., index.js or index.jsx):

- import './index.css';

## Inline Styles
<details> <summary><strong>Click to read more</strong></summary>

**Usage Consideration:**
- Inline styles ({{ color: 'red' }}) are supported in React.
- They are useful for quick tests or debugging, but for long-term maintainability, extracting styles into modules or using styled-components is preferred.


</details>

## Tailwind CSS
<details> <summary><strong>Click to read more</strong></summary>

**Integration & Benefits:**
- Tailwind CSS offers utility-first classes that simplify responsive design and reduce clutter.
- Instead of writing long lists of class names manually, Tailwind lets you apply pre-defined classes.
- In Tailwind v4, you typically import it once at the top level of your application.

**Usage:**
- Add Tailwind class names directly to the className attribute in your components. For more complex styling, use @apply to combine multiple utility classes into a single class.

**Styled Components:**

**Concept:**
-  Styled components allow you to write CSS within your JavaScript files, keeping styles scoped to individual components without relying on separate CSS files.

**Example:**

```CSS

  import styled from 'styled-components';
    const StyledButton = styled.button`

 background-color: var(--primary-color);
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
    `;

```

</details>

**Best Practices**
<details> <summary><strong>Click to read more</strong></summary>


**Modular & Scoped Styling:**
- Keep component styles isolated using CSS Modules or styled-components.
- This prevents style conflicts and simplifies maintenance.

**Avoid Over-Specificity:**
- Instead of deeply nested selectors (e.g., .header .nav .list-item a), use simpler, more generic class names (e.g., .nav-link) to avoid specificity issues that may require !important overrides.

**Organization:**
-  Organize your project so that each component has its own folder containing its JavaScript file, CSS module, and any tests or helper files.

**Example structure for a component:**

```bash
 /components
  /Button
    Button.js
     button.module.css
```
**Responsive Design:**
Ensure responsiveness from the start. Tailwind offers built-in responsive utilities, but even traditional CSS should be written with responsiveness in mind.

**Testing & Performance:**
-  Test your styles across multiple browsers and operating systems.
- For production, make sure to minify your CSS and JavaScript files to improve performance.

</details>

**Project Structure**
<details> <summary><strong>Click to read more</strong></summary>

A typical project structure might look like this:

/project-root
├── index.js         // Entry point: renders the App component
├── index.css        // Global CSS: resets, typography, CSS variables, and animations
├── App.js           // Main component that handles routing and layout
└── /components
    ├── /Button
    │   ├── Button.js
    │   └── button.module.css
    ├── /Header
    │   ├── header.js
    │   └── header.module.css
    └── /Footer
        ├── footer.js
        └── footer.module.css

**Global vs. Component Styles:**
- Global styles (e.g., resets and shared animations) reside in index.css.
- Component-specific styles are encapsulated within CSS modules in their respective folders.

**Routing & Application Setup**

**Client-Side Routing:**
- Utilize React Router for handling client-side navigation, ensuring a seamless SPA experience:
 - import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
 - Components such as Header and Footer are typically rendered outside individual route components, ensuring they persist across all pages.

**Data Handling:**
-  Pages like Home, Characters, and Character Details fetch data from an API.
-  Route parameters (e.g., an ID in the URL) are used to fetch and display details dynamically.

**Entry Point:**
- The index.js file renders the main App component, which encapsulates the router and persistent components.

</details>


**Final Notes**
<details> <summary><strong>Click to read more</strong></summary>

**Scalability:**
 Starting with a modular approach to both JavaScript and CSS makes it easier to scale the application.

 **Consistency:**
- Adhere to consistent naming conventions and organizational practices to keep the project maintainable as it grows.

**Production:**
-  Remember to minify and optimize your CSS and JS files for production to ensure optimal performance.


</details>


# Lecture Notes: userState and UseEffect

## React Hooks Overview 
<details> <summary><strong>Click to read more</strong></summary>


React Hooks provide a way to manage state and side effects in functional components. Below is a brief introduction and examples of the most commonly used hooks:  
- **useState**  
- **useEffect**  
- **useReducer**  
- **useContext**  

These hooks help you store and update data (state) at different points in your application while keeping your code simpler and more organized compared to older class-based components.

</details>

## Table of Contents
<details> <summary><strong>Click to read more</strong></summary>

1. [Key Hooks and Their Purpose](#key-hooks-and-their-purpose)  
2. [useState](#usestate)  
3. [useEffect](#useeffect)  
4. [useReducer](#usereducer)  
5. [useContext](#usecontext)  
6. [Additional Notes](#additional-notes)


</details>

## ## Key Hooks and Their Purpose
<details> <summary><strong>Click to read more</strong></summary>
 **Hook**       | **Purpose**                       | **Best For**                                       |
|----------------|-----------------------------------|----------------------------------------------------|
| **useState**   | Manages local state               | Simple state updates                               |
| **useEffect**  | Handles side effects              | Fetching data, subscriptions, updating the DOM, etc.  |
| **useReducer** | Manages complex state transitions | Multiple actions, more advanced or structured updates |
| **useContext** | Shares state across components    | Avoiding prop drilling, managing global state      |


</details>

## Querying Data
<details> <summary><strong>Click to read more</strong></summary>

</details>

## useState
<details> <summary><strong>Click to read more</strong></summary>

### What It Does
- **useState** lets you add React state to functional components.
- You call it inside a component to create a piece of local state tied to that component’s lifecycle.

### Basic Example
```jsx
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}

export default Counter;

```
- Here, count is the current state and setCount is the function that updates it.
- Using an anonymous function in the onClick ensures setCount is only called when the button is clicked.

### Updating State Correctly

Sometimes, especially in loops or repeated state updates, you may want to use a callback form:
```jsx
setCount(prevCount => prevCount + 1);
```
This ensures you always get the latest state.

### Objects and Arrays in useState

- When using objects or arrays, use the spread operator (...) to create copies instead of mutating the original state directly:
```jsx
const [user, setUser] = useState({ name: "Lasse", age: 55 });

// Correct way to update:
setUser(prevUser => ({
  ...prevUser,
  age: prevUser.age + 1
}));
```
- React expects state to be treated as immutable—always create a new copy instead of modifying the existing one.

### Example with Arrays
```jsx
function TodoList() {
  const [tasks, setTasks] = useState(["Learn React"]);

  const addTask = () => {
    setTasks(prevTasks => [...prevTasks, "New Task"]);
  };

  return (
    <div>
      <ul>
        {tasks.map((task, index) => (
          <li key={index}>{task}</li>
        ))}
      </ul>
      <button onClick={addTask}>Add Task</button>
    </div>
  );
}
```
- he new task is added to a new array using the spread operator.

</details>


## useEffect
<details> <summary><strong>Click to read more</strong></summary>

### What It Does

- useEffect is for performing side effects in a React component:
- Data fetching (e.g., from an API)
- Subscribing or unsubscribing to events (e.g., window resize, WebSocket messages)
- Updating the DOM manually
-  Setting up or cleaning up intervals/timers

### Basic Example (Data Fetching)
```jsx
import React, { useEffect, useState } from "react";

function UsersList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then(response => response.json())
      .then(data => setUsers(data));
  }, []); // The empty array means "run once on mount"

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

export default UsersList;
```
- The second argument [] (dependency array) ensures the effect runs only once when the component mounts.

### Cleanup (e.g., Event Listeners, Intervals)
```jsx
function WindowSize() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener("resize", handleResize);

    // Cleanup function to remove the event listener
    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  return <p>Window width: {width}px</p>;
}

export default WindowSize;
```
-  Always clean up side effects to avoid memory leaks, especially with intervals or event listeners.

### Common Pitfalls

-  Missing the dependency array or incorrectly setting it can cause infinite loops.
- Each time dependencies in the array change, the effect runs again.

</details>


## useReducer
<details> <summary><strong>Click to read more</strong></summary>

**What It Does**

- useReducer is like a “more powerful useState” for complex state logic.
- It’s particularly useful when you have multiple sub-values that need to be managed in one place or when state transitions follow specific patterns.

**Example**
```jsx
import React, { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function CounterWithReducer() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>
        Increment
      </button>
      <button onClick={() => dispatch({ type: "decrement" })}>
        Decrement
      </button>
    </div>
  );
}

export default CounterWithReducer;
```
- A reducer function decides how to update the state based on an action.

</details>

## useContext
<details> <summary><strong>Click to read more</strong></summary>

**What It Does:**

- useContext lets you share state or other data across multiple components without passing props down multiple levels.
-  Useful for global data, like themes (light or dark mode) or user authentication info.

**Basic Example**
```jsx
import React, { createContext, useContext, useState } from "react";

const ThemeContext = createContext();

function App() {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  return (
    <div>
      <ThemeButton />
    </div>
  );
}

function ThemeButton() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <button
      onClick={() => setTheme(theme === "light" ? "dark" : "light")}
      style={{
        backgroundColor: theme === "light" ? "#FFF" : "#333",
        color: theme === "light" ? "#000" : "#FFF"
      }}
    >
      Toggle Theme
    </button>
  );
}

export default App;
```
- ThemeContext.Provider provides the value for any child component that calls useContext(ThemeContext).


</details>

## Additional Notes
<details> <summary><strong>Click to read more</strong></summary>

**Rendering and Virtual DOM**

- React uses a virtual DOM. Whenever state changes, React determines the minimal set of changes required to update the UI.

**Avoiding Infinite Loops with useEffect**

- If you update state inside useEffect without a proper dependency array, you can cause a component to re-render indefinitely.
- Be sure to include correct dependencies in the array or leave it empty if you only want the effect to run once.

**Pagination Example (Brief Overview)**

- You can use a combination of useState (for the current page) and useEffect (to fetch data for that page) to implement pagination.
- Alternatively, fetch all data at once, store it in state, and slice the data to simulate pages locally.
- Pros: Quick local transitions (no extra requests once the data is loaded).
- Cons: Possibly large memory usage or long initial load if the dataset is huge.

**Combining Hooks**

- It’s common to use multiple useEffect hooks in a single component for different tasks (fetching data, setting up an event listener, etc.).
- You can combine useState and useReducer in the same component if needed. They solve similar problems but at different scales of complexity.

</details>

## Summary
<details> <summary><strong>Click to read more</strong></summary>
eact Hooks such as useState, useEffect, useReducer, and useContext allow developers to manage state and side effects in functional components. These hooks simplify code organization and replace the need for most class components. By using them correctly, you can create clean, efficient, and easily testable React applications.

- **useState:** Local state management (simple counters, toggles, forms).
- **useEffect:** Side effects (fetching data, managing subscriptions, intervals).
- **useReducer:** Complex state transitions with multiple actions.
- **useContext:** Global or shared state across multiple components.

Each hook addresses a specific need—together, they form a powerful toolkit for modern React development.

</details>

