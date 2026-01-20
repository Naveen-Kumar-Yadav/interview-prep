Here are **10 React problem-solving coding challenges** along with their solutions, suitable for a **5-year experienced developer**:

---

### **1. Create a Custom Hook for Debouncing Input**
**Problem:** Implement a `useDebounce` hook to delay execution until the user stops typing.

**Solution:**
```jsx
import { useState, useEffect } from "react";

function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const handler = setTimeout(() => setDebouncedValue(value), delay);
    return () => clearTimeout(handler);
  }, [value, delay]);

  return debouncedValue;
}

// Usage
function SearchInput() {
  const [query, setQuery] = useState("");
  const debouncedQuery = useDebounce(query, 500);

  useEffect(() => {
    if (debouncedQuery) {
      console.log("Fetching results for:", debouncedQuery);
    }
  }, [debouncedQuery]);

  return <input value={query} onChange={(e) => setQuery(e.target.value)} />;
}
```

---

### **2. Implement Infinite Scrolling**
**Problem:** Fetch more data when the user scrolls to the bottom.

**Solution:**
```jsx
import { useState, useEffect } from "react";

function InfiniteScroll() {
  const [items, setItems] = useState([]);
  const [page, setPage] = useState(1);

  useEffect(() => {
    fetch(`https://api.example.com/items?page=${page}`)
      .then((res) => res.json())
      .then((data) => setItems((prev) => [...prev, ...data]));
  }, [page]);

  const handleScroll = () => {
    if (window.innerHeight + window.scrollY >= document.body.offsetHeight - 10) {
      setPage((prev) => prev + 1);
    }
  };

  useEffect(() => {
    window.addEventListener("scroll", handleScroll);
    return () => window.removeEventListener("scroll", handleScroll);
  }, []);

  return <ul>{items.map((item, index) => <li key={index}>{item.name}</li>)}</ul>;
}
```

---

### **3. Create a Dark Mode Toggle**
**Problem:** Implement dark mode with local storage persistence.

**Solution:**
```jsx
import { useState, useEffect } from "react";

function DarkModeToggle() {
  const [darkMode, setDarkMode] = useState(() => {
    return localStorage.getItem("darkMode") === "true";
  });

  useEffect(() => {
    document.body.classList.toggle("dark-mode", darkMode);
    localStorage.setItem("darkMode", darkMode);
  }, [darkMode]);

  return <button onClick={() => setDarkMode((prev) => !prev)}>Toggle Dark Mode</button>;
}
```

---

### **4. Build a Custom Hook for Fetching Data**
**Problem:** Implement `useFetch` for reusable data fetching.

**Solution:**
```jsx
import { useState, useEffect } from "react";

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false));
  }, [url]);

  return { data, loading, error };
}

// Usage
function Users() {
  const { data, loading, error } = useFetch("https://jsonplaceholder.typicode.com/users");

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error loading data</p>;

  return <ul>{data.map((user) => <li key={user.id}>{user.name}</li>)}</ul>;
}
```

---

### **5. Implement a Modal Using Portals**
**Problem:** Create a modal that renders outside the main component tree.

**Solution:**
```jsx
import ReactDOM from "react-dom";

function Modal({ isOpen, onClose, children }) {
  if (!isOpen) return null;

  return ReactDOM.createPortal(
    <div className="modal-overlay" onClick={onClose}>
      <div className="modal-content" onClick={(e) => e.stopPropagation()}>
        {children}
        <button onClick={onClose}>Close</button>
      </div>
    </div>,
    document.getElementById("modal-root")
  );
}

// Usage
function App() {
  const [open, setOpen] = useState(false);
  return (
    <>
      <button onClick={() => setOpen(true)}>Open Modal</button>
      <Modal isOpen={open} onClose={() => setOpen(false)}>Hello, Modal!</Modal>
    </>
  );
}
```

---

### **6. Create a Reusable Toast Notification System**
**Problem:** Build a toast system to show notifications.

**Solution:**
```jsx
import { useState } from "react";

function useToast() {
  const [messages, setMessages] = useState([]);

  const addToast = (message) => {
    setMessages((prev) => [...prev, message]);
    setTimeout(() => setMessages((prev) => prev.slice(1)), 3000);
  };

  return { messages, addToast };
}

