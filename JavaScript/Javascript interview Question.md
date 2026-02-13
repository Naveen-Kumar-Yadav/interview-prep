# Advanced JavaScript Interview Questions for 5+ Years of Experience

1. **Explain the concept of closures and provide an example.**  
   Closures are functions that have access to their outer function scope even after the outer function has returned. This means a closure can "remember" the environment in which it was created.

2. **Discuss the prototypal inheritance in JavaScript. How does it differ from classical inheritance?
   JavaScript uses prototypal inheritance where objects can inherit properties and methods from other objects. Unlike classical inheritance where classes are defined and instances are created, JavaScript's approach is more flexible as every object can serve as a prototype for another object.

3. **What are Promises and how do you use them in JavaScript?**  
   Promises are objects that represent the eventual completion (or failure) of an asynchronous operation and its resulting value. You can use `.then()`, `.catch()`, and `.finally()` methods to handle the results or errors of the promise.

4. **Explain the new `async/await` syntax introduced in ES2017.**  
   `async/await` provides a simpler way to work with asynchronous code. The `async` keyword is put in front of a function declaration, and `await` can be used within that function to pause execution until a Promise is resolved.

5. **What is the Event Loop in JavaScript?**  
   The Event Loop is a fundamental concept in JavaScript that allows it to perform non-blocking I/O operations. It continuously checks the call stack and the message queue, executing queued tasks as soon as the call stack is empty.

6. **Can you explain the difference between `==` and `===` in JavaScript?**  
   `==` checks for value equality, performing type coercion if necessary, whereas `===` checks for both value and type equality, without performing any type conversion.

7. **What is the use of the `bind()` method in JavaScript?**  
   The `bind()` method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

8. **How does `this` work in JavaScript?**  
   The value of `this` is determined by how a function is called. In a method, `this` refers to the owner object. In a function, `this` refers to the global object (in non-strict mode). In an event handler, `this` refers to the element that the event is bound to.

9. **What are Generators in JavaScript and how are they different from regular functions?**  
   Generators are special functions that can be paused and resumed, defined using the `function*` syntax. Unlike regular functions that return a single value, generators can yield multiple values over time using the `yield` keyword.

10. **Explain the concept of the 'Prototype Chain'.**  
    The prototype chain is a mechanism by which JavaScript objects inherit properties and methods from other objects. Every object has a prototype, and if a property is not found on the object itself, JavaScript looks up the prototype chain until it finds it or reaches the end of the chain (null).

---