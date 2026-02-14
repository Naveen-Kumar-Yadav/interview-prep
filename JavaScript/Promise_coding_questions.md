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
### 7.Implement sleep() Function.
Create a function that waits for given seconds before continuing.
```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
async function test() {
  console.log("Start");
  await sleep(3000);
  console.log("After 3 seconds");
}

test();
```
### 8.Print Numbers with 1 Second Gap.
Print 1 to 5 with 1 second delay between each.
```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function printNumbers() {
  for (let i = 1; i <= 5; i++) {
    console.log(i);
    await sleep(1000);
  }
}

printNumbers();
```
### 9.Sleep + Retry Pattern (Advanced).
Very common in product companies.
```javascript
async function retry(fn, retries) {
  for (let i = 0; i < retries; i++) {
    try {
      return await fn();
    } catch (err) {
      if (i === retries - 1) throw err;
      await sleep(1000);
    }
  }
}
```
### 10.Alarm Example (Resolve if done before time, else Reject).
Create a Promise that works like an alarm.
If user wakes up before time → resolve
If time finishes → reject
OR
If task finishes before time → resolve, otherwise reject.
```javascript
function alarm(taskPromise, ms) {
  return new Promise((resolve, reject) => {
    const timer = setTimeout(() => {
      reject(new Error("⏰ Alarm! Time exceeded"));
    }, ms);

    taskPromise
      .then(result => {
        clearTimeout(timer);
        resolve(result);
      })
      .catch(err => {
        clearTimeout(timer);
        reject(err);
      });
  });
}

function task() {
  return new Promise(resolve => {
    setTimeout(() => resolve("Task Completed"), 3000);
  });
}

alarm(task(), 5000)
  .then(console.log)
  .catch(console.error);
```
### 11.Wake-up Alarm Example (Fun Interview Version).
```javascript
function wakeUpAlarm(wakeTime) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (wakeTime <= 5) {
        resolve("Good Morning ☀️");
      } else {
        reject("You overslept 😴");
      }
    }, wakeTime * 1000);
  });
}
```
### 12.Create a Basic Promise (resolves after 1 second).

```javascript
function helloWorldPromise() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Hello World");
    }, 1000); // 1 second
  });
}

// Usage
helloWorldPromise()
  .then(message => console.log(message))
  .catch(error => console.error(error));
```
### 13.Reject a Promise (rejects after 2 seconds).

```javascript
function errorPromise() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject("Something went wrong");
    }, 2000); // 2 seconds
  });
}

// Usage
errorPromise()
  .then(message => console.log(message))
  .catch(error => console.error("Error:", error));
```
### Create three Promises that resolve after 1, 2, and 3 seconds respectively. Use Promise.all() to log all results together.

```javascript
// Create three promises with different delays
const promise1 = new Promise(resolve => setTimeout(() => resolve("Resolved after 1 second"), 1000));
const promise2 = new Promise(resolve => setTimeout(() => resolve("Resolved after 2 seconds"), 2000));
const promise3 = new Promise(resolve => setTimeout(() => resolve("Resolved after 3 seconds"), 3000));

// Use Promise.all to wait for all of them
Promise.all([promise1, promise2, promise3])
  .then(results => {
    console.log("All promises resolved:");
    console.log(results);
  })
  .catch(error => {
    console.error("One of the promises failed:", error);
  });
```
### Write an example where two Promises resolve at different times. Use Promise.race() to log whichever finishes first.
```javascript
// Create two promises with different delays
const promise1 = new Promise(resolve => {
  setTimeout(() => resolve("Promise 1 resolved after 2 seconds"), 2000);
});

const promise2 = new Promise(resolve => {
  setTimeout(() => resolve("Promise 2 resolved after 1 second"), 1000);
});

// Use Promise.race to log whichever resolves first
Promise.race([promise1, promise2])
  .then(result => console.log("First resolved:", result))
  .catch(error => console.error("Error:", error));
```
### Example of Promise.allSettled().

```javascript
// Create three promises: 2 resolve, 1 rejects
const promise1 = new Promise(resolve => setTimeout(() => resolve("Resolved after 1 second"), 1000));
const promise2 = new Promise((resolve, reject) => setTimeout(() => reject("Rejected after 2 seconds"), 2000));
const promise3 = new Promise(resolve => setTimeout(() => resolve("Resolved after 3 seconds"), 3000));

// Use Promise.allSettled to wait for all of them regardless of success or failure
Promise.allSettled([promise1, promise2, promise3])
  .then(results => {
    console.log("Results of all promises:");
    results.forEach((result, index) => {
      console.log(`Promise ${index + 1}:`, result);
    });
  });
```
### implementing a concurrency limiter with 3 promises running at a time:

```javascript
// Simulate API call with random delay
function fakeApiCall(id) {
  const delay = Math.floor(Math.random() * 2000) + 1000; // 1-3 sec
  return new Promise(resolve => {
    setTimeout(() => {
      console.log(`API ${id} done after ${delay}ms`);
      resolve(`Result from API ${id}`);
    }, delay);
  });
}

// Concurrency limiter function
async function limitConcurrency(tasks, limit) {
  const results = [];
  const executing = [];

  for (const task of tasks) {
    const p = task().then(result => {
      // Remove finished promise from executing array
      executing.splice(executing.indexOf(p), 1);
      return result;
    });
    
    results.push(p);
    executing.push(p);

    // If we hit concurrency limit, wait for one to finish
    if (executing.length >= limit) {
      await Promise.race(executing);
    }
  }

  return Promise.all(results);
}

// Create 10 fake API tasks
const apiTasks = Array.from({ length: 10 }, (_, i) => () => fakeApiCall(i + 1));

// Run with concurrency limit = 3
limitConcurrency(apiTasks, 3).then(allResults => {
  console.log("All API calls completed:");
  console.log(allResults);
});

```
### If task doesn't complete before deadlineMs, reject with "Timeout".
```javascript
function withDeadline(taskPromise, deadlineMs) {
  return new Promise((resolve, reject) => {
    const timer = setTimeout(() => {
      reject(new Error("Timeout"));
    }, deadlineMs);

    taskPromise
      .then((result) => {
        clearTimeout(timer);
        resolve(result);
      })
      .catch((error) => {
        clearTimeout(timer);
        reject(error);
      });
  });
}

// Example task
function asyncTask(duration) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Task Finished");
    }, duration);
  });
}

// Test
withDeadline(asyncTask(5000), 9000)
  .then(console.log)
  .catch(console.error);

withDeadline(asyncTask(10000), 9000)
  .then(console.log)
  .catch(console.error);
```
### User Typing Before 9 Seconds
User must type "CONFIRM" within 9 seconds.
If typed correctly → resolve "Confirmed"
If not typed in time → reject "Session Expired"

```javascript
function waitForConfirmation(userInputTime, inputValue) {
  return new Promise((resolve, reject) => {
    const timeout = setTimeout(() => {
      reject("Session Expired");
    }, 9000);

    setTimeout(() => {
      if (inputValue === "CONFIRM") {
        clearTimeout(timeout);
        resolve("Confirmed");
      } else {
        clearTimeout(timeout);
        reject("Wrong Input");
      }
    }, userInputTime);
  });
}

// Test
waitForConfirmation(5000, "CONFIRM")
  .then(console.log)
  .catch(console.error);

waitForConfirmation(10000, "CONFIRM")
  .then(console.log)
  .catch(console.error);
```

