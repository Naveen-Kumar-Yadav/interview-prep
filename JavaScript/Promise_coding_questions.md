# Promise Interview Questions

### 1. Create a Timeout Wrapper
If promise takes more than 5 seconds → reject.
```javascript
function withTimeout(promise, ms) {
  const timeout = new Promise((_, reject) =>
    setTimeout(() => reject("Timeout"), ms)
  );
  return Promise.race([promise, timeout]);
}
```
```javascript
function withTimeout(promise, ms = 5000) {
  return new Promise((resolve, reject) => {
    const timer = setTimeout(() => {
      reject(new Error("Timeout"));
    }, ms);

    promise
      .then(value => {
        clearTimeout(timer);
        resolve(value);
      })
      .catch(err => {
        clearTimeout(timer);
        reject(err);
      });
  });
}
```
### 2.Promise that resolves after 10 minutes
```javascript
function promiseAfterTenMinutes() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Success after 10 minutes!");
    }, 10 * 60 * 1000); // 10 minutes
  });
}

// Usage
promiseAfterTenMinutes()
  .then(result => console.log(result))
  .catch(error => console.error(error));
```
Shorter Version (Inline Promise)
```javascript
new Promise(resolve => 
  setTimeout(() => resolve("Success after 10 minutes!"), 600000)
).then(console.log);
```
If You Just Want 10 Seconds (For Testing)
```javascript
new Promise(resolve => 
  setTimeout(() => resolve("Success after 10 minutes!"), 600000)
).then(console.log);
```
This shows modern JavaScript knowledge.
```javascript
function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

async function run() {
  await delay(10 * 60 * 1000);
  console.log("Success after 10 minutes");
}
run();
```
### 3.Implement Promise.all
```javascript
function myPromiseAll(promises) {
  return new Promise((resolve, reject) => {
    let results = [];
    let completed = 0;

    promises.forEach((p, index) => {
      Promise.resolve(p)
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
### 4.Implement Retry Logic.
Retry an API 3 times before failing.
```javascript
function myPromiseAll(promises) {
  return new Promise((resolve, reject) => {
    let results = [];
    let completed = 0;

    promises.forEach((p, index) => {
      Promise.resolve(p)
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
### 5.Implement a Delay Function.

```javascript
// Generic delay function
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

// Async function to use delay
async function run() {
  console.log("Waiting for 3 seconds...");
  await delay(3000); // 3 seconds
  console.log("3 seconds passed!");
  
  console.log("Waiting for 1 second...");
  await delay(1000); // 1 second
  console.log("1 more second passed!");
}

// Execute
run();
```
### 5.Basic Custom Promise Implementation.
```javascript
class MyPromise {
  constructor(executor) {
    this.state = "pending";
    this.value = undefined;
    this.handlers = [];

    const resolve = (value) => {
      if (this.state !== "pending") return;
      this.state = "fulfilled";
      this.value = value;
      this.handlers.forEach(h => h.onFulfilled(value));
    };

    const reject = (error) => {
      if (this.state !== "pending") return;
      this.state = "rejected";
      this.value = error;
      this.handlers.forEach(h => h.onRejected(error));
    };

    try {
      executor(resolve, reject);
    } catch (err) {
      reject(err);
    }
  }

  then(onFulfilled, onRejected) {
    return new MyPromise((resolve, reject) => {

      const handle = () => {
        try {
          if (this.state === "fulfilled") {
            const result = onFulfilled ? onFulfilled(this.value) : this.value;
            resolve(result);
          }

          if (this.state === "rejected") {
            if (onRejected) {
              const result = onRejected(this.value);
              resolve(result);
            } else {
              reject(this.value);
            }
          }

          if (this.state === "pending") {
            this.handlers.push({
              onFulfilled: (value) => {
                try {
                  resolve(onFulfilled ? onFulfilled(value) : value);
                } catch (err) {
                  reject(err);
                }
              },
              onRejected: (error) => {
                try {
                  if (onRejected) {
                    resolve(onRejected(error));
                  } else {
                    reject(error);
                  }
                } catch (err) {
                  reject(err);
                }
              }
            });
          }
        } catch (err) {
          reject(err);
        }
      };

      handle();
    });
  }

  catch(onRejected) {
    return this.then(null, onRejected);
  }
}
const p = new MyPromise((resolve, reject) => {
  setTimeout(() => resolve("Success!"), 1000);
});

p.then(data => {
  console.log(data);
});

```
