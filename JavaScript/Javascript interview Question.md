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
```

**References**:
- [let vs var - Programiz](https://www.programiz.com/javascript/let-vs-var)
- [Understanding let, const, and var - FreeCodeCamp](https://www.freecodecamp.org/news/understanding-let-const-and-var-keywords/)

---

## 4. Ways to Create Objects in JavaScript

### 1. Object Constructor
The simplest way to create an empty object (not recommended).
```javascript
var object = new Object();
```

### 2. Object.create() Method
Creates a new object by passing the prototype object as a parameter.
```javascript
var object = Object.create(null);
```

### 3. Object Literal Syntax
A comma-separated set of name-value pairs wrapped in curly braces.
```javascript
var object = {
  name: "Sudheer",
  age: 34
};
```

### 4. Function Constructor
Create any function and apply the new operator to create object instances.
```javascript
function Person(name) {
  this.name = name;
  this.age = 21;
}
var object = new Person("Sudheer");
```

### 5. Function Constructor with Prototype
Uses prototype for properties and methods.
```javascript
function Person() {}
Person.prototype.name = "Sudheer";
var object = new Person();
```

### 6. ES6 Class Syntax
Modern approach using class syntax.
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}
var object = new Person("Sudheer");
```

### 7. Singleton Pattern
An object which can only be instantiated one time.
```javascript
var object = new (function () {
  this.name = "Sudheer";
})();
```

---

## 5. What is a Prototype Chain?

Prototype chaining is used to build new types of objects based on existing ones. It is similar to inheritance in a class-based language.

The prototype on an object instance is available through `Object.getPrototypeOf(object)` or `__proto__` property, whereas the prototype on a constructor function is available through `Object.prototype`.

