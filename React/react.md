Here are the **Top 20 React.js Interview Questions** for candidates with **5 years of experience**, along with answers:

---

### **1. What are React's key features?**
- **JSX:** JavaScript syntax extension for writing UI components.
- **Virtual DOM:** Efficient UI updates using a diffing algorithm.
- **Component-Based Architecture:** Modular and reusable UI elements.
- **Unidirectional Data Flow:** One-way data binding using props.
- **Hooks:** Functions to manage state and side effects.

---

### **2. Explain the Virtual DOM and how it improves performance.**  
- React creates a **virtual copy of the DOM** (Virtual DOM).
- It performs **diffing** (compares new vs. old Virtual DOM).
- Uses **reconciliation** to update only the changed parts in the real DOM.
- **Reduces direct manipulations**, leading to **better performance**.

---

### **3. What is JSX, and why is it used?**  
- JSX stands for **JavaScript XML**, a syntax extension for writing React components.
- Example:
  ```jsx
  const element = <h1>Hello, React!</h1>;
  ```
- **Why JSX?**
  - Increases readability.
  - Prevents XSS attacks by escaping values.
  - Transpiled into `React.createElement()` calls.

---

### **4. What is the difference between Functional and Class Components?**
| Feature | Functional Component | Class Component |
|---------|----------------------|----------------|
| State Management | Uses **Hooks** (`useState`, `useEffect`) | Uses `this.state` |
| Lifecycle Methods | Uses **Hooks** | Uses methods like `componentDidMount()` |
| Performance | Faster, optimized | Slightly slower |
| Syntax | Simple, concise | Verbose |

---

### **5. What are React Hooks?**
- Hooks **enable state and side effects in functional components**.
- Examples:
  ```jsx
  import { useState, useEffect } from "react";
  
  function Counter() {
    const [count, setCount] = useState(0);
    
    useEffect(() => {
      console.log("Component mounted/updated");
    }, [count]);
    
    return <button onClick={() => setCount(count + 1)}>Increment</button>;
  }
  ```

---

### **6. Explain useState and useEffect Hooks.**
- `useState()`: Manages component **state**.
- `useEffect()`: Handles **side effects** (API calls, subscriptions).
  
Example:
```jsx
const [count, setCount] = useState(0);

useEffect(() => {
  console.log("Count changed:", count);
}, [count]); // Runs when 'count' changes
```

---

### **7. What is Prop Drilling, and how to avoid it?**
- **Prop Drilling**: Passing props deeply through multiple components.
- **Solution**:
  - **Context API**
  - **Redux or Zustand** (state management)

---

### **8. What is Context API?**
- Provides a **global state** without prop drilling.
- Example:
  ```jsx
  const MyContext = React.createContext();
  
  function App() {
    return (
      <MyContext.Provider value="Hello">
        <Child />
      </MyContext.Provider>
    );
  }
  
  function Child() {
    const value = useContext(MyContext);
    return <p>{value}</p>;
  }
  ```

---

### **9. What are controlled and uncontrolled components?**
- **Controlled**: React manages the component state.
- **Uncontrolled**: DOM handles the state.

Example (Controlled):
```jsx
function Form() {
  const [input, setInput] = useState("");
  return <input value={input} onChange={(e) => setInput(e.target.value)} />;
}
```

---

### **10. What is the difference between useCallback and useMemo?**
| Hook | Purpose |
|------|---------|
| `useCallback` | Memoizes a function to avoid unnecessary re-creation. |
| `useMemo` | Memoizes a **computed value** to avoid re-calculations. |

Example:
```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
const memoizedFunction = useCallback(() => handleClick(id), [id]);
```

---

### **11. How does React handle forms?**
- React uses **controlled components** to manage form data.
- Example:
  ```jsx
  function Form() {
    const [text, setText] = useState("");
    return <input value={text} onChange={(e) => setText(e.target.value)} />;
  }
  ```

---

### **12. What is the purpose of useReducer?**
- Used for **complex state management**.
- Alternative to `useState()`, similar to Redux reducer.
  
Example:
```jsx
const reducer = (state, action) => {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    default:
      return state;
  }
};

const [state, dispatch] = useReducer(reducer, { count: 0 });
```

---

### **13. What are Higher-Order Components (HOC)?**
- A **function that takes a component and returns a new component**.
- Used for **code reuse**.

Example:
```jsx
const withLogging = (Component) => (props) => {
  console.log("Component rendered!");
  return <Component {...props} />;
};
```

---

### **14. What are React Portals?**
- Allows rendering outside the main DOM tree.
- Used for **modals, tooltips**.

Example:
```jsx
ReactDOM.createPortal(<Modal />, document.getElementById("modal-root"));
```

---

### **15. What is React Suspense and Lazy Loading?**
- **Suspense**: Defers rendering until a condition is met.
- **Lazy Loading**: Loads components dynamically.

