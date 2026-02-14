# Promise Interview Questions

### 4. Create a Timeout Wrapper
If promise takes more than 5 seconds → reject..
```javascript
function withTimeout(promise, ms) {
  const timeout = new Promise((_, reject) =>
    setTimeout(() => reject("Timeout"), ms)
  );
  return Promise.race([promise, timeout]);
}
```
