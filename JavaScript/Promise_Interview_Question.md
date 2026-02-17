# 📘 JavaScript Promise  
## (Interview Ready – 6+ Years Experience)

---

# 1️⃣ What is a Promise?

A Promise is an object that represents the eventual completion or failure of an asynchronous operation.

It has 3 states:

- pending
- fulfilled
- rejected

---

# 2️⃣ Basic Syntax

```js
const promise = new Promise((resolve, reject) => {
  const success = true;

  if (success) {
    resolve("Operation Successful");
  } else {
    reject("Operation Failed");
  }
});
```

---

# 3️⃣ Promise States Lifecycle

- Starts as **pending**
- Moves to **fulfilled** OR **rejected**
- Once settled → state cannot change (immutable)

---

# 4️⃣ Consuming a Promise

```js
promise
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.error(error);
  })
  .finally(() => {
    console.log("Completed");
  });
```

---

# 5️⃣ Promise Chaining

Each `.then()` returns a new Promise.

```js
Promise.resolve(5)
  .then(val => val * 2)
  .then(val => val + 1)
  .then(console.log);
```

Output:
```
11
```

---

# 6️⃣ Important Rule

If you don’t return inside `.then()`:

```js
Promise.resolve(10)
  .then(val => { val + 5 }) 
  .then(console.log);
```

Output:
```
undefined
```

Because nothing was returned.

---

# 7️⃣ Error Propagation

Errors automatically bubble down the chain.

```js
Promise.resolve()
  .then(() => {
    throw new Error("Something went wrong");
  })
  .catch(err => console.log(err.message));
```

---

# 8️⃣ Promise Methods

---

## 1️⃣ Promise.resolve()

Creates a resolved Promise.

```js
Promise.resolve(100).then(console.log);
```

---

## 2️⃣ Promise.reject()

Creates a rejected Promise.

```js
Promise.reject("Error").catch(console.log);
```

---

## 3️⃣ Promise.all()

- Runs multiple promises in parallel
- Fails fast (rejects immediately if one fails)

```js
Promise.all([p1, p2, p3])
  .then(results => console.log(results))
  .catch(err => console.error(err));
```

---

## 4️⃣ Promise.allSettled()

Waits for all promises to complete.

```js
Promise.allSettled([p1, p2]);
```

Returns:

```js
[
  { status: "fulfilled", value: ... },
  { status: "rejected", reason: ... }
]
```

---

## 5️⃣ Promise.race()

Returns first settled Promise (resolve or reject).

```js
Promise.race([p1, p2]);
```

---

## 6️⃣ Promise.any()

Returns first fulfilled Promise.

Rejects only if all fail.

```js
Promise.any([p1, p2]);
```

---

# 9️⃣ Microtask Queue & Event Loop

Promise callbacks run in **Microtask Queue**.

Execution Order:

1. Call Stack
2. Microtask Queue
3. Macrotask Queue

Example:

```js
console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

Promise.resolve().then(() => console.log("Promise"));

console.log("End");
```

Output:
```
Start
End
Promise
Timeout
```

---

# 🔟 Promise Constructor Behavior

Important Interview Point:

```js
new Promise((resolve, reject) => {
  console.log("Runs immediately");
});
```

The executor function runs synchronously.

Only `.then()` callbacks are asynchronous.

---

# 1️⃣1️⃣ Promise Flattening

If `.then()` returns a Promise:

```js
Promise.resolve()
  .then(() => Promise.resolve(5))
  .then(console.log);
```

JavaScript automatically unwraps nested promises.

---

# 1️⃣2️⃣ Difference: Promise vs Async/Await

| Feature | Promise | Async/Await |
|----------|----------|--------------|
| Syntax | .then() chaining | Looks synchronous |
| Error Handling | .catch() | try/catch |
| Readability | Medium | High |
| Built On | Native | Built on Promises |

---

# 1️⃣3️⃣ Implement Promise.all (Polyfill)

```js
function myPromiseAll(promises) {
  return new Promise((resolve, reject) => {
    let results = [];
    let completed = 0;

    if (promises.length === 0) {
      resolve([]);
    }

    promises.forEach((promise, index) => {
      Promise.resolve(promise)
        .then(value => {
          results[index] = value;
          completed++;

          if (completed === promises.length) {
            resolve(results);
          }
        })
        .catch(reject);
    });
  });
}
```

---

# 1️⃣4️⃣ Retry Pattern

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

---

# 1️⃣5️⃣ Concurrency Control

Limit parallel execution:

```js
async function runWithLimit(tasks, limit) {
  const results = [];
  const executing = [];

  for (const task of tasks) {
    const p = task().then(res => {
      executing.splice(executing.indexOf(p), 1);
      return res;
    });

    results.push(p);
    executing.push(p);

    if (executing.length >= limit) {
      await Promise.race(executing);
    }
  }

  return Promise.all(results);
}
```

---

# 1️⃣6️⃣ Common Interview Questions

1. Why do Promises use microtask queue?
2. What happens if you resolve and reject both?
3. What if no catch is provided?
4. Difference between Promise.all and Promise.allSettled?
5. How to cancel a Promise?
6. What is promise chaining?
7. How does error propagation work?
8. What is promise flattening?

---

# 1️⃣7️⃣ Senior-Level Discussion Points (6+ Years)

Interviewers expect:

- Event loop deep knowledge
- Microtask vs Macrotask understanding
- Error handling strategies
- Performance implications
- Concurrency management
- Polyfill implementation
- Memory leak awareness

---

# 🚀 Suggested Repository Structure

```
/javascript
    promise-notes.md
    promise-polyfills.md
    async-await-notes.md
    event-loop.md
```

---

# 🎯 Final Takeaway

For senior interviews:

- Don’t just explain syntax
- Explain internal mechanics
- Explain performance trade-offs
- Explain real-world use cases
- Demonstrate concurrency thinking

---

End of Notes
