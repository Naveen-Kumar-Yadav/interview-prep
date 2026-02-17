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
# 1️⃣ Map vs Filter vs ForEach

| Method | Returns | Purpose | Mutation | Example |
|--------|--------|---------|---------|---------|
| `map` | New array | Transform each element | No | `[1,2,3].map(x => x*2)` → `[2,4,6]` |
| `filter` | New array | Filter elements based on condition | No | `[1,2,3].filter(x => x>1)` → `[2,3]` |
| `forEach` | undefined | Iterate for side-effects | Can mutate original array | `[1,2,3].forEach(x => console.log(x))` |

**Notes:**  
- Use `map` when you want a **new transformed array**  
- Use `filter` when you want a **subset**  
- Use `forEach` for **side-effects only**

---

# 2️⃣ For, For...in, For...of

| Loop | Iterates Over | Example | Notes |
|------|--------------|--------|------|
| `for` | Index (0..length-1) | `for(let i=0;i<arr.length;i++)` | Traditional loop |
| `for...in` | Keys / indices | `for(let key in obj)` | Iterates **enumerable properties** including prototype |
| `for...of` | Values | `for(let val of arr)` | Works with **iterables** (Array, Map, Set, String) |

**Example:**

```js
const arr = [10,20,30];
for (let i in arr) console.log(i); // 0 1 2
for (let v of arr) console.log(v); // 10 20 30
```

---

# 3️⃣ Rest Operator vs Spread Operator

| Operator | Syntax | Purpose | Example |
|----------|--------|---------|---------|
| Rest `...` | function f(...args) | Collect remaining arguments into an array | `function sum(...nums){ return nums.reduce((a,b)=>a+b); }` |
| Spread `...` | `[...arr]` or `{...obj}` | Expand array/object elements | `const newArr = [...arr,4,5]` |

**Example:**

```js
// Rest
function add(...nums){ return nums.reduce((a,b)=>a+b); }
console.log(add(1,2,3)); // 6

// Spread
const arr = [1,2];
const newArr = [...arr,3,4]; // [1,2,3,4]
```

---

# 4️⃣ Shallow Copy vs Deep Copy

| Feature | Shallow Copy | Deep Copy |
|---------|-------------|-----------|
| Copies | Only first-level | All nested levels |
| Reference | Nested objects **share references** | Fully independent |
| Methods | `Object.assign()`, `[...arr]` | `JSON.parse(JSON.stringify(obj))` or structuredClone |

**Example:**

```js
const obj = {a:1, b:{c:2}};
const shallow = {...obj};
const deep = JSON.parse(JSON.stringify(obj));

obj.b.c = 10;
console.log(shallow.b.c); // 10 (affected)
console.log(deep.b.c);    // 2 (independent)
```

---

# 5️⃣ Event Propagation

- **Event Flow** in the DOM:  
1. **Capture phase** – top → target  
2. **Target phase** – target element  
3. **Bubble phase** – target → top  

```js
element.addEventListener('click', fn, true); // capture
element.addEventListener('click', fn, false); // bubble
```

- Default: bubble phase  
- Can stop propagation using `event.stopPropagation()`

---

# 6️⃣ Event Delegation

- Attach **one listener** to a **parent element** instead of multiple children  
- Use **event.target** to determine which child triggered the event  

```js
document.querySelector('#parent').addEventListener('click', function(e){
  if(e.target.tagName === 'BUTTON') {
    console.log("Button clicked:", e.target.textContent);
  }
});
```

**Benefits:**  
- Efficient memory usage  
- Handles **dynamic elements** added later  

---

# 7️⃣ Summary Table – Common JS Differences

| Concept | Key Difference |
|---------|----------------|
| map vs filter vs forEach | map → transform, filter → subset, forEach → side-effect |
| for vs for..in vs for..of | for → index, for..in → keys, for..of → values |
| rest vs spread | rest → collect args, spread → expand array/object |
| shallow vs deep copy | shallow → first-level only, deep → nested independent |
| event propagation vs delegation | propagation → bubble/capture, delegation → single listener handles children |

---

# 8️⃣ Senior-Level Interview Notes

- Always know **microtasks vs macrotasks** for async event handling  
- Know when to use **spread vs rest**  
- Deep copy is crucial for **immutable state management**  
- Event delegation improves **performance for large dynamic DOM**  
- Be able to **predict outputs** for tricky closures and nested async operations  

---

# 🎯 Senior-Level Takeaway

- Master **array methods and loops**  
- Understand **memory references for copy operations**  
- Know **DOM event flow and delegation patterns**  
- Be able to **combine these concepts** in real-world scenarios  

---
# 9️⃣ Primitive vs Non-Primitive Behavior

- **Primitive**: immutable, copied by value  
- **Non-Primitive**: mutable, copied by reference  

```js
let a = 10;
let b = a; // copy by value
a = 20;
console.log(b); // 10

let obj1 = {x:1};
let obj2 = obj1; // copy by reference
obj1.x = 10;
console.log(obj2.x); // 10
```
---



