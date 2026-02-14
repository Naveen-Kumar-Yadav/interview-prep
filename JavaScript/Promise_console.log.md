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
