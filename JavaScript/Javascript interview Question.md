# JavaScript Interview Questions

## 1. What is JavaScript?

JavaScript is a dynamic computer programming language. It is lightweight and most commonly used as a part of web pages, whose implementations allow client-side script to interact with the user and make dynamic pages. It is an interpreted programming language with object-oriented capabilities.

### DOM (Document Object Model)
DOM is an HTML documentation that separates HTML object element tags, defines how to keep object elements organized, and arranges the object elements in a structured hierarchy.

---

## 2. Data Types

### Primitive Data Types
- **Number**: An integer or a floating-point number (e.g., 3, 3.234, 3e-2)
- **String**: Represents textual data (e.g., 'hello', "hello world!")
- **Boolean**: Any of two values: true or false
- **Null**: Denotes a null value (e.g., let a = null;)
- **Undefined**: A data type whose variable is not initialized (e.g., let a;)
- **BigInt**: An integer with arbitrary precision (e.g., 900719925124740999n, 1n)
- **Symbol**: Data type whose instances are unique and immutable (e.g., let value = Symbol('hello');)

### Non-Primitive Data Types
- **Object**: Key-value pairs of collection of data (e.g., let student = {};)
- **Array**: An ordered collection of elements

**Reference**: [Primitive and Non-Primitive Data Types](https://www.geeksforgeeks.org/primitive-and-non-primitive-data-types-in-javascript/)

---

## 3. Difference between var, let, and const

| Feature | var | let | const |
|---------|-----|-----|-------|
| Scope | Global scope | Block scope | Block scope |
| Re-declare | Yes | No | No |
| Re-assign | Yes | Yes | No |

### Example:
```javascript
// VAR example
var a = "naveen";
var a = "updated";  // Can re-declare
{
  var a = "Kumar";
}
console.log(a); // Output: "Kumar" (global scope)

// LET example
let b = "naveen";
// let b = "updated"; // Cannot re-declare (would throw error)
b = "updated"; // Can re-assign
{
  let b = "Kumar";
}
console.log(b); // Output: "updated" (block scope)

// CONST example
const c = "naveen";
// const c = "updated"; // Cannot re-declare
// c = "updated"; // Cannot re-assign
{
  const c = "Kumar";
}
console.log(c); // Output: "naveen" (block scope)
function makeMultiplier(multiplier) {
  return function(value) {
    return value * multiplier;
  };
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
