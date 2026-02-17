# 📘 JavaScript Generators – Complete Notes  
## (Senior Level – 6+ Years Experience)

---

# 1️⃣ What is a Generator?

- A **generator function** can **pause** and **resume** execution.  
- Introduced in **ES6**.  
- Uses the `function*` syntax.  

```js
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

const g = gen();
console.log(g.next()); // { value: 1, done: false }
console.log(g.next()); // { value: 2, done: false }
console.log(g.next()); // { value: 3, done: false }
console.log(g.next()); // { value: undefined, done: true }
```

---

# 2️⃣ Key Concepts

- **yield**: pauses execution and returns value  
- **.next(value)**: resumes generator, optionally passing value back  
- **done**: indicates if generator is finished  
- Generators are **iterables**, can be used in `for...of`

```js
for (const val of gen()) {
  console.log(val);
}
```

---

# 3️⃣ Passing Values Back

```js
function* gen() {
  const x = yield 10;
  console.log(x);
  const y = yield 20;
  console.log(y);
}

const g = gen();
g.next();       // starts, yields 10
g.next(100);    // resumes, logs 100, yields 20
g.next(200);    // resumes, logs 200
```

---

# 4️⃣ Throwing Errors Inside Generators

```js
function* gen() {
  try {
    yield 1;
  } catch (err) {
    console.log("Caught:", err);
  }
}

const g = gen();
g.next();
g.throw(new Error("Oops")); // "Caught: Error: Oops"
```

- Errors can be **injected** into the generator using `.throw()`

---

# 5️⃣ Generators + Promises (Async Precursor)

Before async/await, generators + Promises were used for async control flow:

```js
function* fetchFlow() {
  const data = yield fetch("api/data");
  console.log(data);
}

// Using a runner function to handle the generator
function run(generator) {
  const g = generator();

  function step(nextVal) {
    const result = g.next(nextVal);
    if (!result.done) {
      result.value.then(step);
    }
  }

  step();
}

run(fetchFlow);
```

- **Async/Await** is syntactic sugar over this pattern  

---

# 6️⃣ Generators vs Async/Await

| Feature | Generator | Async/Await |
|---------|-----------|-------------|
| Control Flow | Manual, iterator-based | Synchronous-looking |
| Return Value | Iterator object | Promise |
| Error Handling | .throw() | try/catch |
| Use Case | Custom iteration, pre-async control | Async operations |

---

# 7️⃣ Infinite Generators

Useful for producing **streams of data**:

```js
function* idGenerator() {
  let id = 1;
  while (true) {
    yield id++;
  }
}

const gen = idGenerator();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

---

# 8️⃣ Generators for Lazy Evaluation

```js
function* numbers(limit) {
  for (let i = 1; i <= limit; i++) {
    yield i * 2; // compute only when needed
  }
}

for (const n of numbers(5)) {
  console.log(n);
}
```

- Efficient for **large data sets** or **infinite sequences**  

---

# 9️⃣ Composing Generators

```js
function* a() { yield 1; yield 2; }
function* b() { yield* a(); yield 3; }

const g = b();
console.log([...g]); // [1, 2, 3]
```

- `yield*` delegates to another generator

---

# 🔟 Interview Tips – Generators

1. Explain **yield, next(), done**  
2. Demonstrate **passing values back to generator**  
3. Show **error injection** with `.throw()`  
4. Compare **Generators vs Async/Await**  
5. Use for **lazy evaluation & infinite sequences**  
6. Discuss **delegation with yield***  

---

# 🚀 Suggested GitHub Structure

```
/javascript
    generators.md
    async-await-notes.md
    async-await-interview-questions.md
    promise-notes.md
    promise-polyfills.md
    event-loop.md
```

---

# 🎯 Senior-Level Takeaway

- Generators give **manual control** over function execution  
- They are **iterable** and can be **paused/resumed**  
- Core concept behind **async/await** implementation  
- Must understand **delegation, value injection, and error handling**  

---

End of Notes
