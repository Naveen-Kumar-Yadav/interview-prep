# 📘 JavaScript Promise Polyfills & Implementations  
## (Senior Level – 6+ Years Experience)

---

# 1️⃣ Why Polyfills?

- Sometimes we need to support older browsers or environments without native Promises.  
- Polyfills mimic native behavior.  
- Useful for **interviews** to demonstrate understanding of Promise mechanics.

---

# 2️⃣ Minimal Promise Polyfill (Basic)

```js
class MyPromise {
  constructor(executor) {
    this.state = "pending";
    this.value = undefined;
    this.handlers = [];

    const resolve = (value) => {
      this.updateResult(value, "fulfilled");
    };

    const reject = (reason) => {
      this.updateResult(reason, "rejected");
    };

    try {
      executor(resolve, reject);
    } catch (err) {
      reject(err);
    }
  }

  updateResult(value, state) {
    if (this.state !== "pending") return;
    this.state = state;
    this.value = value;
    this.executeHandlers();
  }

  executeHandlers() {
    if (this.state === "pending") return;
    this.handlers.forEach((handler) => {
      if (this.state === "fulfilled" && handler.onFulfilled) {
        handler.onFulfilled(this.value);
      }
      if (this.state === "rejected" && handler.onRejected) {
        handler.onRejected(this.value);
      }
    });
    this.handlers = [];
  }

  then(onFulfilled, onRejected) {
    return new MyPromise((resolve, reject) => {
      this.handlers.push({
        onFulfilled: (val) => {
          try {
            if (!onFulfilled) return resolve(val);
            resolve(onFulfilled(val));
          } catch (err) {
            reject(err);
          }
        },
        onRejected: (err) => {
          try {
            if (!onRejected) return reject(err);
            resolve(onRejected(err));
          } catch (e) {
            reject(e);
          }
        },
      });
      this.executeHandlers();
    });
  }

  catch(onRejected) {
    return this.then(null, onRejected);
  }

  static resolve(value) {
    return new MyPromise((resolve) => resolve(value));
  }

  static reject(reason) {
    return new MyPromise((_, reject) => reject(reason));
  }
}
```

---

# 3️⃣ Polyfill: `Promise.all`

```js
MyPromise.all = function(promises) {
  return new MyPromise((resolve, reject) => {
    let results = [];
    let completed = 0;

    if (promises.length === 0) resolve([]);

    promises.forEach((p, index) => {
      MyPromise.resolve(p)
        .then(value => {
          results[index] = value;
          completed++;
          if (completed === promises.length) resolve(results);
        })
        .catch(reject);
    });
  });
};
```

Usage:

```js
MyPromise.all([MyPromise.resolve(1), MyPromise.resolve(2)])
  .then(console.log); // [1, 2]
```

---

# 4️⃣ Polyfill: `Promise.race`

```js
MyPromise.race = function(promises) {
  return new MyPromise((resolve, reject) => {
    promises.forEach(p => {
      MyPromise.resolve(p).then(resolve).catch(reject);
    });
  });
};
```

---

# 5️⃣ Polyfill: `Promise.any`

```js
MyPromise.any = function(promises) {
  return new MyPromise((resolve, reject) => {
    let rejectedCount = 0;
    const errors = [];

    promises.forEach((p, i) => {
      MyPromise.resolve(p).then(resolve).catch(err => {
        errors[i] = err;
        rejectedCount++;
        if (rejectedCount === promises.length) reject(errors);
      });
    });
  });
};
```

---

# 6️⃣ Polyfill: `Promise.allSettled`

```js
MyPromise.allSettled = function(promises) {
  return new MyPromise((resolve) => {
    let results = [];
    let completed = 0;

    if (promises.length === 0) resolve([]);

    promises.forEach((p, index) => {
      MyPromise.resolve(p)
        .then(value => results[index] = { status: "fulfilled", value })
        .catch(reason => results[index] = { status: "rejected", reason })
        .finally(() => {
          completed++;
          if (completed === promises.length) resolve(results);
        });
    });
  });
};
```

---

# 7️⃣ Notes for Interviews

- Demonstrates **deep understanding** of:
  - Promise states (pending, fulfilled, rejected)
  - Async execution with **microtasks**
  - Chaining (`then`) and error propagation
- Can be extended to handle:
  - `finally`
  - Cancellation
  - Timeout wrappers
- Good for **senior-level coding questions**.

---

# 8️⃣ Bonus: Retry with Polyfill

```js
function retry(fn, retries = 3) {
  return new MyPromise((resolve, reject) => {
    function attempt() {
      fn().then(resolve).catch(err => {
        if (retries-- > 0) attempt();
        else reject(err);
      });
    }
    attempt();
  });
}
```

---

# 🚀 Suggested GitHub Structure

```
/javascript
    promise-notes.md
    promise-polyfills.md
    async-await-notes.md
    event-loop.md
```

---

# 🎯 Senior-Level Takeaway

- Polyfills show mastery of **internal mechanics**  
- Great for **interviews, legacy support, and learning internals**  
- Always understand **microtasks vs macrotasks** while building polyfills  

---

End of Notes