// Usage
function App() {
  const { messages, addToast } = useToast();

  return (
    <>
      <button onClick={() => addToast("New Notification!")}>Show Toast</button>
      <div className="toast-container">
        {messages.map((msg, i) => <div key={i} className="toast">{msg}</div>)}
      </div>
    </>
  );
}
```

---

### **7. Build a Todo List with Local Storage**
**Problem:** Implement a simple todo list that persists.

**Solution:**
```jsx
import { useState, useEffect } from "react";

function TodoApp() {
  const [todos, setTodos] = useState(() => JSON.parse(localStorage.getItem("todos")) || []);

  useEffect(() => localStorage.setItem("todos", JSON.stringify(todos)), [todos]);

  return (
    <>
      <input onKeyDown={(e) => e.key === "Enter" && setTodos([...todos, e.target.value])} />
      <ul>{todos.map((todo, i) => <li key={i}>{todo}</li>)}</ul>
    </>
  );
}
```

---

### **8. Implement a Counter with useReducer**
**Problem:** Use `useReducer` instead of `useState`.

**Solution:**
```jsx
import { useReducer } from "react";

function counterReducer(state, action) {
  switch (action.type) {
    case "increment": return state + 1;
    case "decrement": return state - 1;
    default: return state;
  }
}

function Counter() {
  const [count, dispatch] = useReducer(counterReducer, 0);

  return (
    <>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <span>{count}</span>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
    </>
  );
}
```

---

### **9. Implement a Search Bar with Filtering**
**Problem:** Filter list items dynamically as the user types.

**Solution:**
```jsx
import { useState } from "react";

function SearchableList() {
  const items = ["Apple", "Banana", "Cherry", "Date", "Fig"];
  const [query, setQuery] = useState("");

  return (
    <>
      <input onChange={(e) => setQuery(e.target.value.toLowerCase())} />
      <ul>{items.filter((item) => item.toLowerCase().includes(query)).map((item, i) => <li key={i}>{item}</li>)}</ul>
    </>
  );
}
```

---

### **10. Implement a Theme Switcher with Context API**
**Problem:** Toggle between dark and light themes.

**Solution:**
```jsx
const ThemeContext = React.createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");
  return (
    <ThemeContext.Provider value={{ theme, toggle: () => setTheme((t) => (t === "light" ? "dark" : "light")) }}>
      {children}
    </ThemeContext.Provider>
  );
}

// Usage
function App() {
  const { theme, toggle } = useContext(ThemeContext);
  return <button onClick={toggle}>Toggle Theme (Current: {theme})</button>;
}
```

Here are **5 additional problem-solving React challenges** covering **Parent-Child Communication, Interceptors, Authentication, and Axios HTTP calls**:

---

## **11. Parent-Child Communication using Callbacks**
**Problem:** Pass data from a child component to a parent.

**Solution:**
```jsx
function Child({ sendData }) {
  return <button onClick={() => sendData("Hello from Child")}>Send Data</button>;
}

function Parent() {
  const handleData = (data) => alert(data);
  return <Child sendData={handleData} />;
}
```
✅ **Key Concept:** The parent passes a **callback function** (`sendData`), and the child calls it.

---

## **12. Parent-Child Communication using Context API**
**Problem:** Share state between multiple components without prop drilling.

**Solution:**
```jsx
import { createContext, useContext, useState } from "react";

const ThemeContext = createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");
  return (
    <ThemeContext.Provider value={{ theme, toggle: () => setTheme(t => t === "light" ? "dark" : "light") }}>
      {children}
    </ThemeContext.Provider>
  );
}

function Child() {
  const { theme, toggle } = useContext(ThemeContext);
  return <button onClick={toggle}>Toggle Theme (Current: {theme})</button>;
}

function Parent() {
  return (
    <ThemeProvider>
      <Child />
    </ThemeProvider>
  );
}
```
✅ **Key Concept:** Context API enables **global state management** without prop drilling.

---

## **13. Axios Interceptor for API Calls**
**Problem:** Intercept requests and responses to handle errors and authentication.

**Solution:**
```jsx
import axios from "axios";

// Create an instance
const api = axios.create({ baseURL: "https://api.example.com" });

// Request Interceptor
api.interceptors.request.use(
  (config) => {
    config.headers.Authorization = `Bearer ${localStorage.getItem("token")}`;
    return config;
  },
  (error) => Promise.reject(error)
);

// Response Interceptor
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response.status === 401) {
      console.log("Unauthorized! Redirecting to login...");
    }
    return Promise.reject(error);
  }
);

