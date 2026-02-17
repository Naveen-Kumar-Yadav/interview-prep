# 📘 JavaScript Event Loop – Complete Notes  
## (Senior Level – 6+ Years Experience)

---

# 1️⃣ JavaScript Concurrency Model

JavaScript is:

- Single-threaded
- Non-blocking
- Asynchronous
- Uses **Event Loop** to handle async tasks

Key Components:

1. **Call Stack** – Executes functions
2. **Web APIs / Node APIs** – Handles async tasks
3. **Task Queues** – Holds callbacks
   - **Microtask Queue** (Promises, queueMicrotask, MutationObserver)
   - **Macrotask Queue** (setTimeout, setInterval, setImmediate, I/O)
4. **Event Loop** – Moves tasks from queues to call stack

---

# 2️⃣ Microtasks vs Macrotasks

| Feature | Microtask | Macrotask |
|---------|-----------|-----------|
| Examples | Promise.then, queueMicrotask | setTimeout, setInterval, setImmediate, I/O |
| Priority | High | Low |
| Executes | After current execution stack | After microtasks complete |

---

# 3️⃣ Event Loop Execution Flow

1. Execute **call stack** until empty
2. Process **all microtasks**
3. Take the first **macrotask** from the queue
4. Repeat

---

# 4️⃣ Example: Execution Order

```js
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

Promise.resolve().then(() => console.log("Promise"));

console.log("End");
```

### Output

```
Start
End
Promise
Timeout
```

**Explanation:**

1. Synchronous code runs first → "Start" & "End"
2. Promise callback goes to microtask queue → runs after current stack → "Promise"
3. setTimeout goes to macrotask queue → runs after microtasks → "Timeout"

---

# 5️⃣ Nested Microtasks

```js
Promise.resolve()
  .then(() => {
    console.log("First");
    Promise.resolve().then(() => console.log("Second"));
  })
  .then(() => console.log("Third"));
```

### Output

```
First
Second
Third
```

✅ Microtasks added during microtask execution are processed before moving to the next macrotask.

---

# 6️⃣ Microtask Starvation

```js
function loop() {
  Promise.resolve().then(loop);
}
loop();
```

- Microtasks keep adding themselves
- Macrotasks (like setTimeout) may never run
- Causes **starvation**

---

# 7️⃣ Node.js Event Loop Phases

| Phase | Description |
|-------|-------------|
| timers | setTimeout, setInterval callbacks |
| pending callbacks | I/O callbacks deferred to next loop |
| idle, prepare | Internal |
| poll | Retrieves new I/O events; executes I/O callbacks |
| check | setImmediate callbacks |
| close callbacks | socket.on('close') |

**Note:** Microtasks are executed **after each phase**, before moving to the next phase.

---

# 8️⃣ Synchronous vs Asynchronous

- **Synchronous** – runs immediately, blocks stack  
- **Asynchronous** – uses callbacks, promises, timers, does **not block**

---

# 9️⃣ Promise vs setTimeout Example

```js
console.log("Start");

setTimeout(() => console.log("setTimeout"), 0);

Promise.resolve().then(() => console.log("Promise"));

console.log("End");
```

Output:

```
Start
End
Promise
setTimeout
```

---

# 🔟 Event Loop with Async/Await

```js
async function run() {
  console.log("A");
  await Promise.resolve();
  console.log("B");
}

console.log("Start");
run();
console.log("End");
```

### Output

```
Start
A
End
B
```

- `await` pauses inside async function
- Microtask executes after current synchronous code

---

# 1️⃣1️⃣ Real-World Senior-Level Considerations

- Prevent **microtask starvation**
- Avoid memory leaks in long-running async loops
- Optimize heavy computation (Web Workers / Worker Threads)
- Understand concurrency limits in I/O
- Predict execution order in **nested promises + timers** for interviews

---

# 1️⃣2️⃣ Interview Tricky Questions

1. Explain microtask vs macrotask execution order  
2. Predict outputs of nested Promises and setTimeout  
3. Difference between process.nextTick(), setImmediate(), setTimeout(0) in Node.js  
4. What happens if microtasks schedule more microtasks?  
5. How async/await works under the hood  
6. Explain starvation and how to avoid it  
7. Difference between browser event loop vs Node.js event loop

---

# 🚀 Suggested GitHub Structure

```
/javascript
    event-loop.md
    async-await-notes.md
    promise-notes.md
    promise-polyfills.md
```

---

# 🎯 Takeaway

- Understand **event loop phases**
- Master **microtask vs macrotask**
- Be able to **predict output** of tricky async code
- Discuss **performance and memory implications** in senior interviews

---

End of Notes