**References**:
- [MDN - Inheritance and the Prototype Chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
- [MDN - Object Prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)

---

## 6. Difference between Call, Apply, and Bind

### Call
The call() method invokes a function with a given `this` value and arguments provided **one by one**.

```javascript
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2);
}

invite.call(employee1, "Hello", "How are you?"); 
// Output: Hello John Rodson, How are you?

invite.call(employee2, "Hello", "How are you?"); 
// Output: Hello Jimmy Baily, How are you?
```

### Apply
The apply() method invokes a function with a given `this` value and arguments provided as an **array**.

```javascript
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2);
}

invite.apply(employee1, ["Hello", "How are you?"]); 
// Output: Hello John Rodson, How are you?

invite.apply(employee2, ["Hello", "How are you?"]); 
// Output: Hello Jimmy Baily, How are you?
```

### Bind
The bind() method creates a **new function** that, when called, has its `this` keyword set to the provided value.

```javascript
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2);
}

var inviteEmployee1 = invite.bind(employee1);
var inviteEmployee2 = invite.bind(employee2);

inviteEmployee1("Hello", "How are you?"); 
// Output: Hello John Rodson, How are you?

inviteEmployee2("Hello", "How are you?"); 
// Output: Hello Jimmy Baily, How are you?
```

### Summary
- **Call** and **Apply**: Execute the function immediately. Call takes arguments individually, Apply takes an array.
- **Bind**: Creates a new function without executing it immediately.

**Memory tip**: Call = **C**omma (separated list), Apply = **A**rray

**Video Resource**: [Call, Apply, and Bind](https://www.youtube.com/watch?v=rRAvhzux-7Y)

---

## 7. JSON and Common Operations

JSON (JavaScript Object Notation) is a text-based data format following JavaScript object syntax, popularized by Douglas Crockford. It is useful for transmitting data across a network.

### Parsing
Converting a JSON string to a native JavaScript object:
```javascript
JSON.parse(text);
```

### Stringification
Converting a native JavaScript object to a JSON string for transmission:
```javascript
JSON.stringify(object);
```

---

## 8. Array Methods: slice() vs splice()

### slice() Method
Returns the selected elements in an array as a **new array object**. Does not modify the original array.

```javascript
let arrayIntegers = [1, 2, 3, 4, 5];
let arrayIntegers1 = arrayIntegers.slice(0, 2); // returns [1, 2]
let arrayIntegers2 = arrayIntegers.slice(2, 3); // returns [3]
let arrayIntegers3 = arrayIntegers.slice(4);    // returns [5]
```

**Note**: Slice method won't mutate the original array.

### splice() Method
Adds/removes items to/from an array and returns the **removed items**. Modifies the original array.

```javascript
let arrayIntegersOriginal1 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal2 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal3 = [1, 2, 3, 4, 5];

let arrayIntegers1 = arrayIntegersOriginal1.splice(0, 2); 
// returns [1, 2]; original array: [3, 4, 5]

let arrayIntegers2 = arrayIntegersOriginal2.splice(3); 
// returns [4, 5]; original array: [1, 2, 3]

let arrayIntegers3 = arrayIntegersOriginal3.splice(3, 1, "a", "b", "c"); 
// returns [4]; original array: [1, 2, 3, "a", "b", "c"]
```

**Note**: Splice method modifies the original array.

### Comparison Table

| Feature | slice() | splice() |
|---------|---------|----------|
| Mutates Original Array | No (Immutable) | Yes (Mutable) |
| Return Value | Subset of original array | Deleted elements as array |
| Purpose | Pick elements from array | Insert or delete elements |

---

## 9. Difference between == and ===

JavaScript provides both strict (`===`, `!==`) and type-converting (`==`, `!=`) equality comparison.

- **Strict operators** (`===`, `!==`): Check type and value
- **Non-strict operators** (`==`, `!=`): Perform type coercion

### Strict Equality Rules
1. Two strings are strictly equal when they have the same sequence, length, and characters in corresponding positions.
2. Two numbers are strictly equal when they are numerically equal.
   - `NaN` is not equal to anything, including `NaN`
   - Positive and negative zeros are equal to one another
3. Two Booleans are strictly equal if both are true or both are false.
4. Two objects are strictly equal if they refer to the same object.
5. Null and Undefined are not equal with `===`, but equal with `==`.

### Examples
```javascript
0 == false          // true
0 === false         // false

1 == "1"            // true
1 === "1"           // false

null == undefined   // true
null === undefined  // false

'0' == false        // true
'0' === false       // false

[] == []            // false (refer different objects in memory)
[] === []           // false (refer different objects in memory)

{} == {}            // false (refer different objects in memory)
{} === {}           // false (refer different objects in memory)
```

---

## 10. Arrow Functions

An arrow function is a shorter syntax for a function expression and does not have its own `this`, `arguments`, `super`, or `new.target`. These functions are best suited for non-method functions and cannot be used as constructors.

```javascript
// Regular function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// With multiple statements
const multiply = (a, b) => {
  const result = a * b;
  return result;
};
```

---

## 11. First Class Functions

In JavaScript, functions are first-class objects. This means functions are treated like any other variable and can be:
- Passed as arguments to other functions
- Returned by another function
- Assigned as a value to a variable

```javascript
// Function as a variable
const handler = () => console.log("This is a click handler function");

// Function as an argument (callback)
document.addEventListener("click", handler);

// Function returning a function
const makeGreeting = (greeting) => {
  return (name) => {
    return greeting + ', ' + name;
  };
};

const sayHello = makeGreeting('Hello');
console.log(sayHello('John')); // Output: Hello, John
```

---

## 12. Polyfill

A polyfill in JavaScript is a piece of code that provides functionality that is not natively supported in some web browsers. It essentially "fills in" the gaps, allowing developers to use newer features or APIs that may not be available in older browser versions.

### Key Points About Polyfills:

**Backward Compatibility**: Polyfills enable developers to use modern web standards without worrying about browser compatibility.

**Implementation of New Features**: Polyfills mimic new JavaScript APIs using older syntax that is more widely supported.

### Examples of Polyfills:
- **Promise**: For browsers that do not support Promises, use the es6-promise library
- **fetch**: Polyfills like whatwg-fetch provide the fetch API in older environments
- **Object.assign**: Provides a polyfill for environments that don't support it natively

### Usage:
Polyfills are often included conditionally in web applications. Tools like Babel can automatically add polyfills for the specific environments targeted by your codebase.

---

## 13. Temporal Dead Zone (TDZ)

### Hindi Explanation
"Temporal Dead Zone" (TDZ) ek programming term hai jo JavaScript ke context mein use hota hai, khas kar ES6 (ECMAScript 2015) ke "let" aur "const" keywords ke sath. TDZ tab hota hai jab ek variable ko declare kiya gaya hai, lekin uski value ko initialize nahi kiya gaya hai.

Iska matlab hai ki jab tak aap variable ko declare nahi kar lete, aap us variable ko access nahi kar sakte. Agar aap access karne ki koshish karte hain, to aapko "ReferenceError" milta hai.

```javascript
console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 5;
```

Yahaan, a ko declare kiya gaya hai let keyword ke sath, lekin jab aap console.log(a) ko call karte hain, tab a TDZ mein hota hai, isliye aapko error milta hai. TDZ tab tak continue hoti hai jab tak variable ko declare aur initialize nahi kar diya jata.

Yeh behavior var keyword ke sath nahi hota. var ke sath, variables hoisting ke through accessible hote hain, lekin unki values undefined hoti hain agar initialization se pehle access kiya jaye.

TDZ ka primary purpose variable declaration aur initialization ko ensure karna hai, taaki code ki readability aur debugging process behtar ho.

### English Explanation
The "Temporal Dead Zone" (TDZ) is a programming term used in JavaScript, particularly with the `let` and `const` keywords introduced in ES6 (ECMAScript 2015). TDZ occurs when a variable has been declared but not yet initialized.

This means that until you declare and initialize the variable, you cannot access it. If you try to access it before the declaration, you'll get a ReferenceError.

```javascript
console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 5;
```

Here, `a` is declared with the `let` keyword, but when you try to `console.log(a)`, `a` is in the TDZ, and hence you get an error. The TDZ persists until the variable is declared and initialized.

This behavior does not apply to the `var` keyword. With `var`, variables are hoisted and accessible, but they are undefined if accessed before initialization.

**The primary purpose of TDZ is to ensure that variables are declared and initialized properly before use, which improves code readability and debugging.**

---

## 14. Closures

### Definition
A closure is a programming concept where an inner function retains access to the variables of its outer function even after the outer function has finished executing. This allows the inner function to remember and use the outer function's variables.

### Hindi Explanation
Closure ek programming concept hai jo JavaScript aur kai dusre programming languages mein use hota hai. Closure tab banta hai jab ek function apni outer function ke scope ke variables ko access karta hai, even though outer function apni execution complete kar chuki hoti hai.

### Example
```javascript
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable) {
    console.log("Outer Variable: " + outerVariable);
    console.log("Inner Variable: " + innerVariable);
  };
}

const closureFunction = outerFunction("I'm outside!");
closureFunction("I'm inside!");
```

**Explanation**:
- `outerFunction` is an outer function that accepts `outerVariable` and returns an inner function `innerFunction`
- `innerFunction` can access both `outerVariable` and `innerVariable`
- When `closureFunction` is called, it can still access `outerVariable` through closure

### Key Points
- **Enclosing Scope**: Closure ensures the inner function retains access to the variables of its enclosing (outer) function
- **Data Encapsulation**: Closures can be used to create private variables or methods

### Use Cases

#### 1. Data Encapsulation (Private Variables)
```javascript
function createCounter() {
  let count = 0; // Private variable
  return function() {
    count += 1;
    return count;
  };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

#### 2. Function Factories
```javascript
function makeMultiplier(multiplier) {
  return function(value) {
    return value * multiplier;
  };
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

#### 3. Maintaining State
```javascript
function createGreeting(greeting) {
  return function(name) {
    return greeting + ', ' + name;
  };
}

const sayHello = createGreeting('Hello');
console.log(sayHello('Alice')); // Hello, Alice
console.log(sayHello('Bob'));   // Hello, Bob
```

#### 4. Partial Application and Currying
```javascript
function add(a) {
  return function(b) {
    return a + b;
  };
}

const addFive = add(5);
console.log(addFive(10)); // 15
```

#### 5. Asynchronous Programming
```javascript
function asyncOperation() {
  let result = 0;
  setTimeout(function() {
    result = 42;
    console.log('Async operation result:', result);
  }, 1000);
}

asyncOperation();
```

---

## 15. Currying

Currying is a functional programming technique in which a function is transformed to accept multiple arguments one at a time, rather than taking all arguments at once.

### Concept
- **Function Transformation**: Transforms a function that takes multiple arguments into a series of functions, each taking a single argument
- **Partial Application**: Allows partial application of function arguments

### How It Works
```javascript
// Normal function
function multiply(a, b) {
  return a * b;
}

// Curried function
function curriedMultiply(a) {
  return function(b) {
    return a * b;
  };
}

const multiplyBy2 = curriedMultiply(2);
console.log(multiplyBy2(5)); // 10
```

### Explanation
- **Normal Function**: `multiply` takes two arguments `a` and `b` and returns their product
- **Curried Function**: `curriedMultiply` takes one argument `a` and returns a new function that takes another argument `b`
- **Partial Application**: `multiplyBy2` is a partially applied function where `a` is fixed to 2

### Benefits
- **Modularity**: Allows for more modular and reusable code
- **Function Composition**: Helps in composing functions and creating more specific functions from general ones
- **Lazy Evaluation**: Supports lazy evaluation, where functions can be applied incrementally

Currying is widely used in functional programming and can be very powerful in JavaScript for creating flexible and reusable functions.
```
