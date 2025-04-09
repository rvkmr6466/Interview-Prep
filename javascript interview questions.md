## Basic JavaScript - Interview Answers
1. ### What are the different data types in JavaScript?
JavaScript has:
- Primitive Types: String, Number, Boolean, Undefined, Null, BigInt, and Symbol.
- Non-Primitive Type: Object (includes Arrays, Functions, etc.)

2. ### What is the difference between var, let, and const?
- var is function-scoped, can be re-declared and updated.
- let is block-scoped, cannot be re-declared but can be updated.
- const is block-scoped, cannot be re-declared or updated (though objects/arrays can be mutated).

3. ### What is hoisting in JavaScript?
Hoisting is a behavior where variable and function declarations are moved to the top of their scope before code execution.
- var is hoisted with undefined.
- let and const are hoisted but not initialized (they stay in a temporal dead zone until declared).

4. ### What are truthy and falsy values?
- Falsy values: false, 0, '', null, undefined, NaN
- Everything else is truthy (e.g., '0', [], {}, 'false', etc.)

5. ### What is the difference between == and ===?
- == compares values with type coercion.
- === compares values and types strictly (no coercion).
 ```
 2 == '2'  // true
 2 === '2' // false
 ```
6. ### What is a closure in JavaScript?
A closure is a function that has access to its outer function’s scope even after the outer function has returned.
 ```
 function outer() {
    let count = 0;
    return function inner() {
       count++;
       return count;
    };
 }
 
 const counter = outer();
 counter(); // 1
 ```

7. ### How does the this keyword work?
- In regular functions, this refers to the object that calls the function.
- In arrow functions, this is lexically bound (refers to this of the outer scope).
- In the global context (non-strict mode), this refers to window in browsers.

8. ### What is the difference between null and undefined?
- null: Explicitly means “no value”.
- undefined: A variable declared but not assigned a value.

9. ### What is event bubbling and event capturing?
- Bubbling: Event starts from the target element and bubbles up to the parent.
- Capturing: Event starts from the parent and goes down to the target element.
- Default behavior is bubbling.

10. ### How does the typeof operator work?
typeof is used to get the data type of a variable.
 ```
 Example:
  typeof "hello"  // "string"
  typeof 123       // "number"
  typeof undefined // "undefined"
  typeof null      // "object" (quirk in JS)
  ```

## Functions & Scope – Interview Answers
1. ### What are arrow functions and how are they different from regular functions?
- Arrow functions are a shorter syntax for writing functions introduced in ES6.
- They do not have their own this, arguments, or super, and are not suitable for methods.
 ```
 const add = (a, b) => a + b;
 ```

- Traditional functions have their own this depending on the caller:
 ```
 function sayHi() {
    console.log(this);
 }
 ```

2. ### What is a callback function?
A callback is a function passed as an argument to another function, which is then called after a task is completed.
 ```
 function greet(name, callback) {
    console.log("Hi " + name);
    callback();
 }

 greet("John", () => console.log("Callback executed"));
 ```

3. ### What is a higher-order function?
A function that takes another function as an argument or returns a function is called a higher-order function.
 ```
 function multiplier(factor) {
    return function (number) {
       return number * factor;
    };
 }

 const double = multiplier(2);
 double(5); // 10
 ```

4. ### What is the scope of a variable in JavaScript?
- Global Scope: Available everywhere.
- Function Scope: var is function-scoped.
- Block Scope: let and const are block-scoped (only available inside {}).

 ```
 if (true) {
    var x = 10;
    let y = 20;
 }
 console.log(x); // 10
 console.log(y); // ReferenceError
 ```
5. ### What is the difference between function declaration and function expression?
- Function Declaration: Can be hoisted.
 ```
 function greet() {
    console.log("Hello");
 }
 ```

- Function Expression: Not hoisted. ### Stored in a variable.
 ```
 const greet = function () {
   console.log("Hello");
 };
 ```

## Asynchronous JavaScript – Interview Answers
1. ### What is the event loop in JavaScript?
- The event loop is what allows JavaScript (which is single-threaded) to perform non-blocking operations.
- It continuously checks the call stack and task queue, and executes queued tasks when the call stack is empty.
- It enables handling of callbacks, promises, and DOM events.

2. ### What is the difference between setTimeout and setInterval?
- setTimeout(fn, delay): Executes fn once after the delay.
- setInterval(fn, interval): Repeatedly executes fn every interval milliseconds.
 ```
 setTimeout(() => console.log("Once"), 1000);
 setInterval(() => console.log("Repeat"), 1000);
 ```
3. ### What are Promises and how do they work?
- Promises are used to handle asynchronous operations.
- They have three states: pending, fulfilled, and rejected.
- Use .then() and .catch() to handle the result.
 ```
 const promise = new Promise((resolve, reject) => {
    let success = true;
   success ? resolve("Done") : reject("Failed");
 });
 
 promise.then(console.log).catch(console.error);
 ```

4. ### What is async/await and how does it improve asynchronous code?
- async/await is syntax sugar over Promises.
- It makes asynchronous code look synchronous and is easier to read and maintain.
- Must be used inside an async function.

 ```
 async function getData() {
    try {
       const response = await fetch('https://api.example.com');
       const data = await response.json();
       console.log(data);
    } catch (error) {
       console.error(error);
    }
 }
 ```

5. ### What is the difference between microtask and macrotask queues?
- Microtasks: Include Promises (.then()), MutationObserver.
- Macrotasks: Include setTimeout, setInterval, setImmediate, and I/O.
  Microtasks are prioritized and executed before the next macrotask.

