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

### Basic Promise Resolution

```javascript
console.log("Start");

const promise1 = new Promise((resolve) => {
  console.log("Promise started");
  resolve("Resolved");
});

promise1.then((result) => {
  console.log(result);
});

console.log("End");
```
Answer
```css
Start
Promise started
End
Resolved
```
💡 Why?

The first console.log("Start") is executed.
The promise executor runs immediately, logging Promise started.
The .then() block is scheduled as a microtask after the current code finishes executing.
console.log("End") runs next.
Finally, the .then() callback logs Resolved when the microtask queue is processed.

### Nested Promises.
```javascript
const promise2 = new Promise((resolve) => {
  resolve("Resolved 1");
});

promise2.then((result) => {
  console.log(result);
  return new Promise((resolve) => {
    resolve("Resolved 2");
  });
}).then((result) => {
  console.log(result);
});
```
Answer
```css
Resolved 1
Resolved 2
```
💡 Why?

The first .then() logs Resolved 1 and returns a new promise.
The second .then() waits for the returned promise to resolve, logging Resolved 2.

### Chained Promise with Immediate Resolution.
```javascript
const promise3 = Promise.resolve();

promise3
  .then(() => {
    console.log("Then 1");
  })
  .then(() => {
    console.log("Then 2");
  })
  .then(() => {
    console.log("Then 3");
  });
```
Answer
```css
Then 1
Then 2
Then 3
```
💡 Why?

When a promise is immediately resolved (Promise.resolve()), its .then() handlers are queued in the microtask queue.
Each .then() returns a new promise that resolves after its callback runs, resulting in a sequential execution of Then 1, Then 2, and Then 3.

### Rejection Handling
```javascript
const promise4 = new Promise((_, reject) => {
  reject("Error occurred");
});

promise4
  .then(() => {
    console.log("This will not run");
  })
  .catch((error) => {
    console.log("Caught:", error);
  })
  .then(() => {
    console.log("This will still run");
  });
```
Answer
```css
Caught: Error occurred
This will still run
```
💡 Why?

The promise is rejected with the message "Error occurred".
The .catch() block catches the error and logs Caught: Error occurred.
After .catch(), the next .then() still runs because it’s treated as a resolved promise unless the catch throws again.


### Mixing Async/Await with Promises
```javascript
async function asyncFunc() {
  console.log("Async function started");
  return "Async result";
}

asyncFunc().then((result) => {
  console.log(result);
});

console.log("Synchronous log");
```
Answer
```css
Async function started
Synchronous log
Async result
```
💡 Why?
When asyncFunc is called, it immediately logs Async function started.
The return value of an async function is a promise, so the .then() is scheduled as a microtask.
console.log("Synchronous log") runs next, followed by the resolution of the promise which logs Async result.


### What will be logged?

```javascript
const promise = new Promise((resolve, reject) => {
 resolve(‘First’);
 resolve(‘Second’);
});

promise.then(console.log);
```
Options:
- A) ‘First’
- B) ‘Second’
- C) Both ‘First’ and ‘Second’
- D) Nothing

Answer: A) ‘First’

Explanation:
Once a promise is resolved, additional calls to `resolve()` are ignored. The first resolution takes effect; subsequent calls do nothing. So, only `’First’` gets logged.

### What will be the output?

```javascript
const promise = new Promise((resolve) => {
 resolve(‘Resolved’);
});
promise.then((res) => {
 console.log(res);
 return ‘Next’;
}).then((res) => {
 console.log(res);
});
Options:
- A) Resolved
Next
- B) Resolved
undefined
- C) undefined
undefined
- D) Error
```
Answer: A) Resolved
Next

Explanation:

The first `.then()` logs `’Resolved’` and returns `’Next’`. The second `.then()` receives `’Next’` and logs it.

### Output of this code?

```javascript
Promise.resolve(1)
 .then((res) => {
 console.log(res);
 return Promise.reject(‘Error!’);
 })
 .then(() => {
 console.log(‘This will not run’);
 })
 .catch((err) => {
 console.log(‘Caught:’, err);
 });
```
Options:
- A) 1
This will not run
- B) 1
Caught: Error!
- C) Caught: Error!
- D) Error thrown, no output

Answer: B) 1
Caught: Error!

Explanation:

The first `.then()` logs `’1'` and returns a rejected promise. The next `.then()` is skipped, and control passes to `.catch()` which logs `’Caught: Error!’`.

### What will be printed?

```javascript
async function test() {
 console.log(‘Start’);
 await Promise.resolve(‘Resolved’);
 console.log(‘After await’);
}

test();
console.log('End');
```
Options:
- A) Start
End
After await
- B) Start
After await
End
- C) End
Start
After await
- D) Error

Answer: A)

Explanation:
`test()` starts and logs `’Start’`. The `await` pauses the function, allowing `’End’` to log immediately in the main thread. After the promise resolves, `’After await’` logs.

Question 5: What is the output?

```javascript
const p1 = new Promise((resolve) => {
 setTimeout(() => resolve(‘First’), 1000);
});
const p2 = new Promise((resolve) => {
 setTimeout(() => resolve(‘Second’), 500);
});
Promise.race([p1, p2]).then(console.log);
```
Options:
- A) First
- B) Second

- C) Both First and Second
- D) Nothing

Answer: B) Second

Explanation:
`Promise.race()` resolves with the value of the first promise to settle. Since `p2` resolves after 500ms, `’Second’` is logged.

