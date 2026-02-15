### Microtask vs Macrotask
```javascript
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

Promise.resolve().then(() => {
  console.log("C");
});

console.log("D");
```
Answer
```css
A
D
C
B
```
Why?
Order of execution:
Synchronous → A
Synchronous → D
Microtask (Promise) → C
Macrotask (setTimeout) → B

### Nested Promises

```javascript
Promise.resolve()
  .then(() => {
    console.log("1");
    return Promise.resolve("2");
  })
  .then((res) => {
    console.log(res);
  });

console.log("3");
```
Answer
```css
3
1
2
```
Why?
3 is synchronous
.then() always executes asynchronously
Returned Promise is automatically unwrapped

### Error Handling Chain

```javascript
Promise.resolve()
  .then(() => {
    throw new Error("Error!");
  })
  .then(() => {
    console.log("Then after error");
  })
  .catch((err) => {
    console.log("Caught:", err.message);
  })
  .then(() => {
    console.log("After catch");
  });
```
Answer
```css
Caught: Error!
After catch
```
💡 Why?

Error skips the next .then()

Goes directly to .catch()

After catch, chain continues normally

👉 Yes, "After catch" WILL run.

### Promise Inside setTimeout

```javascript
setTimeout(() => {
  console.log("Timeout 1");

  Promise.resolve().then(() => {
    console.log("Promise inside Timeout");
  });
}, 0);

Promise.resolve().then(() => {
  console.log("Promise 1");
});

setTimeout(() => {
  console.log("Timeout 2");
}, 0);
```
Answer
```css
Promise 1
Timeout 1
Promise inside Timeout
Timeout 2
```
Execution order:

Microtask → Promise 1

Macrotask → Timeout 1

Microtask created inside Timeout → Promise inside Timeout

Next macrotask → Timeout 2

👉 Microtasks always drain completely before next macrotask.

### Promise.resolve in Then

```javascript
Promise.resolve()
  .then(() => {
    console.log("A");
    return "B";
  })
  .then((val) => {
    console.log(val);
    return Promise.resolve("C");
  })
  .then((val) => {
    console.log(val);
  });

console.log("D");
```
Answer
```css
D
A
B
C
```
💡 Why?

D is synchronous

Promise chain runs after call stack

Returning normal value → auto wrapped in Promise

Returning Promise → automatically flattened

```css
body {
    background-color: black;
    color: white;
}
```