## Objects, Arrays & ES6 Features – Interview Answers
1. ### What are the different ways to clone an object in JavaScript?
- Shallow Copy:
 ```
 const obj1 = { a: 1 };
 const obj2 = Object.assign({}, obj1);
 const obj3 = { ...obj1 };
 ```
- Deep Copy (removes reference from nested objects):
 ```
 const deepCopy = JSON.parse(JSON.stringify(obj1)); // not ideal for all cases
 ```

2. ### What are destructuring assignments?
Destructuring allows you to extract values from arrays or objects into variables.

 ```
 const user = { name: "Alice", age: 25 };
 const { name, age } = user; // name = "Alice", age = 25

 const arr = [1, 2, 3];
 const [a, b] = arr; // a = 1, b = 2
 ```

3. ### What are template literals?
Template literals are string literals that allow embedded expressions using backticks (`).
```
const name = "John";
console.log(`Hello, ${name}!`); // Hello, John!
```

4. ### What is the spread operator (...) and rest parameter?
- Spread Operator: Expands iterable elements.
 ```
 const arr1 = [1, 2];
 const arr2 = [...arr1, 3]; // [1, 2, 3]
 ```

- Rest Parameter: Gathers arguments into an array.
 ```
 function sum(...numbers) {
    return numbers.reduce((a, b) => a + b);
 }
 ```

5. ### What is the difference between map(), filter(), and reduce() methods?
- map(): Transforms each element and returns a new array.
 ```
 [1, 2, 3].map(x => x * 2); // [2, 4, 6]
 ```
- filter(): Filters elements based on condition.
 ```
 [1, 2, 3].filter(x => x > 1); // [2, 3]
 ```
- reduce(): Reduces the array to a single value.
 ```
 [1, 2, 3].reduce((acc, val) => acc + val, 0); // 6
 ```

## DOM & Events – Interview Answers
1. ### What is the DOM and how do you manipulate it with JavaScript?
- The DOM (Document Object Model) is a tree structure representation of the HTML document.
- JavaScript can access and manipulate it using methods like:
 ```
 document.getElementById("id");
 document.querySelector(".class");
 element.innerHTML = "new content";
 element.style.color = "red";
 ```

2. ### What are event listeners and how are they used?
- Event listeners allow you to execute code when a specific event occurs.
 ```
 const button = document.querySelector("button");
 button.addEventListener("click", () => {
    alert("Button clicked!");
 });
 ```

3. ### What is the difference between innerHTML, innerText, and textContent?
- innerHTML: Gets/sets HTML content (includes tags).
- innerText: Gets/sets visible text content (excludes hidden elements and formatting).
- textContent: Gets/sets all text content (includes hidden elements, faster than innerText).
 ```
 element.innerHTML = "<b>Bold</b>";
 element.innerText = "<b>Bold</b>";     // displays tags as text
 element.textContent = "<b>Bold</b>";   // same as above
 ```
4. ### How do you prevent default behavior in an event handler?
Use event.preventDefault() inside the event listener to prevent the default action (like form submission, link redirect).
 ```
 document.querySelector("form").addEventListener("submit", function(e) {
    e.preventDefault();
  console.log("Form submission prevented!");
 });
 ```

5. ### What is event delegation?
- Event delegation is a technique where a parent element handles events from its child elements.
- It’s efficient because you don’t need to attach listeners to each child.
 ```
 document.getElementById("list").addEventListener("click", function(e) {
    if (e.target.tagName === "LI") {
      console.log("Item clicked:", e.target.textContent);
    }
 });
```

## Advanced JavaScript – Interview Answers
1. ### What is a prototype in JavaScript?
- Every JavaScript object has a hidden internal property called [[Prototype]], accessible via .prototype (for functions/constructors) or **__proto__**.
- It allows inheritance of properties and methods.
  ```
  function Person(name) {
    this.name = name;
  }

  Person.prototype.sayHello = function () {
    console.log(`Hi, I'm ${this.name}`);
  };

  const john = new Person("John");
  john.sayHello(); // Hi, I'm John
  ```

2. ### What is prototypal inheritance?
- It’s a feature in JavaScript where an object can inherit properties and methods from another object using its prototype chain.
- This is done through Object.create(), constructor functions, or ES6 class syntax.
 ```
 const parent = { greet() { console.log("Hello!"); } };
 const child = Object.create(parent);
 child.greet(); // Hello!
 ```

3. ### What is the difference between deep copy and shallow copy?
- Shallow Copy: Copies only the top-level properties.
 ```
 const obj1 = { a: 1, b: { c: 2 } };
 const shallow = { ...obj1 };
 shallow.b.c = 99; // changes original too
 ```
- Deep Copy: Copies all nested levels.
 ```
 const deep = JSON.parse(JSON.stringify(obj1));
 ```

4. ### How does JavaScript handle memory management?
- JavaScript uses automatic garbage collection.
- Memory is allocated when variables/objects are created and deallocated when no longer referenced.
- Common issue: memory leaks from closures, unused event listeners, or global variables.

5. ### What is a module in JavaScript (ES6 modules)?
- ES6 introduced native module support using export and import.
- Modules help organize and reuse code.
 ```javascript 
 math.js

 export function add(a, b) {
    return a + b;
 }
 ```
 ```javascript
 main.js

 import { add } from './math.js';
 console.log(add(2, 3)); // 5
 ```
    ```
