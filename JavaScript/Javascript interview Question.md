# JavaScript Interview Questions

## 1. What is a closure?
A closure is a feature in JavaScript where an inner function has access to the outer function's variables. It allows create private variables.
```javascript
function outerFunction() {
    let outerVariable = 'I am from outer function!';
    function innerFunction() {
        console.log(outerVariable);
    }
    return innerFunction;
}

const innerFunc = outerFunction();
innerFunc(); // Output: I am from outer function!
```

## 2. What is the difference between `==` and `===`?
`==` checks for value equality with type coercion, while `===` checks for both value and type equality.
```javascript
console.log(1 == '1'); // true
console.log(1 === '1'); // false
```

## 3. Explain the concept of promises in JavaScript.  
A promise is an object that represents the eventual completion or failure of an asynchronous operation and its resulting value. Promises can be in one of three states: pending, fulfilled, or rejected.  
```javascript
const myPromise = new Promise((resolve, reject) => {
    // Asynchronous operation
    const success = true;
    if (success) {
        resolve('Operation successful!');
    } else {
        reject('Operation failed!');
    }
});

myPromise
    .then(result => console.log(result))
    .catch(error => console.log(error));
```

## 4. Describe event delegation and how it works.
Event delegation is a technique in which a single event listener is added to a parent element to manage events for multiple child elements. When the event occurs, it bubbles up to the parent where the event listener is defined.

```html
<ul id="parent">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
<script>
    document.getElementById('parent').addEventListener('click', function(event) {
        if(event.target.tagName === 'LI') {
            console.log(event.target.textContent);
        }
    });
</script>
```

## 5. What is the purpose of the `bind` method?
The `bind` method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.
```javascript
function greet() {
    console.log(`Hello, ${this.name}`);
}

const person = { name: 'John' };
const greetPerson = greet.bind(person);
greetPerson(); // Output: Hello, John
```
