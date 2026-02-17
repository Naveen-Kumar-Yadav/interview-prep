# 📘 Async/Await – Most Asked Interview Questions & Answers  
## (Senior Level – 6+ Years Experience)

---

# 1️⃣ What is `async/await` in JavaScript?

**Answer:**  

- `async` functions always return a **Promise**.  
- `await` pauses execution of the async function until the Promise resolves.  
- Provides **synchronous-looking code** for asynchronous operations.  

```js
async function fetchData() {
  return "Hello";
}

fetchData().then(console.log); // Hello
```

---

# 2️⃣ Difference between `async/await` and Promises

| Feature | Promises | Async/Await |
|---------|----------|-------------|
| Syntax | .then() chaining | Synchronous-looking |
| Readability | Medium | High |
| Error Handling | .catch() | try/catch |
| Built On | Native | Promises |

---

# 3️⃣ Can `await` be used outside an `async` function?

**Answer:**  

- In **modules**, `await` can be used at the top level (Top-Level Await).  
- Otherwise, **await must be inside an `async` function**, otherwise it throws a SyntaxError.

```js
// Top-level await (ES Modules)
const data = await fetch("https://api.com");
```

---

# 4️⃣ How does `async/await` work under the hood?

- `async` functions **return a Promise**.  
- `await` pauses execution and schedules a **microtask**.  
- Equivalent to a **generator function + Promise wrapper** in ES6.  

```js
async function fn() { return 10; }
```

is equivalent to:

```js
function fn() {
  return Promise.resolve(10);
}
```

---

# 5️⃣ Sequential vs Parallel Execution

### Sequential (Slower)
```js
const a = await task1();
const b = await task2();
```

### Parallel (Faster)
```js
const [a, b] = await Promise.all([task1(), task2()]);
```

**Tip:** Always consider performance in loops or multiple async calls.

---

# 6️⃣ How to handle errors with Async/Await?

**Answer:** Use `try/catch` or `Promise.allSettled` for multiple promises.

```js
try {
  const result = await asyncTask();
} catch (err) {
  console.error(err);
}
```

---

# 7️⃣ How to handle multiple async tasks with partial failures?

```js
const results = await Promise.allSettled([task1(), task2(), task3()]);

results.forEach(result => {
  if (result.status === "fulfilled") console.log("Success:", result.value);
  else console.log("Failure:", result.reason);
});
```

- Avoids breaking the entire batch if one promise fails.

---

# 8️⃣ Can we cancel an async function?

**Answer:**  

- Native async functions **cannot be cancelled** directly.  
- Use **AbortController** or **flags** to implement cancellation.

```js
const controller = new AbortController();
fetch("url", { signal: controller.signal });
// Cancel: controller.abort();
```

---

# 9️⃣ What is the difference between `return await` and `return`?

```js
async function fn() {
  return await Promise.resolve(10);
}
```

- **`return await`**: waits for resolution, allows try/catch to catch errors.  
- **`return Promise`**: returns promise directly, errors are caught by caller.  

**Interview Tip:** Use `return await` inside try/catch, otherwise skip it for performance.

---

# 🔟 Common Mistakes with Async/Await

1. Sequential `await` inside loops → slow execution  
2. Not using `try/catch` → unhandled promise rejections  
3. Using `await` outside async function (syntax error)  
4. Expecting `async` functions to block main thread → they don’t  
5. Forgetting to combine with `Promise.all` for parallel execution  

---

# 1️⃣1️⃣ Retry Pattern with Async/Await

```js
async function retry(fn, retries = 3) {
  try {
    return await fn();
  } catch (err) {
    if (retries === 0) throw err;
    return retry(fn, retries - 1);
  }
}
```

- Useful for **network requests** and **unstable APIs**  

---

# 1️⃣2️⃣ Interview Trick Question: Execution Order

```js
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

Promise.resolve().then(() => console.log("Promise"));

async function run() {
  console.log("A");
  await Promise.resolve();
  console.log("B");
}

run();
console.log("End");
```

**Output:**

```
Start
A
End
Promise
B
Timeout
```

**Explanation:**  
- `run()` starts and prints `A`  
- `await` schedules microtask → `B` runs after current stack  
- Promise microtask runs before next macrotask (`setTimeout`)

---

# 1️⃣3️⃣ Best Practices (Senior Level)

- Avoid sequential `await` in loops → use `Promise.all`  
- Always handle errors with `try/catch`  
- Understand microtasks vs macrotasks  
- Combine with **cancellation** and **timeout patterns** for production code  
- Explain **internal mechanics** in interviews (how async/await uses promises under the hood)  

---

# 🚀 Suggested GitHub Structure

```
/javascript
    async-await-interview-questions.md
    async-await-notes.md
    promise-notes.md
    promise-polyfills.md
    event-loop.md
    generators.md
```

---

# 🎯 Senior-Level Takeaway

- Know the **execution order**, microtask queue behavior  
- Explain **performance trade-offs**  
- Be ready for **nested async/await + promises + timers** tricky questions  
- Show **real-world usage** like retries, partial failures, parallel execution  

---

End of Notes
