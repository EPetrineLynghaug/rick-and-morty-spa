React Application with Modular & Scoped Styling
Overview

This project leverages React alongside modern CSS practices to create a scalable, maintainable single-page application (SPA). The styling strategy combines global CSS, CSS Modules, and optional libraries such as Tailwind CSS and styled-components. These lecture notes from February 4 outline the best practices for naming conventions, file organization, and styling approaches.
CSS & Styling Guidelines
CSS Modules

* File Naming & Importing:
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

    import './index.css';

Inline Styles

**Usage Consideration:**
- Inline styles ({{ color: 'red' }}) are supported in React.
- They are useful for quick tests or debugging, but for long-term maintainability, extracting styles into modules or using styled-components is preferred.

Tailwind CSS

**Integration & Benefits:**
- Tailwind CSS offers utility-first classes that simplify responsive design and reduce clutter.
- Instead of writing long lists of class names manually, Tailwind lets you apply pre-defined classes.
- In Tailwind v4, you typically import it once at the top level of your application.

**Usage:**
- Add Tailwind class names directly to the className attribute in your components. For more complex styling, use @apply to combine multiple utility classes into a single class.

**Styled Components:**

**Concept:**
-  Styled components allow you to write CSS within your JavaScript files, keeping styles scoped to individual components without relying on separate CSS files.
- Example:
```css

    import styled from 'styled-components';

    const StyledButton = styled.button`
      background-color: var(--primary-color);
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 4px;
    `;
```

**Best Practices**

**Modular & Scoped Styling:**
- Keep component styles isolated using CSS Modules or styled-components.
- This prevents style conflicts and simplifies maintenance.

**Avoid Over-Specificity:**
- Instead of deeply nested selectors (e.g., .header .nav .list-item a), use simpler, more generic class names (e.g., .nav-link) to avoid specificity issues that may require !important overrides.

**Organization:**
-  Organize your project so that each component has its own folder containing its JavaScript file, CSS module, and any tests or helper files.
Example structure for a component:

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

**Project Structure**

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

Client-Side Routing:
    - Utilize React Router for handling client-side navigation, ensuring a seamless SPA experience:

 - import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

 - Components such as Header and Footer are typically rendered outside individual route components, ensuring they persist across all pages.

**Data Handling:**
     Pages like Home, Characters, and Character Details fetch data from an API.
     Route parameters (e.g., an ID in the URL) are used to fetch and display details dynamically.

**Entry Point:**
        The index.js file renders the main App component, which encapsulates the router and persistent components.

**Final Notes**

 **Scalability:**
 Starting with a modular approach to both JavaScript and CSS makes it easier to scale the application.

 **Consistency:**

- Adhere to consistent naming conventions and organizational practices to keep the project maintainable as it grows.

**Production:**
-  Remember to minify and optimize your CSS and JS files for production to ensure optimal performance.