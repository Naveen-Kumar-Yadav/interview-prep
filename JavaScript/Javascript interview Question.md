JavaScript

JavaScript is a dynamic computer programming language. It is lightweight and most commonly used as a part of web pages, whose implementations allow client-side script to interact with the user and make dynamic pages. It is an interpreted programming language with object-oriented capabilities.

DOM: It is an html documentation, it separates html object elements tags,Model,seperate how to keep object element,It arranges the object element .

Data Type
Primitive:-Number,Boolean,Null,Undefined,String
Non-Primitive:-Object,Array

Data Types
Description
Example
String
represents textual data
'hello', "hello world!" etc
Number
an integer or a floating-point number
3, 3.234, 3e-2 etc.
BigInt
an integer with arbitrary precision
900719925124740999n , 1n etc.
Boolean
Any of two values: true or false
true and false
undefined
a data type whose variable is not initialised
let a;
null
denotes a null value
let a = null;
Symbol
data type whose instances are unique and immutable
let value = Symbol('hello');
Object
key-value pairs of collection of data
let student = { };

URL:-https://www.geeksforgeeks.org/primitive-and-non-primitive-data-types-in-javascript/



Difference between var let and const

var => Global Scope, re-declare, re-assign.
let => Block scope, cannot redeclare, re-assign.
const => Block scope, cannot redeclare, can't re-assign.

 ====Var =====           =====Let====       ====Const=====   
var a = "naveen";         let a = "naveen";      const a = "naveen";
va ar = "naveen";              a = "naveen";                a = "kumar";
{                                       {                                      {
  var a = "Kumar";             var b = "Kumar";            var b = "Kumar";       
}                                        }                                       }     
console.log(a);               console.log(a);                console.log(a);
                                       console.log(b);                console.log(b);
                           


URL 
https://www.programiz.com/javascript/let-vs-var
https://www.freecodecamp.org/news/understanding-let-const-and-var-keywords/#:~:text=Once%20you've%20declared%20a,a%20new%20value%20at%20all.

What are the possible ways to create objects in JavaScript

  There are many ways to create objects in javascript as below

   1. Object constructor:

 The simplest way to create an empty object is using the Object constructor. Currently this             approach is not recommended.

            var object = new Object(); 

2. Object's create method: 

The create method of Object creates a new object by passing the prototype object as a parameter

           var object = Object.create(null);			

3. Object literal syntax:

 The object literal syntax (or object initializer), is a comma-separated set of name-value pairs wrapped in curly braces.

var object = {
name: "Sudheer"
age: 34
};

4. Function constructor:

Create any function and apply the new operator to create object instances,

function Person(name) {
this.name = name;
this.age = 21;
}
var object = new Person("Sudheer");

5. Function constructor with prototype:

This is similar to function constructor but it uses prototype for their properties and methods,

function Person() {}
Person.prototype.name = "Sudheer";
var object = new Person();

This is equivalent to an instance created with an object create method with a function prototype and then call that function with an instance and parameters as arguments.

function func {};
new func(x, y, z);

(OR)
// Create a new instance using function prototype.
var newInstance = Object.create(func.prototype)
// Call the function
var result = func.call(newInstance, x, y, z),
// If the result is a non-null object then use it otherwise just use the new instance.
console.log(result && typeof result === 'object' ? result : newInstance);

6. ES6 Class syntax:

ES6 introduces class feature to create the objects

class Person {
constructor(name) {
this.name = name;
}
}
var object = new Person("Sudheer");

7. Singleton pattern:

A Singleton is an object which can only be instantiated one time. Repeated calls to its constructor return the same instance and this way one can ensure that they don't accidentally create multiple instances.

var object = new (function () {
this.name = "Sudheer";
})();


2. What is a prototype chain

Prototype chaining is used to build new types of objects based on existing ones. It is similar to inheritance in a class based language.

The prototype on object instance is available throughObject.getPrototypeOf(object) or **proto** property whereas prototype on constructors function is available through Object.prototype.

 https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain

https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes

 Video
  https://www.youtube.com/watch?v=AYzjeA7Hw2I

  https://www.youtube.com/watch?v=pCt672Dq05M
 
 





What is the difference between Call, Apply and Bind 

The difference between Call, Apply and Bind can be explained with below examples,

Call: The call() method invokes a function with a given this value and arguments provided one by one

var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };
function invite(greeting1, greeting2) {
console.log(
greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2
);
}
invite.call(employee1, "Hello", "How are you?"); // Hello John Rodson, How are you?
invite.call(employee2, "Hello", "How are you?"); // Hello Jimmy Baily, How are you?

Apply: Invokes the function with a given this value and allows you to pass in arguments as an array

