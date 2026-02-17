# 📘 JavaScript Interview Questions & Answers  
## (Senior Level – 6+ Years Experience)

---

# 1️⃣ Scope & Hoisting

**Q1. What is the difference between var, let, and const?**

- `var`: function-scoped, can be redeclared, hoisted with `undefined`  
- `let`: block-scoped, cannot redeclare in same scope, not initialized before declaration  
- `const`: block-scoped, cannot redeclare or reassign, must be initialized  

**Q2. Explain Hoisting**

- Declarations are moved to the top of their scope before execution  
- Only declarations are hoisted, not initializations  

```js
console.log(a); // undefined
var a = 10;

console.log(b); // ReferenceError
let b = 20;
```

---

# 2️⃣ Closures

**Q3. What is a closure?**

- A function that **remembers variables from its outer scope** even after the outer function finishes

```js
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  };
}
const counter = outer();
console.log(counter()); // 1
```

**Q4. Common closure pitfalls in loops**

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// Output: 3,3,3
```

**Fix with `let`**

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// Output: 0,1,2
```

---

# 3️⃣ `this` Keyword

**Q5. Explain `this` in JavaScript**

- `this` refers to **execution context**  
- In global scope → `window` (browser), `global` (Node.js)  
- In object method → the object itself  
- In constructor → the new instance  

**Q6. Arrow function and `this`**

- Arrow functions **do not have their own `this`**, they inherit from the outer scope  

```js
const obj = {
  x: 10,
  arrow: () => console.log(this.x)
};
obj.arrow(); // undefined
```

---

# 4️⃣ Call, Apply, Bind

**Q7. Difference between call, apply, bind**

```js
function greet(greeting, name) {
  console.log(greeting + ", " + name);
}

greet.call(this, "Hello", "Alice"); // Hello, Alice
greet.apply(this, ["Hi", "Bob"]);   // Hi, Bob
const bound = greet.bind(this, "Hey");
bound("Charlie");                    // Hey, Charlie
```

- `call` → invoke function with arguments  
- `apply` → invoke function with array of arguments  
- `bind` → returns a new function with bound `this`  

---

# 5️⃣ Prototype & Inheritance

**Q8. Difference between `__proto__` and `prototype`**

- `prototype` → object attached to **function constructor**  
- `__proto__` → reference to the **prototype of the object instance**  

**Q9. How does inheritance work in JS?**

```js
function Parent() { this.name = "Parent"; }
Parent.prototype.sayHi = function() { console.log("Hi"); }

function Child() { Parent.call(this); }
Child.prototype = Object.create(Parent.prototype);
Child.prototype.constructor = Child;

const c = new Child();
c.sayHi(); // Hi
```

---

# 6️⃣ Async JavaScript

**Q10. Difference between Promises and Async/Await**

- Promises → `.then()` chaining  
- Async/Await → synchronous-looking syntax, built on Promises  

**Q11. Common Async Patterns**

- `Promise.all` → run in parallel, fail fast  
- `Promise.allSettled` → get results of all  
- `Promise.race` → first resolved/rejected  
- Retry pattern:

```js
async function retry(fn, retries = 3) {
  try { return await fn(); } 
  catch (err) { if (retries-- > 0) return retry(fn, retries); else throw err; }
}
```

---

# 7️⃣ Event Loop & Microtasks

**Q12. Execution Order Example**

```js
console.log("Start");
setTimeout(() => console.log("Timeout"), 0);
Promise.resolve().then(() => console.log("Promise"));
console.log("End");
```

**Output:**

```
Start
End
Promise
Timeout
```

- Synchronous → microtasks → macrotasks  

**Q13. Node.js Phases**

- timers → I/O → check → close  
- Microtasks executed **after each phase**  

---

# 8️⃣ Generators

**Q14. What is a Generator?**

- Function that can **pause and resume** using `yield`  
- Returns **iterator**

```js
function* gen() { yield 1; yield 2; }
const g = gen();
console.log(g.next().value); // 1
```

**Q15. Delegating Generators**

```js
function* a() { yield 1; yield 2; }
function* b() { yield* a(); yield 3; }
console.log([...b()]); // [1,2,3]
```

---

# 9️⃣ ES6 Features

- `let`, `const`, template literals  
- Arrow functions, default parameters  
- Destructuring, spread/rest operators  
- Classes, modules  
- Map, Set, WeakMap, WeakSet  
- Symbols, iterators, generators  

---

# 🔟 Memory Management & Garbage Collection

- JS uses **automatic garbage collection**  
- Closures can **retain memory** → possible memory leaks  
- Avoid global variables and long-lived references  

---

# 1️⃣1️⃣ Advanced Patterns

- **Currying**

```js
const add = a => b => c => a+b+c;
console.log(add(1)(2)(3)); // 6
```

- **Memoization**

```js
const memo = fn => { const cache = {}; return x => cache[x] || (cache[x] = fn(x)); }
```

- **Module Pattern**

```js
const module = (function() {
  let secret = 0;
  return { inc: () => ++secret, get: () => secret };
})();
```

---

# 1️⃣2️⃣ Most Asked Interview Questions

1. Explain closures with examples  
2. Difference between `var`, `let`, `const`  
3. Hoisting and temporal dead zone  
4. Explain `this` and arrow functions  
5. Call, Apply, Bind differences  
6. Prototype vs `__proto__`  
7. Promise vs Async/Await  
8. Event Loop & microtasks  
9. Generators and yield*  
10. Currying, memoization, module pattern  
11. Sequential vs parallel async execution  
12. Top-level await and async function pitfalls  
13. Closure memory leak scenarios  
14. Predict tricky async outputs (Promises + setTimeout + async/await)

---
---


