### **1. What is the use of Webpack in React?**
**Answer:**
- **Webpack** is a module bundler used in React applications to bundle JavaScript, JSX, CSS, and other assets into optimized files for the browser.
- It works with Babel to convert JSX and modern JavaScript into browser-compatible code.
-  Webpack also helps with code splitting, lazy loading, and asset management like images and styles.
---
### **2. What is Babel in ReactJS?**
**Answer:**
- Babel is a **JavaScript compiler (transpiler)** used in ReactJS to convert modern JavaScript and JSX code into a version of JavaScript that browsers can understand.
- **Why Babel is needed in React**
- Browsers do **not understand JSX** or some modern JavaScript (ES6+). Babel helps by converting:
- **JSX → JavaScript**.
- **ES6+ → ES5 (browser-compatible JS)**

### **3. What are Synthetic Events in React?**
**Answer:**
- **Synthetic Events** are React’s wrapper around native browser events.
- They provide a **consistent and normalized event system** that works the same way across all browsers.
- **Why does React use Synthetic Events?**
  - Ensure **cross-browser compatibility**.
  - Improve **performance** using event delegation.
  - Automatically manage event cleanup.
  - Improve performance using **event delegation**.

### **4. What is React Fiber?**
**Answer:**
- React Fiber is the engine React uses to render and update the UI in a smooth,**non-blocking** way by breaking work into small prioritized tasks.
- Fiber is React’s **reconciliation engine** allowing:
  - Incremental rendering.
  - Task prioritization.
  - Efficient updates for large apps.
    
### **5. What is React Profiler?**
**Answer:**
- **React Profiler** is a **developer tool** used to **measure and analyze the performance of React components**.
- React Profiler helps you see which components re-render, how often they render, and how long they take.
- **Why it’s useful?**
  - Finds **slow components**.
  - Detects **unnecessary re-renders**.
  - Helps optimize performance.
    
### **6. What is a React query ?**
**Answer:**
- **React Query** is a powerful and flexible data-fetching library for React applications. It simplifies the process of fetching, **caching**, **synchronizing**, and updating data from various sources, such as APIs, databases, and GraphQL endpoints. React Query is designed to work seamlessly with React and provides a set of hooks that enable efficient data management and a smooth user experience.

### **7. HashRouter vs BrowserRouter**
**Answer:**
- HashRouter uses URL hashes and doesn’t need server setup, while BrowserRouter uses clean URLs and requires server configuration.
  
### **8. useRef vs forwardRef**
**Answer:**
- **useRef** is a React hook used to **store a mutable value or access a DOM element** without causing a re-render.
- **forwardRef** allows a **parent component to pass a ref to a child component**.
  
### **9. Why do we need Redux and the Context API, and which one is better?**
**Answer:**
 - Both are used for **state management** to avoid **prop drilling** and share data between multiple components
 - **Context API**
   - Built-in React feature.
   - Best for **small to medium apps**
   - Used for **global data** (theme, auth, language).
   - **Pros:** Simple, no extra library.
   - **Cons:** Performance issues with frequent updates.
 - **Redux**
   - External state management library.
   - Best for **large, complex apps**.
   - Centralized, predictable state with DevTools.
   - **Pros:** Scalable, debugging, middleware support.
   - **Cons:** More boilerplate (less with Redux Toolkit).
     
### **10. Optimizing Performance in Large React Apps**
**Answer:**
 - Use **React.memo** and **useMemo**hooks to prevent unnecessary renders.
 - Implement **code splitting** with **React.lazy**.
 - Use the **Profiler API** to identify slow renders.
 
### **11. How do you test React components?**
**Answer:**
- **Jest:** Test runner.
- **React Testing Library:** Render and assert components.
- **Cypress:** E2E testing.
  
### **12. How does React handle server-side rendering (SSR)?**
**Answer:**
 - Frameworks like Next.js render React on the server for SEO/performance, hydrating it client-side.

---

### **13. useEffect for API Fetching.**
Example:
```jsx
import { useEffect, useState } from "react";

function Users() {
  const [data, setData] = useState([]);

  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch("https://api.example.com/users");
        const result = await response.json();
        setData(result);
      } catch (error) {
        console.error(error);
      }
    };

    fetchData();
  }, []); 

  return <div>{data.length} Users</div>;
}

```
### **14. What are Pure Components?**
**Answer:**
**Pure Components**in React are components that only re-render when their props or state change. They use shallow comparison to check if the props or state have changed, preventing unnecessary re-renders and improving performance.
- Class components can extend **React.PureComponent** to become pure.
- Functional components can use **React.memo** for the same effect.
  ```jsx
  const PureFunctionalExample = React.memo(function ({ value }) {
  return <div>{value}</div>;
    });
  
  ```
  
### **15. Rules of Hooks**
**Answer:**
- Only call Hooks at the **top level**.
- Only call Hooks from **React functions**.
  This ensures consistent hook order across renders.