Example:
```jsx
const LazyComponent = React.lazy(() => import("./LazyComponent"));
<Suspense fallback={<Loading />}>
  <LazyComponent />
</Suspense>;
```

---

### **16. What are error boundaries in React?**
- **Class components that catch errors in child components.**
  
Example:
```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  render() {
    return this.state.hasError ? <h1>Something went wrong!</h1> : this.props.children;
  }
}
```

---

### **17. What is the difference between Redux and Context API?**
| Feature | Redux | Context API |
|---------|-------|------------|
| Complexity | High | Low |
| Middleware | Yes (e.g., Thunk, Saga) | No |
| Performance | Optimized for large apps | Best for small apps |

---

### **18. How to improve React performance?**
- Use **React.memo** to memoize components.
- Use **lazy loading**.
- Optimize **re-renders** using `useCallback` and `useMemo`.
- Use **shouldComponentUpdate** in class components.

---

### **19. How does reconciliation work in React?**
- **Diffing Algorithm** detects changes in Virtual DOM.
- Uses **key props** in lists for efficient updates.
- React **updates only necessary nodes**.

---

### **20. What are keys in React, and why are they important?**
- Keys help React **identify elements efficiently** in lists.
- **Best practice:** Use **unique IDs**.

Example:
```jsx
{items.map((item) => (
  <li key={item.id}>{item.name}</li>
))}
```

### **21. What is React.StrictMode?**
- A wrapper component that **identifies potential problems** in an application.
- Helps with:
  - Detecting **legacy lifecycle methods**.
  - Identifying **unexpected side effects**.
  - Highlighting **unsafe component patterns**.
  
Example:
```jsx
<React.StrictMode>
  <App />
</React.StrictMode>
```

---

### **22. What is hydration in React?**
- Hydration is the process of **attaching event listeners to a pre-rendered HTML page**.
- Used in **Server-Side Rendering (SSR)** for faster page loads.

Example:
```jsx
ReactDOM.hydrate(<App />, document.getElementById("root"));
```

---

### **23. How does React handle reconciliation in lists?**
- React uses **keys** to efficiently update lists.
- **Without keys:** Re-renders all items.
- **With keys:** Updates only changed items.

Bad practice:
```jsx
{items.map((item, index) => <li key={index}>{item}</li>)} // Avoid index as key
```
Good practice:
```jsx
{items.map((item) => <li key={item.id}>{item.name}</li>)} // Use unique ID
```

---

### **24. How does React optimize large lists?**
- **Windowing/Virtualization**: Renders only visible items using **react-window** or **react-virtualized**.
  
Example using `react-window`:
```jsx
import { FixedSizeList } from "react-window";

const Row = ({ index, style }) => <div style={style}>Row {index}</div>;

<FixedSizeList height={200} itemCount={1000} itemSize={35}>
  {Row}
</FixedSizeList>;
```

---

### **25. What is the difference between useLayoutEffect and useEffect?**
| Hook | When it runs | Use Case |
|------|-------------|----------|
| `useEffect` | After rendering | Fetching data, logging |
| `useLayoutEffect` | Before painting the screen | DOM measurements, animations |

Example:
```jsx
useLayoutEffect(() => {
  console.log("Runs before painting UI");
});
```

---

### **26. What are forwardRefs in React?**
- Allows passing **a reference to a child component**.
- Useful for **interacting with DOM elements**.

Example:
```jsx
const Input = React.forwardRef((props, ref) => <input ref={ref} {...props} />);

function Parent() {
  const inputRef = useRef();
  return <Input ref={inputRef} />;
}
```

---

### **27. What is the difference between useRef and useState?**
| Hook | Purpose | Triggers Re-render? |
|------|---------|--------------------|
| `useRef` | Holds a mutable reference | No |
| `useState` | Manages component state | Yes |

Example:
```jsx
const ref = useRef(0);
ref.current += 1; // Does NOT re-render

const [count, setCount] = useState(0);
setCount(count + 1); // Triggers re-render
```

---

### **28. What are React Fragments and why are they used?**
- **Fragments (`<></>`)** allow grouping elements **without adding extra DOM nodes**.

Example:
```jsx
<>
  <h1>Title</h1>
  <p>Some text</p>
</>
```
Equivalent to:
```jsx
<React.Fragment>
  <h1>Title</h1>
  <p>Some text</p>
</React.Fragment>
```

---

### **29. What is reconciliation in React?**
- **Process of updating the UI efficiently** using a diffing algorithm.
- Works by:
  - Comparing new and old **Virtual DOM**.
  - Updating only **changed nodes** in the real DOM.

---

### **30. What is the purpose of defaultProps in React?**
- Used to **set default values** for component props.

Example:
```jsx
function Button({ label }) {
  return <button>{label}</button>;
}

Button.defaultProps = {
  label: "Click Me",
};
```

---

These **30 questions** cover advanced React concepts for experienced developers. Let me know if you need more! 🚀