var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };
function invite(greeting1, greeting2) {
console.log(
greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2
);
}
invite.apply(employee1, ["Hello", "How are you?"]); // Hello John Rodson, How are you?
invite.apply(employee2, ["Hello", "How are you?"]); // Hello Jimmy Baily, How are you?

bind: returns a new function, allowing you to pass any number of arguments

var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };
function invite(greeting1, greeting2) {
console.log(
greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2
);
}
var inviteEmployee1 = invite.bind(employee1);
var inviteEmployee2 = invite.bind(employee2);
inviteEmployee1("Hello", "How are you?"); // Hello John Rodson, How are you?
inviteEmployee2("Hello", "How are you?"); // Hello Jimmy Baily, How are you?

Call and apply are pretty interchangeable. Both execute the current function immediately. You need to decide whether it’s easier to send in an array or a comma separated list of arguments. You can remember by treating Call is for comma (separated list) and Apply is for Array.

Whereas Bind creates a new function that will have this set to the first parameter passed to bind().

This method is predefined and built in javascript.
Bind return value

https://www.youtube.com/watch?v=rRAvhzux-7Y
What is JSON and its common operations

JSON is a text-based data format following JavaScript object syntax, which was popularised by Douglas Crockford . It is useful when you want to transmit data across a network and it is basically just a text file with an extension of .json, and a MIME type of application/json
Parsing: Converting a string to a native object
JSON.parse(text);
Stringification: converting a native object to a string so it can be transmitted across the network
JSON.stringify(object);

What is the purpose of the array slice method

The slice() method returns the selected elements in an array as a new array object. It selects the elements starting at the given start argument, and ends at the given optional end argument without including the last element. If you omit the second argument then it selects till the end.

Some of the examples of this method are,

let arrayIntegers = [1, 2, 3, 4, 5];
let arrayIntegers1 = arrayIntegers.slice(0, 2); // returns [1,2]
let arrayIntegers2 = arrayIntegers.slice(2, 3); // returns [3]
let arrayIntegers3 = arrayIntegers.slice(4); //returns [5]

Note: Slice method won't mutate the original array but it returns the subset as a new array.

What is the purpose of the array splice method

The splice() method is used to either add/remove items to/from an array, and then returns the  removed item. The first argument specifies the array position for insertion or deletion whereas the optional second argument indicates the number of elements to be deleted. Each additional argument is added to the array.

Some of the examples of this method are,

let arrayIntegersOriginal1 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal2 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal3 = [1, 2, 3, 4, 5];
let arrayIntegers1 = arrayIntegersOriginal1.splice(0, 2); // returns [1, 2]; original array: [3, 4, 5]
let arrayIntegers2 = arrayIntegersOriginal2.splice(3); // returns [4, 5]; original array: [1, 2, 3]
let arrayIntegers3 = arrayIntegersOriginal3.splice(3, 1, "a", "b", "c"); //returns [4]; original array: [1, 2, 3, "a", "b", "c

Note: Splice method modifies the original array and returns the deleted array.

What is the difference between slice and splice

Some of the major difference in a tabular form
Slice
Splice
Doesn't modify the original
array(immutable)
Returns the subset of original array
Modifies the original array(mutable)

Returns the deleted elements as array
Used to pick the elements from array
Used to insert or delete elements to/from array




What is the difference between == and === operators

JavaScript provides both strict(===, !==) and type-converting(==, !=) equality comparison. The strict operators take type of variable in consideration, while non-strict operators make type correction/conversion based upon values of variables. The strict operators follow the below conditions for different types

1. Two strings are strictly equal when they have the same sequence of characters, same length, and same characters in corresponding positions.
2. Two numbers are strictly equal when they are numerically equal. i.e, Having the same number value. There are two special cases in this,
         1. NaN is not equal to anything, including NaN.
         2. Positive and negative zeros are equal to one another
3. Two Boolean operands are strictly equal if both are true or both are false.
4. Two objects are strictly equal if they refer to the same Object.
5. Null and Undefined types are not equal with ===, but equal with ==. i.e, null===undefined --> false but null==undefined --> true

Some of the example which covers the above cases,

0 == false // true
0 === false // false
1 == "1" // true
1 === "1" // false
null == undefined // true
null === undefined // false
'0' == false // true
'0' === false // false
[]==[] or []===[] //false, refer different objects in memory
{}=={} or {}==={} //false, refer different objects in memory


What are lambda or arrow functions

An arrow function is a shorter syntax for a function expression and does not have its own this, arguments, super, or new.target . These functions are best suited for non-method functions, and they cannot be used as constructors.


What is a first class function

In Javascript, functions are first class objects. First-class functions means when functions in that language are treated like any other variable.