// Usage
async function fetchData() {
  try {
    const { data } = await api.get("/users");
    console.log(data);
  } catch (error) {
    console.error("API Error:", error);
  }
}
```
✅ **Key Concept:** Interceptors allow modifying requests before they are sent and handling errors globally.

---

## **14. Authentication with JWT Tokens**
**Problem:** Implement login/logout with JWT-based authentication.

**Solution:**
```jsx
import { useState } from "react";
import axios from "axios";

function AuthComponent() {
  const [token, setToken] = useState(localStorage.getItem("token"));

  const login = async () => {
    const { data } = await axios.post("https://api.example.com/login", { username: "user", password: "pass" });
    localStorage.setItem("token", data.token);
    setToken(data.token);
  };

  const logout = () => {
    localStorage.removeItem("token");
    setToken(null);
  };

  return (
    <>
      {token ? (
        <>
          <p>Logged in</p>
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <button onClick={login}>Login</button>
      )}
    </>
  );
}
```
✅ **Key Concept:** JWT tokens are stored in `localStorage` and used for authentication.

---

## **15. Make HTTP Requests with Axios in React**
**Problem:** Fetch data from an API using `axios` with error handling.

**Solution:**
```jsx
import { useState, useEffect } from "react";
import axios from "axios";

function UsersList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    axios.get("https://jsonplaceholder.typicode.com/users")
      .then((res) => setUsers(res.data))
      .catch((err) => setError(err.message))
      .finally(() => setLoading(false));
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;

  return <ul>{users.map((user) => <li key={user.id}>{user.name}</li>)}</ul>;
}
```
✅ **Key Concept:** `axios` simplifies HTTP requests, with built-in error handling.

---

### **🔹 Summary of Concepts Covered:**
1. **Parent-Child Communication**
   - Using **callbacks**
   - Using **Context API**
2. **Axios Interceptors**
   - Automatically attach **auth headers**.
   - Handle **global API errors**.
3. **Authentication**
   - JWT-based **login/logout**.
4. **HTTP API Calls**
   - Fetching data with **error handling**.

🚀 Let me know if you need more advanced problems!

---

## **16. Implement Stopwatch (Start, Stop, Reset + live Timer)**
**Problem:** Stopwatch.

**Solution:**
```jsx

import React, { useState, useEffect, useRef } from "react";

export default function App() {
  const [swTime, setSwTime] = useState(0);
  const [swRunning, setSwRunning] = useState(false);
  const swIntervalRef = useRef(null);

  useEffect(() => {
    if (swRunning) {
      swIntervalRef.current = setInterval(() => {
        setSwTime((prev) => prev + 10);
      }, 10);
    } else {
      clearInterval(swIntervalRef.current);
    }
    return () => clearInterval(swIntervalRef.current);
  }, [swRunning]);

  const formatSwTime = (time) => {
    const minutes = Math.floor(time / 60000);
    const seconds = Math.floor((time % 60000) / 1000);
    const milliseconds = Math.floor((time % 1000) / 10);
    return `${minutes.toString().padStart(2, "0")}:${seconds
      .toString()
      .padStart(2, "0")}.${milliseconds.toString().padStart(2, "0")}`;
  };

  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h1>Hello world</h1>
        
      <h2> Stopwatch</h2>
      <div style={{ fontSize: "2em", margin: "20px" }}>{formatSwTime(swTime)}</div>
      <button onClick={() => setSwRunning(true)}>Start</button>
      <button onClick={() => setSwRunning(false)}>Pause</button>
      <button onClick={() => { setSwTime(0); setSwRunning(false); }}>Reset</button>
    </div>
  );
}
```
---
## **17. Build a Debounced Search with API Call**
**Problem:** Create a search input that.
 - Calls API after **300ms debounce**.
 - Cancels previous requests
 - Shows loading state

**Solution:**
```jsx

import { useEffect, useState } from "react";

function Search() {
  const [query, setQuery] = useState("");
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    if (!query) return;

    const controller = new AbortController();
    const timer = setTimeout(async () => {
      setLoading(true);
      try {
        const res = await fetch(
          `https://api.example.com/search?q=${query}`,
          { signal: controller.signal }
        );
        const result = await res.json();
        setData(result);
      } catch (err) {
        if (err.name !== "AbortError") console.error(err);
      } finally {
        setLoading(false);
      }
    }, 300);

    return () => {
      clearTimeout(timer);
      controller.abort();
    };
  }, [query]);

  return (
    <input onChange={(e) => setQuery(e.target.value)} />
  );
}
```

---
