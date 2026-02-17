# 📘 Debounce and Throttle 
---

# 1️⃣ What is Debounce?

- **Debounce** ensures a function is called **only after a certain delay** has passed since the **last time it was invoked**.  
- Commonly used for **search input, resize, scroll** events to reduce frequent calls.  

**Use Case:**  
- Search input: wait for user to stop typing before making an API call.  

**Example:**

```js
function debounce(fn, delay) {
  let timer;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

// Usage
const searchInput = document.getElementById('search');
searchInput.addEventListener('input', debounce((e) => {
  console.log('API Call:', e.target.value);
}, 300));
```

**Key Points:**  
- Waits for inactivity  
- Reduces API calls and improves performance  

---

# 2️⃣ What is Throttle?

- **Throttle** ensures a function is called **at most once in a specified interval**, regardless of how many times the event occurs.  
- Commonly used for **scroll, resize, or mouse move events** to limit frequent execution.  

**Use Case:**  
- Infinite scrolling: update scroll position **at most once per 200ms**.  

**Example:**

```js
function throttle(fn, limit) {
  let lastCall = 0;
  return function(...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
}

// Usage
window.addEventListener('scroll', throttle(() => {
  console.log('Scroll event processed');
}, 200));
```

**Key Points:**  
- Executes function at regular intervals  
- Limits performance overhead for frequent events  

---

# 3️⃣ Difference Between Debounce and Throttle

| Feature | Debounce | Throttle |
|---------|---------|----------|
| Execution | After delay from last call | At most once per interval |
| Use Case | User input, search boxes | Scroll, resize, mouse move |
| Function Calls | Fewer, only after inactivity | Regular, limited calls |
| Example | `debounce(fetchData, 300)` | `throttle(handleScroll, 200)` |

---

# 4️⃣ Advanced Debounce / Throttle Patterns

### Leading vs Trailing Calls

```js
// Debounce with leading call
function debounce(fn, delay, immediate = false) {
  let timer;
  return function(...args) {
    const callNow = immediate && !timer;
    clearTimeout(timer);
    timer = setTimeout(() => timer = null, delay);
    if (callNow) fn.apply(this, args);
  };
}
```

- `immediate = true` → call at **start of event**  
- `immediate = false` → call at **end of event** (default)  

---

# 5️⃣ Most Asked Interview Questions

1. What is the difference between **debounce and throttle**?  
2. Give examples of when to use **debounce** vs **throttle**  
3. How would you implement **debounce** in JavaScript?  
4. How would you implement **throttle** in JavaScript?  
5. Explain **leading vs trailing calls** in debounce/throttle  
6. Performance benefits of debounce/throttle in real applications  
7. Difference between **throttle with timeout vs timestamp** implementation  

---

# 6️⃣ Tips for Senior-Level Interviews

- Always discuss **performance benefits**  
- Be ready to **write implementations from scratch**  
- Explain **use cases in UI/UX optimization**  
- Compare **debounce vs throttle in infinite scroll vs search**  
- Mention **leading vs trailing call differences**  

---


---

# 🎯 Senior-Level Takeaway

- **Debounce:** delay execution until inactivity  
- **Throttle:** limit execution frequency  
- Both improve **performance for frequent events**  
- Mastering these patterns is crucial for **real-world JS performance optimization**  

---

End of Notes