For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable. For example, in the below example, handler functions assigned to a listener
const handler = () => console.log("This is a click handler function"); document.addEventListener("click", handler

Call Apply Bind method



 const obj = {
     fname:"Naveen",
     lastName: "Yadav"
 }
 
  function greeting( profession ){
      return this.fname + " " + this.lastName + " " + profession
  }

Call:  The call() method calls a function with a given value and arguments provided individually.



Example

 console.log(greeting.call(obj,"Software Engineer"))
 
Apply : The call() method calls a function with a given value and arguments provided array.


 console.log(greeting.apply(obj,["Software Engineer"]))
 
Bind: The bind() method creates a new function that, when called, has its keyword set to the provided value.

Example

 const newFunc = greeting.bind(obj)
 
 console.log(newFunc("Software Engineer"),"Bind method") 


Polyfill.
A polyfill in JavaScript is a piece of code (usually JavaScript code) that provides functionality that is not natively supported in some web browsers. It essentially "fills in" the gaps, allowing developers to use newer features or APIs that may not be available in older browser versions.
Agar koi function browser support nahi karta h . To ham ese implement karne ke liye polyfill ka use karte h
Key Points About Polyfills:
Backward Compatibility: Polyfills enable developers to use modern web standards and features without worrying about browser compatibility. For example, if you want to use Array.prototype.includes(), which is not available in Internet Explorer, you can use a polyfill that defines this method if it is not already present.
Implementation of New Features: Polyfills often mimic new JavaScript APIs or methods using older JavaScript syntax and constructs that are more widely supported. This allows developers to write code using the latest standards while maintaining compatibility with older browsers.
Examples of Polyfills:
Promise: For browsers that do not support Promises, a polyfill like the es6-promise library can be used.
fetch: Polyfills like whatwg-fetch provide the fetch API in environments that do not support it.
Object.assign: Provides a polyfill for environments that do not support Object.assign natively.
Usage: Polyfills are often included conditionally in web applications. Tools like Babel can also automatically add polyfills for the specific environments targeted by your codebase, ensuring that only the necessary polyfills are included.





"Temporal Dead Zone" (TDZ) ek programming term hai jo JavaScript ke context mein use hota hai, khas kar ES6 (ECMAScript 2015) ke "let" aur "const" keywords ke sath. TDZ tab hota hai jab ek variable ko declare kiya gaya hai, lekin uski value ko initialize nahi kiya gaya hai.
Iska matlab hai ki jab tak aap variable ko declare nahi kar lete, aap us variable ko access nahi kar sakte. Agar aap access karne ki koshish karte hain, to aapko "ReferenceError" milta hai.
Example:
javascript

console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 5;

Yahaan, a ko declare kiya gaya hai let keyword ke sath, lekin jab aap console.log(a) ko call karte hain, tab a TDZ mein hota hai, isliye aapko error milta hai. TDZ tab tak continue hoti hai jab tak variable ko declare aur initialize nahi kar diya jata.
Yeh behavior var keyword ke sath nahi hota. var ke sath, variables hoisting ke through accessible hote hain, lekin unki values undefined hoti hain agar initialization se pehle access kiya jaye.
TDZ ka primary purpose variable declaration aur initialization ko ensure karna hai, taaki code ki readability aur debugging process behtar ho.


The "Temporal Dead Zone" (TDZ) is a programming term used in the context of JavaScript, particularly with the let and const keywords introduced in ES6 (ECMAScript 2015). TDZ occurs when a variable has been declared but not yet initialized.
This means that until you declare and initialize the variable, you cannot access it. If you try to access it before the declaration, you'll get a ReferenceError.
Example:

console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 5;

Here, a is declared with the let keyword, but when you try to console.log(a), a is in the TDZ, and hence you get an error. The TDZ persists until the variable is declared and initialized.
This behavior does not apply to the var keyword. With var, variables are hoisted and accessible, but they are undefined if accessed before initialization.
The primary purpose of TDZ is to ensure that variables are declared and initialized properly before use, which improves code readability and debugging.

Closure 
A closure is a programming concept where an inner function retains access to the variables of its outer function even after the outer function has finished executing. This allows the inner function to remember and use the outer function’s variables.
Hindi Explanation.
Closure ek programming concept hai jo JavaScript aur kai dusre programming languages mein use hota hai. Closure tab banta hai jab ek function apni outer function ke scope ke variables ko access karta hai, even though outer function apni execution complete kar chuki hoti hai.
Conceptual Explanation:
Inner Function Access: Closure ke zariye, ek inner function outer function ke variables ko access kar sakta hai, jo outer function ke scope ke part hote hain.
Persistent Scope: Closure ke zariye, variables jo outer function ke scope ka part hain, unki values ko "remember" kiya ja sakta hai, even after the outer function has finished executing.
Example:
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable) {
    console.log("Outer Variable: " + outerVariable);
    console.log("Inner Variable: " + innerVariable);
  };
}

const closureFunction = outerFunction("I'm outside!");
closureFunction("I'm inside!");

Explanation:
outerFunction ek outer function hai jo ek outerVariable ko accept karta hai aur ek inner function innerFunction return karta hai.
innerFunction outerVariable aur innerVariable dono ko access kar sakta hai.
Jab closureFunction ko call kiya jata hai, to outerVariable ki value ko bhi access kiya ja sakta hai, jo closure ke zariye possible hota hai.
Key Points:
Enclosing Scope: Closure ensures that the inner function retains access to the variables of its enclosing (outer) function.
Data Encapsulation: Closures can be used to create private variables or methods, thereby encapsulating data.
Closures are a powerful feature in JavaScript that enable various programming patterns and can be used for data encapsulation, function factories, and more.

Closures ka use programming mein kai tarikon se hota hai. Yeh powerful feature hai jo flexibility aur functionality provide karta hai. Yahan kuch key reasons hain jinke liye closures ka use kiya jata hai:

Why use?.

1. Data Encapsulation (Private Variables):
Closures ka use private variables aur methods create karne ke liye hota hai. JavaScript mein, closures ko use karke aap data ko encapsulate kar sakte hain aur variables ko private rakh sakte hain jo directly access nahi kiye ja sakte.
Example:

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

Is example mein, count variable createCounter function ke scope ke andar encapsulated hai aur counter function ke through hi access aur modify kiya ja sakta hai.
2. Function Factories:
Closures ko function factories banane ke liye use kiya jata hai. Aap ek function create kar sakte hain jo specific configuration ke saath multiple functions create karta hai.
Example:
function makeMultiplier(multiplier) {
  return function(value) {
    return value * multiplier;
  };
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15

Yahaan, makeMultiplier function ek multiplier value ko accept karta hai aur ek function return karta hai jo is multiplier ke saath value ko multiply karta hai.
3. Maintaining State:
Closures ko use karke aap state ko maintain kar sakte hain across multiple function calls. Yeh especially useful hota hai jab aapko function ke state ko preserve karna hota hai.
Example:
function createGreeting(greeting) {
  return function(name) {
    return greeting + ', ' + name;
  };
}

const sayHello = createGreeting('Hello');
console.log(sayHello('Alice')); // Hello, Alice
console.log(sayHello('Bob')); // Hello, Bob

Is example mein, greeting variable createGreeting function ke closure ke part hai aur isko sayHello function ke through access kiya ja sakta hai.
4. Partial Application and Currying:
Closures ko partial application aur currying ke techniques mein bhi use kiya jata hai, jo functions ko partially apply karke re-useable functions create karne mein help karte hain.
Example:
function add(a) {
  return function(b) {
    return a + b;
  };
}

const addFive = add(5);
console.log(addFive(10)); // 15

Yahaan, add function ek partial application create karta hai jahan a value fix hoti hai aur b value ko dynamically provide kiya jata hai.
5. Asynchronous Programming:
Closures ka use asynchronous programming mein bhi hota hai, jahan functions callbacks aur promises ke saath deal karte hain aur closures ke zariye state aur variables ko manage karte hain.
Example:
function asyncOperation() {
  let result = 0;
  setTimeout(function() {
    result = 42;
    console.log('Async operation result:', result);
  }, 1000);
}

asyncOperation();

Is example mein, result variable ko setTimeout callback function ke zariye access kiya jata hai, jo closure ki madad se possible hota hai.
Closures ka use karke aap code ko modular, reusable, aur maintainable bana sakte hain, aur complex programming patterns ko simplify kar sakte hain.

Currying 
Currying ek functional programming technique hai jo JavaScript mein use hoti hai. Currying ka matlab hai ek function ko aise transform karna ki woh multiple arguments ko ek ek karke accept kare, rather than taking all arguments at once.
Concept:
Function Transformation: Currying transforms a function that takes multiple arguments into a series of functions, each taking a single argument.
Partial Application: It allows partial application of function arguments, meaning you can provide some arguments and get a new function that expects the remaining arguments.
How It Works:
Basic Function: A function that normally takes multiple arguments.
Curried Function: Transforms this function into a series of functions where each function takes one argument.
Example:
javascript
Copy code
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

Explanation:
Normal Function: multiply takes two arguments a and b and returns their product.
Curried Function: curriedMultiply takes one argument a and returns a new function that takes another argument b and returns the product of a and b.
Partial Application: multiplyBy2 is a partially applied function where a is fixed to 2. It can now be used to multiply any number by 2.
Benefits:
Modularity: Currying allows for more modular and reusable code.
Function Composition: It helps in composing functions and creating more specific functions from general ones.
Lazy Evaluation: It supports lazy evaluation, where functions can be applied incrementally.
Currying is widely used in functional programming and can be very powerful in JavaScript for creating flexible and reusable functions.






