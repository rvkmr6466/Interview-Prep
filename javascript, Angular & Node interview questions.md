## Basic JavaScript - Interview Answers
### Q. What are the different data types in JavaScript?
JavaScript has:
- Primitive Types: String, Number, Boolean, Undefined, Null, BigInt, and Symbol.
- Non-Primitive Type: Object (includes Arrays, Functions, etc.)

### Q. What is the difference between var, let, and const?
- `var` is function-scoped, can be re-declared and updated.
- `let` is block-scoped, cannot be re-declared but can be updated.
- `const` is block-scoped, cannot be re-declared or updated (though objects/arrays can be mutated).

### Q. What is hoisting in JavaScript?
Hoisting is a behavior where variable and function declarations are moved to the top of their scope before code execution.
- `var` is hoisted with undefined.
- `let` and `const` are hoisted but not initialized (they stay in a temporal dead zone until declared).

### Q. What are truthy and falsy values?
- Falsy values: false, 0, '', null, undefined, NaN
- Everything else is truthy (e.g., '0', [], {}, 'false', etc.)

### Q. What is the difference between == and ===?
- == compares values with type coercion.
- === compares values and types strictly (no coercion).
 ```javascript
 2 == '2'  // true
 2 === '2' // false
 ```
### Q. What is a closure in JavaScript?
A closure is a function that has access to its outer function’s scope even after the outer function has returned.
```javascript
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

### Q. How does the `this` keyword work?
- In regular functions, `this` refers to the object that calls the function.
- In arrow functions, `this` is lexically bound (refers to `this` of the outer scope).
- In the global context (non-strict mode), `this` refers to window in browsers.

### Q. What is the difference between null and undefined?
- `null`: Explicitly means `no value`.
- `undefined`: A variable declared but not assigned a value.

### Q. What is event bubbling and event capturing?
- `Bubbling`: Event starts from the target element and bubbles up to the parent.
- `Capturing`: Event starts from the parent and goes down to the target element.
- Default behavior is bubbling.

### Q. How does the typeof operator work?
typeof is used to get the data type of a variable.
 Example:
```javascript
typeof "hello"  // "string"
typeof 123       // "number"
typeof undefined // "undefined"
typeof null      // "object" (quirk in JS)
```

## Functions & Scope – Interview Answers
### Q. What are arrow functions and how are they different from regular functions?
- Arrow functions are a shorter syntax for writing functions introduced in ES6.
- They do not have their own this, arguments, or super, and are not suitable for methods.
 ```javascript
 const add = (a, b) => a + b;
 ```

- Traditional functions have their own this depending on the caller:
 ```javascript
 function sayHi() {
    console.log(this);
 }
 ```

### Q. What is a callback function?
A callback is a function passed as an argument to another function, which is then called after a task is completed.
 ```javascript
 function greet(name, callback) {
    console.log("Hi " + name);
    callback();
 }

 greet("John", () => console.log("Callback executed"));
 ```

### Q. What is a higher-order function?
A function that takes another function as an argument or returns a function is called a higher-order function.
 ```javascript
 function multiplier(factor) {
    return function (number) {
       return number * factor;
    };
 }

 const double = multiplier(2);
 double(5); // 10
 ```

### Q. What is the scope of a variable in JavaScript?
- Global Scope: Available everywhere.
- Function Scope: var is function-scoped.
- Block Scope: let and const are block-scoped (only available inside {}).

 ```javascript
 if (true) {
    var x = 10;
    let y = 20;
 }
 console.log(x); // 10
 console.log(y); // ReferenceError
 ```
### Q. What is the difference between function declaration and function expression?
- Function Declaration: Can be hoisted.
 ```javascript
 function greet() {
    console.log("Hello");
 }
 ```

- Function Expression: Not hoisted. #### Stored in a variable.
 ```javascript
 const greet = function () {
   console.log("Hello");
 };
 ```

## Asynchronous JavaScript – Interview Answers
### Q. What is the event loop in JavaScript?
- The event loop is what allows JavaScript (which is single-threaded) to perform non-blocking operations.
- It continuously checks the call stack and task queue, and executes queued tasks when the call stack is empty.
- It enables handling of callbacks, promises, and DOM events.

### Q. What is the difference between setTimeout and setInterval?
- setTimeout(fn, delay): Executes fn once after the delay.
- setInterval(fn, interval): Repeatedly executes fn every interval milliseconds.
 ```javascript
 setTimeout(() => console.log("Once"), 1000);
 setInterval(() => console.log("Repeat"), 1000);
 ```
### Q. What are Promises and how do they work?
- Promises are used to handle asynchronous operations.
- They have three states: `pending`, `fulfilled`, and `rejected`.
- Use `.then()` and `.catch()` to handle the result.

 ```javascript
 const promise = new Promise((resolve, reject) => {
    let success = true;
   success ? resolve("Done") : reject("Failed");
 });
 
 promise.then(console.log).catch(console.error);
 ```

### Q. What is async/await and how does it improve asynchronous code?
- async/await is syntax sugar over Promises.
- It makes asynchronous code look synchronous and is easier to read and maintain.
- Must be used inside an `async` function.

 ```javascript
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

### Q. What is the difference between microtask and macrotask queues?
- Microtasks: Include Promises (`.then())`, `MutationObserver`.
- Macrotasks: Include `setTimeout`, `setInterval`, `setImmediate`, and `I/O`.
  Microtasks are prioritized and executed before the next macrotask.

## Objects, Arrays & ES6 Features – Interview Answers
### Q. What are the different ways to clone an object in JavaScript?
- Shallow Copy:
 ```javascript
 const obj1 = { a: 1 };
 const obj2 = Object.assign({}, obj1);
 const obj3 = { ...obj1 };
 ```
- Deep Copy (removes reference from nested objects):
 ```javascript
 const deepCopy = JSON.parse(JSON.stringify(obj1)); // not ideal for all cases
 ```

### Q. What are destructuring assignments?
Destructuring allows you to extract values from arrays or objects into variables.

```javascript
const user = { name: "Alice", age: 25 };
const { name, age } = user; // name = "Alice", age = 25

const arr = [1, 2, 3];
const [a, b] = arr; // a = 1, b = 2
```

### Q. What are template literals?
Template literals are string literals that allow embedded expressions using backticks (`).
```javascript
const name = "John";
console.log(`Hello, ${name}!`); // Hello, John!
```

### Q. What is the spread operator (...) and rest parameter?
- Spread Operator: Expands iterable elements.
```javascript
const arr1 = [1, 2];
const arr2 = [...arr1, 3]; // [1, 2, 3]
```

- Rest Parameter: Gathers arguments into an array.
```javascript
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b);
}
```

### Q. What is the difference between `map()`, `filter()`, and `reduce()` methods?
- `map()`: Transforms each element and returns a new array.
```javascript
[1, 2, 3].map(x => x * 2); // [2, 4, 6]
```javascript
- filter(): Filters elements based on condition.
```javascript
[1, 2, 3].filter(x => x > 1); // [2, 3]
```
- reduce(): Reduces the array to a single value.
```javascript
[1, 2, 3].reduce((acc, val) => acc + val, 0); // 6
```

## DOM & Events – Interview Answers
### Q. What is the DOM and how do you manipulate it with JavaScript?
- The DOM (Document Object Model) is a tree structure representation of the HTML document.
- JavaScript can access and manipulate it using methods like:
```javascript
document.getElementById("id");
document.querySelector(".class");
element.innerHTML = "new content";
element.style.color = "red";
```

### Q. What are event listeners and how are they used?
- Event listeners allow you to execute code when a specific event occurs.
```javascript
const button = document.querySelector("button");
button.addEventListener("click", () => {
  alert("Button clicked!");
});
```

### Q. What is the difference between innerHTML, innerText, and textContent?
- innerHTML: Gets/sets HTML content (includes tags).
- innerText: Gets/sets visible text content (excludes hidden elements and formatting).
- textContent: Gets/sets all text content (includes hidden elements, faster than innerText).
```javascript
element.innerHTML = "<b>Bold</b>";
element.innerText = "<b>Bold</b>";     // displays tags as text
element.textContent = "<b>Bold</b>";   // same as above
```
### Q. How do you prevent default behavior in an event handler?
Use event.preventDefault() inside the event listener to prevent the default action (like form submission, link redirect).
```javascript
document.querySelector("form").addEventListener("submit", function(e) {
  e.preventDefault();
console.log("Form submission prevented!");
});
 ```

### Q. What is event delegation?
- Event delegation is a technique where a parent element handles events from its child elements.
- It’s efficient because you don’t need to attach listeners to each child.
```javascript
document.getElementById("list").addEventListener("click", function(e) {
  if (e.target.tagName === "LI") {
    console.log("Item clicked:", e.target.textContent);
  }
});
```

## Advanced JavaScript – Interview Answers
### Q. What is a prototype in JavaScript?
- Every JavaScript object has a hidden internal property called [[Prototype]], accessible via .prototype (for functions/constructors) or **__proto__**.
- It allows inheritance of properties and methods.
  ```javascript
  function Person(name) {
    this.name = name;
  }

  Person.prototype.sayHello = function () {
    console.log(`Hi, I'm ${this.name}`);
  };

  const john = new Person("John");
  john.sayHello(); // Hi, I'm John
  ```

### Q. What is prototypal inheritance?
- It’s a feature in JavaScript where an object can inherit properties and methods from another object using its prototype chain.
- This is done through Object.create(), constructor functions, or ES6 class syntax.
 ```javascript
 const parent = { greet() { console.log("Hello!"); } };
 const child = Object.create(parent);
 child.greet(); // Hello!
 ```

### Q. What is the difference between deep copy and shallow copy?
- Shallow Copy: Copies only the top-level properties.
 ```javascript
 const obj1 = { a: 1, b: { c: 2 } };
 const shallow = { ...obj1 };
 shallow.b.c = 99; // changes original too
 ```
- Deep Copy: Copies all nested levels.
 ```javascript
 const deep = JSON.parse(JSON.stringify(obj1));
 ```

### Q. How does JavaScript handle memory management?
- JavaScript uses automatic garbage collection.
- Memory is allocated when variables/objects are created and deallocated when no longer referenced.
- Common issue: memory leaks from closures, unused event listeners, or global variables.

### Q. What is a module in JavaScript (ES6 modules)?
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

## Add-ons questions
### Q. What is javascript and why it is used for backend?
JavaScript (JS) is a high-level, interpreted programming language that is commonly used to create interactive effects within web browsers. It is a dynamic, prototype-based language that supports object-oriented, imperative, and functional programming styles.

Node.js is a runtime environment that allows JavaScript to be executed on the server side. It is used for backend development because:

1. **Event-driven architecture**: Node.js uses an event-driven, non-blocking I/O model, which makes it efficient and suitable for building scalable network applications.
2. **Single language**: Developers can use JavaScript for both frontend and backend development, which simplifies the development process and allows for code reuse.
3. **Package management**: Node.js has a vast ecosystem of libraries and modules through npm (Node Package Manager), which accelerates development by providing reusable code.
4. **Performance**: Node.js is built on the V8 JavaScript engine from Google, which compiles JavaScript to native machine code, resulting in high performance.

### Q. What will be the output?
 ```javascript
 console.log(a);
 var a = 10;
 ```
 _**Output:**_ undefined
 
 ```javascript
 console.log(b);
 let b = 10;
 ```
 _**Output:**_ d is not defined
 ```javascript
 console.log("start");
 setTimeout(()=>{console.log("settimeout1")});
 setTimeout(()=>{console.log("settimeout2")},0);
 Promise.resolve().then(()=>console.log("promise"));
 console.log("end");
 ```
_**Output:**_
start
end
promise
settimeout1
settimeout2
 
**Note:** Promise has more priority than setTimeout.

#### process.nextTick, Promises, setTimeout, and setImmediate
The priority order of `process.nextTick`, `Promises`, `setTimeout`, and `setImmediate` in JavaScript's event loop is: `process.nextTick` (highest) > `Promises` > `setTimeout` > `setImmediate`.  
Explanation:
- _process.nextTick():_ This function always runs before any other task, even before promises. It enqueues a callback to be executed in the next iteration of the event loop, ensuring it gets processed before other tasks that might be waiting.
- _Promises:_ `Promises`, which are microtasks, have a higher priority than macrotasks like `setTimeout` and `setImmediate`. They are executed as soon as the call stack is empty, before the event loop moves to the next macrotask.
- _setTimeout():_ `setTimeout` callbacks are macrotasks and are executed after the call stack is empty and all microtasks (including promises) have been processed. If `setTimeout` has a delay of 0, it will be executed in the next iteration of the event loop, after the microtasks have been completed.
- _setImmediate():_ `setImmediate` is also a macrotask and is executed after the current event loop iteration completes and all microtasks are processed. It is processed in the Check phase, which is later than the Timer phase where setTimeout with 0 delay is processed.

---
### Q. How Asynchronous call works?
Asynchronous calls allow a program to start a task and continue executing other code without waiting for the task to finish, using mechanisms like callbacks or promises to handle the result later. 
Here's a more detailed explanation:
1. **_The Concept of Asynchronous Operations_**
- **Non-Blocking:** Asynchronous operations are non-blocking, meaning the program doesn't halt while waiting for a task to complete. 
- **Parallel Execution:** This allows the program to perform other tasks concurrently, improving efficiency and responsiveness. 
- **Common Use Cases:** Asynchronous operations are crucial for tasks that take time, such as network requests, file I/O, or database operations. 
2. _**How Asynchronous Calls Work**_
- **Initiating the Task:** The program initiates an asynchronous task, such as making a network request. 
- **Continuing Execution:** The program doesn't wait for the task to complete; it continues executing other code. 
- **Handling the Result:** When the task completes, a mechanism (like a callback or promise) is used to notify the program and provide the result. 
- **Callback:** A callback is a function passed as an argument to another function, which is then called when the asynchronous operation is finished. 
- **Promises:** Promises are objects that represent the eventual completion (or failure) of an asynchronous operation and its resulting value. 
3. _**Examples**_
#### **JavaScript:**
- **`setTimeout()`** and **`setInterval()`**  
  Used to execute code after a delay or at regular intervals, respectively. These functions demonstrate asynchronous behavior in JavaScript.
- **`fetch()`**  
  Utilized to make network requests. It operates asynchronously and returns a **Promise**, allowing you to handle the response once it's available.
- **`addEventListener()`**  
  Enables attaching event handlers (callbacks) to events such as button clicks, key presses, or form submissions. These handlers are executed asynchronously when the specified event occurs.

---

### Q. Add a delay of two second between two console.log.
```javascript
console.log(1);
await new Promise(resolve => setTimeout(resolve, 3000)); // 3 sec
console.log(2);
```
---

### Q. Find Output
```javascript
let obj1 = { key: "value" };
let obj2 = obj1;
let obj3 = obj2;
obj1.key = "new value";
obj2 = { key: "another value" };
console.log(obj1.key); 
console.log(obj2.key); 
console.log(obj3.key); 
```
Output=>
new value
another value
new value

---

### Q. Reverse string and remove duplicate in javascript
```javascript
let s = "ravi Kumar";
let s1 ="";
let s3 = "";
let arr = s.split("");
let s2 = new Set(arr);

for(let i=s.length-1; i>=0; i--) {
    s3+=s[i];
    if (!s1.includes(s[i])) {
        s1+=s[i];
    }
}
console.log(s1); // ramuK iv
console.log(s3); // ramuK ivar
```
---
### Q. Middleware in Node.js
Middleware in Node.js refers to functions that intercept requests before they reach the final route handler. These functions have access to the request object (`req`), the response object (`res`), and the `next()` function, which allows them to pass control to the subsequent middleware in the chain. Middleware functions can perform a variety of tasks, including modifying request or response objects, executing code, ending the request-response cycle, or calling the next middleware function.
There are several types of middleware: 
- _Application-level middleware:_ Bound to an instance of `express` using `app.use()`. It applies to all routes defined after it. 
- _Router-level middleware:_ Bound to an instance of `express.Router()`. It applies only to the routes defined within that router. 
- _Third-party middleware:_ External packages installed via npm, such as `body-parser` or `cookie-parser`, which add specific functionalities. 
- _Built-in middleware:_ Included with Express, like `express.static` for serving static files or `express.json` for parsing JSON request bodies. 
- _Error-handling middleware:_ Functions with four arguments (`err`, `req`, `res`, `next`) that handle errors passed down the middleware chain.

Middleware is useful for tasks like: 
- Authentication and authorization 
- Logging 
- Request parsing (e.g., JSON, URL-encoded data) 
- Serving static files 
- Error handling

```javascript
const express = require('express');
const app = express();

// Application-level middleware
app.use((req, res, next) => {
  console.log('Time:', Date.now());
  next();
});

// Route-specific middleware
const myLogger = (req, res, next) => {
  console.log('LOGGED');
  next();
};

app.get('/example', myLogger, (req, res) => {
  res.send('Example Route');
});

// Error-handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```
---
### Q. Implement a function fn in JavaScript that can be invoked multiple times in a chain, where each call increments a count of how many times it was invoked. When the final call is made with 0 as an argument, the function should return the total number of times it was previously invoked in the chain. // Examples: // fn()()()(0) should return 3 because fn was called 3 times before passing 0. // fn()()()()()(0) should return 5 because fn was called 5 times before passing 0.
```javascript
function fn(count = 1) {
  return function inner(arg) {
    if (arg === 0) {
      return count;
    }
    return fn(count + 1);
  };
}

console.log(fn()()()()(0));
```
---
### Q. Streams in NodeJS
In Node.js, streams facilitate handling streaming data, allowing data to be processed piece by piece. This approach is efficient for working with large datasets, such as files or network communications, as it avoids loading the entire dataset into memory at once. 
There are four main types of streams:
- _Readable_: Used for reading data from a source. 
- _Writable_: Used for writing data to a destination. 
- _Duplex_: Combines both readable and writable streams. 
- _Transform_: A type of duplex stream that modifies or transforms data as it passes through.

Streams inherit from the EventEmitter class, enabling them to emit events during data processing. The pipe() method is commonly used to efficiently move data from a readable stream to a writable stream. Streams are essential for managing I/O operations, handling large files, and building scalable applications in Node.js.
```javascript
const fs = require('fs');

// Create a readable stream from a file
const readableStream = fs.createReadStream('input.txt');

// Create a writable stream to a file
const writableStream = fs.createWriteStream('output.txt');

// Pipe data from the readable stream to the writable stream
readableStream.pipe(writableStream);

// Handle events
readableStream.on('data', (chunk) => {
  console.log('Received chunk:', chunk);
});

readableStream.on('end', () => {
  console.log('Finished reading');
});

readableStream.on('error', (err) => {
  console.error('Error:', err);
});

writableStream.on('finish', () => {
    console.log('Finished writing');
});
```
---
### Q. How Authentication works in Node.js. 
Authentication verifies a user's identity, while JWT (JSON Web Token) is a standard for securely transmitting information between parties as a JSON object. In Node.js, these concepts work together to manage user sessions and secure APIs. 

- **User Login:** When a user attempts to log in, the server verifies their credentials (e.g., username and password) against a database.
- **Token Generation:** If the credentials are valid, the server generates a JWT. This token contains user information (payload), is signed using a secret key, and has an expiration time.
- **Token Transmission:** The server sends the JWT back to the client (e.g., in the response body or as a cookie).
- **Protected Route Access:** When the client needs to access a protected route or resource, it includes the JWT in the request headers (typically in the `Authorization` header as a `Bearer token`).
- **Token Verification:** The server receives the request, extracts the JWT, and verifies its signature using the same secret key used to sign it.
- **Authorization:** If the token is valid and not expired, the server decodes the payload to extract user information and grants access to the requested resource. If the token is invalid or expired, the server denies access and returns an error.
- **Logout:** To log out, the client simply discards the JWT. The server does not need to do anything, as the token is stateless and self-contained. 

// Example using express and jsonwebtoken library
```javascript
const express = require('express');
const jwt = require('jsonwebtoken');
const app = express();

app.post('/login', (req, res) => {
  // Authenticate user (e.g., check credentials against database)
  const user = { id: 1, username: 'testuser' };
  const secretKey = 'your-secret-key';
  const token = jwt.sign(user, secretKey, { expiresIn: '1h' });
  res.json({ token });
});

app.get('/protected', verifyToken, (req, res) => {
  res.json({ message: 'Protected resource accessed', user: req.user });
});

function verifyToken(req, res, next) {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1];
  if (!token) return res.sendStatus(401);

  const secretKey = 'your-secret-key';
  jwt.verify(token, secretKey, (err, user) => {
    if (err) return res.sendStatus(403);
    req.user = user;
    next();
  });
}
```
## Q. How memory management works in Node.js?
Node.js uses the V8 JavaScript engine, which handles memory management automatically through garbage collection. The memory is divided into the heap (for objects) and the stack (for function calls). The garbage collector reclaims memory occupied by objects that are no longer reachable. 

Understanding memory management in Node.js involves being aware of how memory is allocated and released. While V8 handles much of this automatically, developers should avoid practices that lead to memory leaks. 

Node.js provides tools for monitoring memory usage, such as `process.memoryUsage()`, which returns information about memory consumption. Developers can also use the `--max-old-space-size` flag to adjust the maximum memory allocated for the heap.

#### Best Practices for Memory Management

**Avoid global variables:** 
- Excessive use of global variables can prevent memory from being reclaimed. 
**Handle closures carefully:** 
- Closures can unintentionally keep references to variables, leading to memory leaks. 
**Use streams for large data:** 
- When processing large files or data sets, streams can help manage memory usage efficiently. 
**Monitor memory usage:** 
- Tools like `process.memoryUsage()` and heap profilers can help identify memory leaks. 
**Set memory limits:** 
- Use the `--max-old-space-size` flag to limit the amount of memory Node.js can use. 
**Use the Buffer class:** 
- When dealing with binary data, using the `Buffer` class ensures efficient memory handling. 
**Garbage collection:** 
- Node.js employs a two-generation garbage collection system: 
  - **Minor GC (Scavenger):** Collects short-lived objects in the "new space." 
	- **Major GC (Mark-Sweep & Mark-Compact):** Collects long-lived objects in the "old space." 

By understanding these concepts and following best practices, developers can write more efficient and reliable Node.js applications. 

---
## Q. Find the output:
```javascript
let output = (function(x) {
    delete x;
    return x;
})(0);
```
**Output:**
```
0
```

---
## Q. Piping in Node.js

In **Node.js**, **piping** is a powerful mechanism used to **connect the output of one stream to the input of another**, enabling efficient data handling without having to manually manage reading and writing.

It is most commonly used with **streams** (such as file streams, HTTP streams, or custom streams) to **transfer data efficiently and asynchronously**.

### **What Is Piping?**

Piping allows you to **chain streams** together, so the data flows from one stream to another. It's especially useful for large files or continuous data streams where buffering everything into memory is not efficient.

### **Basic Syntax:**

```javascript
readableStream.pipe(writableStream);
```

### **Example: Copying a File**

```javascript
const fs = require('fs');

const readable = fs.createReadStream('input.txt');
const writable = fs.createWriteStream('output.txt');

readable.pipe(writable);
```

This code reads data from `input.txt` and writes it directly to `output.txt` using a pipe. This method is **non-blocking and memory-efficient**.

### **Chaining Pipes with Multiple Streams (Compression Example)**

```javascript
const fs = require('fs');
const zlib = require('zlib');

const readable = fs.createReadStream('input.txt');
const compressed = zlib.createGzip();
const writable = fs.createWriteStream('input.txt.gz');

readable.pipe(compressed).pipe(writable);
```

This example reads a file, compresses it using `zlib.createGzip()`, and writes the compressed content to a new file.

### **Why Use Pipe?**

- Handles backpressure automatically (slows down reading if the writable stream can't keep up).
- Improves performance with large files.
- Simplifies code for streaming operations.

### **Key Methods and Events:**

- `.pipe(destination[, options])`: Pipes readable stream to a writable.
- `.unpipe()`: Detaches a pipe.
- `on('data')`, `on('end')`, `on('error')`: Common stream events.

### **Conclusion:**

Piping in Node.js is a clean and efficient way to **stream data between sources and destinations**, especially useful in file manipulation, real-time processing, and network data transfer. It helps build fast, low-memory, scalable applications in Node.js.

---
## Q. Splice in JavaScript
The `splice()` method in JavaScript modifies an array by removing, replacing, or adding elements. It changes the original array and returns an array containing the removed elements.

**Syntax** 
```javascript
array.splice(start, deleteCount, item1, item2, ...);
```
- `start`: The index to start changing the array. 
- `deleteCount`: The number of elements to remove. If 0, no elements are removed. 
- `item1, item2, ...`: Optional. The elements to add to the array, starting at the start index. 

**Examples** 

```javascript
const months = ["Jan", "Feb", "Mar", "Apr"];

// Remove 1 element starting at index 2
const removed = months.splice(2, 1);
// months: ["Jan", "Feb", "Apr"]
// removed: ["Mar"]

// Add elements without removing any
months.splice(2, 0, "Mar", "Apr");
// months: ["Jan", "Feb", "Mar", "Apr", "Apr"]

// Replace 1 element at index 1 with two new elements
months.splice(1, 1, "New Feb 1", "New Feb 2");
// months: ["Jan", "New Feb 1", "New Feb 2", "Mar", "Apr", "Apr"]

// Remove elements from the end using a negative start index
months.splice(-2, 2)
// months: ["Jan", "New Feb 1", "New Feb 2", "Mar"]
```

**Return Value** 

`splice()` returns an array containing the deleted elements. If no elements are removed, it returns an empty array.

**Mutating the Array**

It's important to note that `splice()` modifies the original array directly. If you need to keep the original array unchanged, consider using `toSpliced()` (ES2023) or creating a copy of the array before using `splice()`. For shallow copies, methods like `slice()`, `Array.from()`, or `Object.assign()` can be used. 

---
## Q. 
Currying is a functional programming technique where a function that takes multiple arguments is transformed into a series of functions, each taking a single argument. This allows for partial application of arguments, creating new functions with some parameters already set. Currying is named after mathematician Haskell Curry. 
Here's a more detailed explanation:  

### How Currying Works:  

#### - Original Function: 
A function that typically takes multiple arguments (e.g., `add(x, y)`).  

#### - Curried Function: 
The same function rewritten to take one argument at a time. The first function returns a new function that takes the next argument, and so on.
  - For example, `add(x)(y)` would be a curried version of `add(x, y)`.  

#### - Partial Application: 
Currying enables partial application. You can call the curried function with only some of the arguments, creating a new function that will use those provided arguments when the remaining arguments are supplied later.

### Benefits of Currying:  

#### - Code Reusability: 
Currying allows you to create specialized versions of a function by providing some of its arguments upfront, making the code more reusable.  

#### - Higher-Order Functions: 
Currying is often used to create higher-order functions, which are functions that take other functions as arguments or return functions.

#### - Modularity: 
Currying can help break down complex functions into smaller, more manageable functions, promoting modularity. 

#### - Function Composition: 
Currying facilitates function composition, where you can combine simpler functions to build more complex ones.

Example (JavaScript): 
```javascript
// Normal function
function add(x, y) {
  return x + y;
}

// Curried function
function curryAdd(x) {
  return function(y) {
    return x + y;
  };
}

// Using curried function with partial application
const addFive = curryAdd(5);
console.log(addFive(2)); // Output: 7 (5 + 2)
console.log(addFive(10)); // Output: 15 (5 + 10)
```

---
## Q. The temporal dead zone (TDZ)
The temporal dead zone (TDZ) is a behavior in JavaScript that occurs when declaring variables using `let` and `const`. It refers to the period between entering the scope and the actual declaration of the variable. During this period, the variable cannot be accessed and will throw a ReferenceError if you try to use it.  
The TDZ exists to help catch errors and ensure more predictable behavior, especially with const declarations. It enforces that variables should be declared before they are used, promoting cleaner and more maintainable code. 
```javascript
{
  // TDZ starts for variable 'a'
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
  let a = 10; // TDZ ends for variable 'a'
  console.log(a); // Output: 10
}
```

---
## Q. ES6 Features
ES6 (ECMAScript 2015) introduced significant features to JavaScript, enhancing its capabilities and syntax. Some key features with examples are: 

- `let` and `const` Declarations: Block-scoped variable declarations, offering more control over variable scope compared to var. 
```javascript
let x = 10;
const PI = 3.14;

if (true) {
  let x = 20;
  const PI = 3.14159;
  console.log(x); // Output: 20
  console.log(PI); // Output: 3.14159
}

console.log(x); // Output: 10
console.log(PI); // Output: 3.14
```
- Arrow Functions: Concise syntax for function expressions, and they do not bind their own this value. 
```javascript
const add = (a, b) => a + b;
console.log(add(5, 3)); // Output: 8
```
- Template Literals: String interpolation and multi-line strings using backticks. 
```javascript
    const name = "John";
const message = `Hello, ${name}!
This is a multi-line string.`;
console.log(message);
// Output:
// Hello, John!
// This is a multi-line string.
```
- Destructuring: Extract values from arrays or objects into distinct variables. 
```javascript
const arr = [1, 2, 3];
const [a, b, c] = arr;
console.log(a, b, c); // Output: 1 2 3

const obj = { name: "Alice", age: 30 };
const { name, age } = obj;
console.log(name, age); // Output: Alice 30
```
- Default Parameters: Set default values for function parameters. 
```javascript
function greet(name = "Guest") {
  console.log(`Hello, ${name}!`);
}

greet(); // Output: Hello, Guest!
greet("Bob"); // Output: Hello, Bob!
```
- Rest and Spread Operators: 
	- Rest: Collect multiple function arguments into an array. 
	- Spread: Expand an iterable (like an array or object) into individual elements. 
    ```javascript
    function sum(...numbers) {
      return numbers.reduce((acc, num) => acc + num, 0);
    }
    
    console.log(sum(1, 2, 3, 4)); // Output: 10
    
    const arr1 = [1, 2, 3];
    const arr2 = [...arr1, 4, 5];
    console.log(arr2); // Output: [1, 2, 3, 4, 5]
    ```
- Enhanced Object Literals: Shorthand syntax for object properties and methods. 
    ```javascript
    const x = 10, y = 20;
    const obj = { x, y,
       add() {
        return this.x + this.y;
      }
    };
    console.log(obj.add()); // Output: 30
    ```
- Classes: Syntactic sugar for constructor functions, providing a more structured way to create objects. 
    ```javascript
    class Person {
      constructor(name) {
        this.name = name;
      }
    
      greet() {
        console.log(`Hello, my name is ${this.name}.`);
      }
    }
    
    const person = new Person("Charlie");
    person.greet(); // Output: Hello, my name is Charlie.
    ```
- Modules: Organize code into separate files for better maintainability, using import and export. 
    ```javascript
    // math.js
    export function add(a, b) {
      return a + b;
    }
    
    // app.js
    import { add } from './math.js';
    console.log(add(2, 3)); // Output: 5
    ```
- Promises: Handle asynchronous operations more cleanly, replacing callbacks. 
    ```javascript
    function fetchData() {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve("Data fetched successfully!");
        }, 1000);
      });
    }
    
    fetchData().then(data => console.log(data)); // Output: Data fetched successfully! (after 1 second)
    ```
- Symbols: Create unique and immutable values, often used as object property keys to avoid naming conflicts. 
    ```javascript
    const mySymbol = Symbol('description');
    const obj = {
      [mySymbol]: 'This is a symbol property'
    };
    console.log(obj[mySymbol]); // Output: This is a symbol property
    ```
- Iterators and for...of Loop: Iterate over iterable objects like arrays, maps, sets, and strings. 

  ```javascript
  const arr = [10, 20, 30];
  for (const value of arr) {
    console.log(value);
  }
  // Output:
  // 10
  // 20
  // 30
  ```

- Maps and Sets: New data structures for storing collections of data. 

  // Map
  ```javascript
  const myMap = new Map();
  myMap.set('name', 'David');
  myMap.set('age', 25);
  console.log(myMap.get('name')); // Output: David
  
  // Set
  const mySet = new Set();
  mySet.add(1);
  mySet.add(2);
  mySet.add(2); // Duplicates are ignored
  console.log(mySet.has(2)); // Output: true
  ```

---
## Q. Create your own deepcopy implementation function in javascript
### Deep Copy Function (Approach 1)
Here's the implementation of a deepCopy function in JavaScript: 
```javascript
function deepCopy(obj) {
  if (typeof obj !== "object" || obj === null) {
    return obj;
  }

  let copy = Array.isArray(obj) ? [] : {};

  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      copy[key] = deepCopy(obj[key]);
    }
  }
  return copy;
}
```
This function recursively copies all properties of an object, including nested objects and arrays, ensuring that the copied object is completely independent of the original. It handles primitive types, arrays, and objects, providing a robust solution for deep copying in JavaScript. 

Creating a deep copy function in JavaScript involves recursively copying all properties of an object or elements of an array, ensuring that nested objects and arrays are also duplicated rather than referenced. Here’s a simple implementation of a deep copy function:

### Deep Copy Function (Approach 2)

```javascript
function deepCopy(obj) {
    // Check for null or non-object types (including functions)
    if (obj === null || typeof obj !== 'object') {
        return obj; // Return the value if obj is not an object
    }

    // Handle arrays
    if (Array.isArray(obj)) {
        const arrCopy = []; // Create a new array
        for (let i = 0; i < obj.length; i++) {
            arrCopy[i] = deepCopy(obj[i]); // Recursively copy each element
        }
        return arrCopy; // Return the new array
    }

    // Handle objects
    const objCopy = {}; // Create a new object
    for (const key in obj) {
        if (obj.hasOwnProperty(key)) { // Check if the property is the object's own
            objCopy[key] = deepCopy(obj[key]); // Recursively copy each property
        }
    }
    return objCopy; // Return the new object
}
```

### Explanation of the Code:

1. **Base Case**: The function first checks if the input `obj` is `null` or not an object (like a number, string, or boolean). If so, it simply returns the value, as primitive types do not need to be copied.

2. **Array Handling**: If the input is an array, it creates a new array and recursively copies each element from the original array into the new one.

3. **Object Handling**: If the input is an object, it creates a new object and iterates over each property. For each property, it checks if it belongs to the object (using `hasOwnProperty`) and recursively copies the value.

4. **Return**: Finally, it returns the newly created object or array.

### Example Usage:

```javascript
const original = {
    name: "Alice",
    age: 30,
    hobbies: ["reading", "traveling"],
    address: {
        city: "Wonderland",
        zip: 12345
    }
};

const copy = deepCopy(original);

// Modifying the copy
copy.name = "Bob";
copy.hobbies.push("gaming");
copy.address.city = "New Wonderland";

console.log(original); // Original remains unchanged
console.log(copy);     // Copy reflects the changes
```

### Important Considerations:

- **Circular References**: This implementation does not handle circular references. If you need to handle objects that reference themselves, you would need to keep track of already copied objects using a Map or WeakMap.

- **Functions and Special Objects**: This implementation does not copy functions, Dates, RegExps, or other special objects. You may need to extend the function to handle these cases if necessary.

### Conclusion:

This `deepCopy` function provides a straightforward way to create deep copies of objects and arrays in JavaScript. You can enhance it further based on your specific needs, such as handling special cases or optimizing performance.

---
## Q. 

---
## Q. 

---
## Q. 

---

## TODO 
Currying
-------------------------------------------- End Javascript & Node.js --------------------------------------------

---
---



## Angular Interview Questions

### Q. Angular 17 Features with Examples
Angular 17 brought a fresh syntax, performance improvements, and better dev ergonomics. Here's a section-wise guide with examples to explore the new capabilities.
#### 1. Built-in Control Flow (`@if`, `@for`, `@switch`)
Angular now supports native control flow syntax directly in templates, replacing structural directives like `*ngIf`, `*ngFor`.
##### Example: `@if` and `@else`
```
<!-- user.component.html -->
@if (user?.isLoggedIn) {
  <p>Welcome, {{ user.name }}!</p>
} @else {
  <p>Please log in.</p>
}
```
##### Example: `@for`
```html
<!-- items.component.html -->
<ul>
  @for (item of items; track item.id) {
    <li>{{ item.name }}</li>
  }
</ul>
```
#### Example: `@switch`
```html
<!-- status.component.html -->
@switch (status) {
  @case ('loading') {
    <p>Loading...</p>
  }
  @case ('error') {
    <p>Error occurred.</p>
  }
  @default {
    <p>Data loaded!</p>
  }
}
```
#### 🧱 2. Deferrable Views (`@defer`)
Deferrable views let you lazy-load parts of the UI based on triggers.
##### Example: Lazy load on idle
```html
<!-- dashboard.component.html -->
@defer (on idle) {
  <analytics-chart></analytics-chart>
}
```
Other triggers:  
- `on timer(3000)`
- `on interaction`
- `on condition(isLoaded)`
#### ⚡ 3. View Transitions API
Enable animated route/page transitions with the [View Transitions API](https://developer.mozilla.org/en-US/docs/Web/API/View_Transitions_API).
##### Example: `app.component.ts`
```ts
// app.component.ts
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-root',
  standalone: true,
  templateUrl: './app.component.html',
})
export class AppComponent {
  constructor(private router: Router) {}

  navigate(path: string) {
    document.startViewTransition(() => {
      this.router.navigate([path]);
    });
  }
}
```
```html
<!-- app.component.html -->
<button (click)="navigate('/about')">Go to About</button>
```
##### 4. Standalone Components
No more need for `NgModule`. Use `standalone: true` and import directly.
##### Example: `hello.component.ts`
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello',
  standalone: true,
  template: `<h2>Hello Angular 17!</h2>`
})
export class HelloComponent {}
```
Use in routing:
```ts
// app.routes.ts
import { Routes } from '@angular/router';
import { HelloComponent } from './hello.component';

export const routes: Routes = [
  { path: 'hello', component: HelloComponent }
];
```
#### 5. SSR & Hydration Enhancements
Angular 17 improves hydration time with better server-to-client DOM reconciliation.
```bash
ng add @angular/ssr
```
Hydration is now enabled by default when SSR is configured.
#### 6. Strictly Typed Reactive Forms
Now forms are fully type-safe.
##### Example:
```ts
const loginForm = new FormGroup({
  email: new FormControl<string>('', { nonNullable: true }),
  password: new FormControl<string>('', { nonNullable: true }),
});
```
> TypeScript will now help catch mistakes like assigning numbers to strings.
#### ⚡ 7. Vite + Esbuild (Experimental)
Angular now supports Vite + Esbuild for fast development builds.
```bash
ng build --configuration=esbuild
```
Enable via experimental builder in `angular.json`.
#### 📘 Summary Table
| Feature              | Description                                  | Syntax/Usage                 |
|----------------------|----------------------------------------------|------------------------------|
| `@if`, `@for`, `@switch` | Modern control flow in templates         | `@if`, `@for`, `@switch`     |
| `@defer`             | Lazy load components/views                   | `@defer (on idle) {}`        |
| View Transitions API | Native animated routing                      | `document.startViewTransition()` |
| Standalone Components| Decluttered structure, no `NgModule` needed  | `standalone: true`           |
| SSR & Hydration      | Faster rendering and reactivity              | `ng add @angular/ssr`        |
| Typed Forms          | Type-safe reactive forms                     | `FormControl<string>`        |
| Vite/Esbuild         | Fast experimental build system               | `--configuration=esbuild`    |

---
### Q. Exception handling in Angular  
Angular applications can handle exceptions using several approaches: 
**Try...Catch Blocks** 
As in standard JavaScript, try...catch blocks manage errors within specific code sections, particularly for synchronous operations. 
```javascript
try {
  // Code that may throw an error
  const result = synchronousFunction();
  console.log('Result:', result);
} catch (error) {
  // Handle the error
  console.error('An error occurred:', error);
}
```
**ErrorHandler** 
Angular's ErrorHandler provides centralized error handling across the application. By extending this class, developers can customize how errors are managed globally. 
```javascript
import { ErrorHandler, Injectable } from '@angular/core';

@Injectable()
export class GlobalErrorHandler implements ErrorHandler {
  handleError(error: any) {
    // Custom error handling logic
    console.error('Global error handler:', error);
    // Send error to server, display user-friendly message, etc.
  }
}
```
// In module or application configuration:
providers: [{ provide: ErrorHandler, useClass: GlobalErrorHandler }]
**RxJS catchError Operator** 
```javascript
For asynchronous operations with observables, catchError from RxJS intercepts and handles errors gracefully. 
import { of } from 'rxjs';
import { catchError, tap } from 'rxjs/operators';

this.http.get('/api/data').pipe(
  tap(data => console.log('Data received:', data)),
  catchError(error => {
    console.error('HTTP error:', error);
    // Handle error (e.g., log, return default value, rethrow)
    return of([]); // Return a new observable to continue the stream
  })
).subscribe(data => {
  // Process data or handle completion
});
```
**HttpInterceptor** 
```javascript
HttpInterceptor provides a robust way to handle errors related to the server and network by intercepting HTTP requests and responses. 
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent, HttpErrorResponse } from '@angular/common/http';
import { Observable, throwError } from 'rxjs';
import { catchError } from 'rxjs/operators';

@Injectable()
export class HttpErrorInterceptor implements HttpInterceptor {
  intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    return next.handle(request)
      .pipe(
        catchError((error: HttpErrorResponse) => {
          // Handle error
          console.error('HTTP error intercepted:', error);
          return throwError(() => error); // Re-throw the error
        })
      );
  }
}
```
//In module or application configuration:
providers: [{ provide: HTTP_INTERCEPTORS, useClass: HttpErrorInterceptor, multi: true }]
You can define multiple interceptors, and they will be called in the order they are provided. 

---
### Q. Signal in Angular  
Signals in Angular are a reactivity primitive that notifies interested consumers when a wrapped value changes. They optimize change detection by tracking where values are used, ensuring updates only occur when necessary. 

Key Concepts 
- _Signal_: A wrapper around a value that notifies consumers upon changes.
- _Computed Signal_: A read-only signal whose value is derived from other signals.
- _Effect_: A side effect that runs when signal values it depends on change.
**Basic Usage** 
```javascript
Creating a Signal:
import { signal } from '@angular/core';
const count = signal(0);
```
```javascript
Reading a Signal: 
const currentCount = count(); // Access the value
```
```javascript
Updating a Signal:
count.set(1); // Sets the value to 1
count.update(value => value + 1); // Increments the value
count.mutate(value => value.push(newValue)); // Mutates the value
```
```javascript
Computed Signals: 
import { computed, signal } from '@angular/core';
const firstName = signal('John');
const lastName = signal('Doe');
const fullName = computed(() => `${firstName()} ${lastName()}`);
  
console.log(fullName()); // Output: John Doe
```
```javascript
effects:
import { effect, signal } from '@angular/core';
   
const counter = signal(0);
 
effect(() => {
     console.log('Counter value changed:', counter());
});
counter.set(1); // Triggers the effect and logs "Counter value changed: 1"
```
**Benefits:**
- _Improved Performance:_ Granular change detection reduces unnecessary updates.
- _Simpler Syntax_: More straightforward than Observables for simple state management.
- _Predictable Updates_: Ensures glitch-free and consistent data flow. 

---
### Q. Zone.js  
`zone.js` is a crucial library for Angular applications, managing and tracking asynchronous operations. It essentially creates execution contexts, or "zones," that monitor tasks like event handling, timers, promises, and HTTP requests. This allows Angular to automatically detect changes and update the UI accordingly, ensuring efficient change detection. 
`zone.js` intercepts and wraps asynchronous tasks, enabling Angular to run code before and after these tasks. This mechanism is vital for triggering Angular's change detection cycle whenever an asynchronous operation completes, ensuring the UI remains synchronized with the application state. While change detection is not part of zone.js itself, Angular utilizes `zone.js` to initiate it automatically. 
Angular offers the `NgZone` service, which allows developers to run code outside the context of zone.js when necessary, such as for performance optimization. This can be useful when dealing with tasks that don't require UI updates. 
It's worth noting that Angular is moving towards a zoneless architecture, with `zone.js` no longer accepting new features. This shift aims to provide more fine-grained control over change detection and potentially improve performance. 

---
## Q. SwitchMap
`switchMap` is an **RxJS operator** used in Angular to map an observable to another observable while **canceling previous subscriptions** if a new value comes in.  
### **How it Works?**  
- Ideal for handling **API calls, user inputs, and search functionalities** where only the latest request matters.
- Prevents **unnecessary network requests** and **race conditions**.  
### **Example Usage in Angular HTTP Calls**  
```typescript
this.searchInput.valueChanges.pipe(
  debounceTime(300), // Wait before firing request
  switchMap(query => this.apiService.search(query)) // Cancels previous request
).subscribe(results => console.log(results));
```
### **Key Differences (vs `mergeMap`)**  
- **`switchMap`** → Cancels previous requests, keeps only the latest one.  
- **`mergeMap`** → Runs all requests concurrently without canceling.  
### **Best Use Cases**  
- **Live search** (cancel previous search request).  
- **Authentication (Login)** (only last request matters).  
- **Auto-refresh API calls** (avoid outdated responses).

---
## Q. What is component in angular?
A component in Angular is a fundamental building block for creating user interfaces. It encapsulates a portion of the user interface's logic and presentation. Each component consists of three main parts:
- _Template_: Defines the HTML structure and layout of the component's view.
- _Class_: Contains the logic, data, and methods that control the component's behavior.
- _Metadata_: Provides information about the component, such as its selector, template, and styles.
Components are designed to be reusable and modular, promoting a structured and maintainable application architecture. They facilitate the separation of concerns, making it easier to develop, test, and update different parts of the application independently.

---
## Q. What is template driven form vs reactive driven form.
Angular provides two ways to build forms: **Template-Driven Forms** and **Reactive Forms**.  
| Feature | Template-Driven Forms | Reactive Forms |
|---------|----------------------|---------------|
| **Approach** | Uses **directives** in the template (HTML-driven) | Uses **form controls** in the TypeScript code (code-driven) |
| **Form Creation** | Uses `FormsModule` | Uses `ReactiveFormsModule` |
| **Binding** | **Two-way data binding** with `ngModel` | **Explicit form control binding** using `FormControl` and `FormGroup` |
| **Validation** | Uses **HTML-based validators** (`required`, `minlength`, etc.) | Uses **programmatic validators** (`Validators.required`, `Validators.minLength()`, etc.) |
| **Scalability** | Best for **simple forms** | Better for **complex, dynamic forms** |
| **Flexibility** | Less flexible, tightly coupled to the template | More flexible, easier to manage dynamically |
| **Testing** | Harder to unit test | Easier to unit test |

### **When to Use What?**  
- **Template-Driven Forms** – Best for simple forms with minimal logic.  
- **Reactive Forms** – Ideal for complex forms, dynamic validations, and better testability.  
**Example:**  
**Template-Driven Form:**  
  ```html
  <form #userForm="ngForm">
    <input type="text" name="username" ngModel required />
  </form>
  ```
**Reactive Form:**  
  ```typescript
  userForm = new FormGroup({
    username: new FormControl('', Validators.required)
  });
  ```
**Note:** Reactive Forms are recommended for most real-world applications due to better flexibility and maintainability.

---
## Q. What is SPA?
A **Single Page Application (SPA)** loads a single HTML page and dynamically updates content **without full page reloads**. It improves performance and user experience by using **JavaScript frameworks (Angular, React, Vue)** to handle UI updates and fetch data via APIs.  

### **Key Features:**  
- Faster navigation, no flickering.  
- Uses **AJAX/REST API/GraphQL** for data fetching.  
- Examples: **Gmail, Facebook, Google Maps**.  

**Efficient but needs SEO optimization & initial load handling.**

---
## Q. How Angular works?
Angular is a **component-based** frontend framework that uses **TypeScript**. It follows the **MVC** pattern and works by:  
1. **Bootstrapping** – Loads the root module (`AppModule`) and component (`AppComponent`).  
2. **Templates & Data Binding** – Uses **HTML templates** and **binding** (`{{ }}`) to display dynamic data.  
3. **Directives & Components** – Components control the UI, while directives add behavior.  
4. **Dependency Injection** – Services are injected into components for reusability.  
5. **Routing** – `RouterModule` enables navigation between pages.  
6. **Change Detection** – Updates the DOM when data changes, using **Zone.js**.  
7. **RxJS & Observables** – Handles async data streams efficiently.
8. **Compilation & Optimization**
    1. Ahead-of-Time (AOT) Compilation improves performance.
    2. Lazy Loading loads modules only when needed, optimizing performance.
  
---
## Q. Interceptors in Angular 
Interceptors in Angular are services that allow you to intercept and modify HTTP requests and responses. They are useful for tasks such as adding _headers_, _handling authentication_, _logging_, or _caching_. Interceptors work by sitting between your application and the backend server, intercepting requests before they are sent and responses before they are received. They can modify these requests and responses, or handle them directly.
To create an interceptor, you need to create a class that **implements the HttpInterceptor interface** and define the `intercept` method. This method takes two arguments: the `HttpRequest` object and the `HttpHandler` object. The `HttpRequest` object represents the outgoing request, and the `HttpHandler` object represents the next interceptor in the chain, or the backend server if there are no more interceptors.
```javascript
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable()
export class MyInterceptor implements HttpInterceptor {
  intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    // Modify the request
    const modifiedRequest = request.clone({
      setHeaders: {
        'Authorization': 'Bearer my-token'
      }
    });

    // Handle the request
    return next.handle(modifiedRequest);
  }
}
```
To use an interceptor, you need to provide it in your application module or component. 
```javascript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
import { MyInterceptor } from './my.interceptor';

@NgModule({
  imports: [
    BrowserModule,
    HttpClientModule
  ],
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: MyInterceptor, multi: true }
  ]
})
export class AppModule { }
```
You can define multiple interceptors, and they will be called in the order they are provided. 

---
## Q.  nth Highest salary in MongoDB
#### Approach 1: 
	SELECT DISTINCT salary 
	FROM employees 
	ORDER BY salary DESC 
	LIMIT 1 OFFSET N-1;

#### In MongoDB:
```javascript
db.employees.aggregate([
  { $group: { _id: "$salary" } },   // Group by salary
  { $sort: { _id: -1 } },           // Sort salaries in descending order
  { $limit: N },                    // Limit to top N salaries
  { $skip: N-1 }                    // Skip (N-1) results to get the Nth
])
```

---
## Q. Service injection in Angular
Service injection in Angular can be achieved through constructor injection or by using the `@Inject` decorator or the `inject()` function. Here's a breakdown of the differences:

**1. Constructor Injection**
This is the most common and traditional way to inject dependencies.
_Mechanism:_ Dependencies are declared as parameters in the class constructor. Angular's dependency injection system automatically resolves and provides these dependencies when the class is instantiated.
```javascript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class MyService {
  getValue(): string {
    return 'Hello from MyService';
  }
}

import { Component } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: `{{ message }}`,
})
export class MyComponent {
  message: string;

  constructor(private myService: MyService) {
    this.message = this.myService.getValue();
  }
}
```
_Advantages:_
- Clear and explicit dependency declaration, improving code readability.
- Easier to test, as dependencies can be easily mocked or stubbed during unit testing.
- Promotes immutability, as dependencies are typically assigned to readonly properties.
_Disadvantages:_
- Can become verbose with many dependencies.
- May lead to circular dependency issues in complex scenarios.
- Inheritance can become cumbersome as derived classes need to call the base class constructor with all dependencies.

**2. @Inject Decorator**
The `@Inject` decorator is used to specify the dependency token when the type of the dependency is not readily available or when using custom tokens.
_Mechanism_: It is placed before a constructor parameter to explicitly define the token associated with the dependency.
```javascript
import { Inject, Injectable } from '@angular/core';
    @Injectable({
      providedIn: 'root'
    })
export class MyService {
      getValue(): string {
        return 'Hello from MyService';
      }
}

import { Component } from '@angular/core';

const MY_TOKEN = 'myToken';

@Component({
      selector: 'app-my-component',
      template: `{{ message }}`,
      providers: [{ provide: MY_TOKEN, useValue: 'Injected Value' }]
})
export class MyComponent {
      message: string;

      constructor(@Inject(MY_TOKEN) public injectedValue: string, private myService: MyService) {
        this.message = this.myService.getValue() + ' ' + this.injectedValue;
      }
}
```
_Advantages:_
- Allows injecting dependencies using tokens, useful for non-class dependencies or abstract types.
_Disadvantages:_
- Less common in typical scenarios where the dependency type is a class.
- Can make code less readable compared to constructor injection with type inference.

**3. inject() Function**
The inject() function provides a functional way to inject dependencies, especially useful in newer Angular versions and in situations outside of constructors.
_Mechanism:_ It retrieves a dependency directly from the injector using the provided token.
```javascript
import { Component, inject, Injectable } from '@angular/core';

@Injectable({
      providedIn: 'root'
    })
    export class MyService {
      getValue(): string {
        return 'Hello from MyService';
      }
    }

@Component({
      selector: 'app-my-component',
      template: `{{ message }}`,
})
export class MyComponent {
      private myService = inject(MyService);
      message: string = this.myService.getValue();
}
```
_Advantages:_ 
- More readable, especially with many dependencies, as it keeps the constructor clean.
- Enables injecting dependencies in functions, computed properties, and other contexts outside the constructor.
- Simplifies inheritance scenarios, as derived classes don't need to pass dependencies to the base class constructor.
_Disadvantages:_
- Can be less explicit about dependencies compared to constructor injection.
- Might be less familiar to developers accustomed to constructor injection.

---
## Q. Transferring Data Between Angular Components
Angular offers several ways to transfer data between components, each suited for different scenarios. Here's a breakdown of the most common methods:

**1. Parent to Child:** Using `@Input()` 
- The parent component passes data to a child component using the `@Input()` decorator.
**Parent Component:**
```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'parent',
    template: `
      <child [message]="parentMessage"></child>
    `,
})
export class ParentComponent {
    parentMessage = 'Hello from parent!';
}
```
**Child Component:**
```javascript
import { Component, Input } from '@angular/core';
@Component({
    selector: 'child',
    template: `<p>{{ message }}</p>`,
})
export class ChildComponent {
    @Input() message: string;
}
```

**2. Child to Parent:** Using `@Output()` and `EventEmitter`
- The child component sends data to the parent component using the `@Output()` decorator and `EventEmitter`.

**Parent Component:**
```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'parent',
    template: `
      <child (messageEvent)="handleMessage($event)"></child>
      <p>Received from child: {{ childMessage }}</p>
    `,
})
export class ParentComponent {
    childMessage = '';

    handleMessage(message: string) {
        this.childMessage = message;
    }
}
```
**Child Component:**
```javascript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
    selector: 'child',
    template: `<button (click)="sendMessage()">Send Message</button>`,
})
export class ChildComponent {
    @Output() messageEvent = new EventEmitter<string>();

    sendMessage() {
        this.messageEvent.emit('Hello from child!');
    }
}
```

**3. Using a Service**
- A service can be used to share data between any components, regardless of their relationship. This is useful for sharing data between sibling components or deeply nested components.

**Data Service:**
```
import { Injectable } from '@angular/core';
import { BehaviorSubject } from 'rxjs';

@Injectable({ providedIn: 'root' })
export class DataService {
    private messageSource = new BehaviorSubject<string>('Default message');
    currentMessage = this.messageSource.asObservable();

    changeMessage(message: string) {
        this.messageSource.next(message);
    }
}
```
**Component 1:**
```
import { Component, OnInit } from '@angular/core';
import { DataService } from '../data.service';

@Component({
    selector: 'component1',
    template: `
      <p>Message: {{ message }}</p>
      <button (click)="changeMessage()">Change Message</button>
    `,
})
export class Component1 implements OnInit {
    message: string;

    constructor(private dataService: DataService) {}

    ngOnInit() {
        this.dataService.currentMessage.subscribe(
            (message) => (this.message = message)
        );
    }

    changeMessage() {
        this.dataService.changeMessage('Message from Component 1');
    }
}
```
**Component 2:**
```
import { Component, OnInit } from '@angular/core';
import { DataService } from '../data.service';

@Component({
    selector: 'component2',
    template: `<p>Message: {{ message }}</p>`,
})
export class Component2 implements OnInit {
    message: string;

    constructor(private dataService: DataService) {}

    ngOnInit() {
        this.dataService.currentMessage.subscribe(
            (message) => (this.message = message)
        );
    }
}

```
**4. Using Subject or BehaviorSubject**
- For more complex scenarios, you can use `Subject` or `BehaviorSubject` from RxJS to share data between components.  A `BehaviorSubject` holds the current value, while a `Subject` does not.

**Component 1:**
```
import { Component } from '@angular/core';

import { DataService } from '../data.service';

@Component({
  selector: 'component1',
  template: `
    <button (click)="sendMessage()">Send Message</button>
  `,
})
export class Component1 {
  constructor(private dataService: DataService) {}

  sendMessage() {
    this.dataService.messageSource.next('Hello from Component 1');
  }
}
```
**Component 2:**
```
import { Component, OnInit, OnDestroy } from '@angular/core';
import { DataService } from '../data.service';
import { Subscription } from 'rxjs';

@Component({
  selector: 'component2',
  template: `
    <p>Message: {{ message }}</p>
  `,
})
export class Component2 implements OnInit, OnDestroy {
  message: string;
  subscription: Subscription;

  constructor(private dataService: DataService) {}

  ngOnInit() {
    this.subscription = this.dataService.messageSource.subscribe(message => {
      this.message = message;
    });
  }

  ngOnDestroy() {
    this.subscription.unsubscribe();  //prevent memory leak
  }
}
```

**5. `Using @ViewChild()` or `@ViewChildren()`**
- A parent component can directly access the properties and methods of its child components using `@ViewChild()` or `@ViewChildren()`.

**Parent Component:**
```
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { ChildComponent } from './child.component';

@Component({
  selector: 'parent',
  template: `
    <child></child>
    <p>Message from child: {{ childMessage }}</p>
  `,
})
export class ParentComponent implements AfterViewInit {
  @ViewChild(ChildComponent) child: ChildComponent;
  childMessage: string;

  ngAfterViewInit() {
    this.childMessage = this.child.childMessage;
  }
}
```
**Child Component:**
```
import { Component } from '@angular/core';

@Component({
  selector: 'child',
  template: `<p>Child Component</p>`,
})
export class ChildComponent {
  childMessage = 'Hello from child!';
}
```

---
## Q. Authentication in Angular
Authentication is the process of verifying a user's identity. In Angular applications, this typically involves verifying credentials (like username and password) against a server. Here's a general overview of how to implement authentication in Angular:

#### 1. Setting Up a Backend Server
- You'll need a backend server to handle user authentication. This server will:
  - Receive login requests from the Angular application.
  - Verify the provided credentials (e.g., against a database).
  - Issue a token (e.g., JWT - JSON Web Token) upon successful authentication.
  - Handle subsequent requests from the Angular application, verifying the token to ensure the user is authenticated.
  - The specific implementation of the backend server is beyond the scope of this document, but popular choices include Node.js with Express, Django, Ruby on Rails, and ASP.NET.

#### 2. Installing Necessary Modules
- In your Angular project, you might need modules like:
  - `@angular/common`: For making HTTP requests.
  - `rxjs`: For handling asynchronous operations.

#### 3. Creating an Authentication Service
- Create an Angular service to handle authentication-related logic. This service will typically include methods for:
  - `login()`: Sends a request to the backend server with the user's credentials.
  - `logout()`: Clears any stored tokens and user information.
  - `isAuthenticated()`: Checks if the user is currently authenticated (e.g., by checking for a valid token).
  - `storeToken()`: Stores the token received from the backend.
  - `getToken()`: Retrieves the token.

```javascript
import { Injectable } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { Observable, throwError, BehaviorSubject } from 'rxjs';
import { catchError, tap } from 'rxjs/operators';

interface AuthResponse {
    token: string;
    expiresIn: number;
}

@Injectable({
    providedIn: 'root',
})
export class AuthService {
    private apiUrl = 'http://your-backend-api/auth'; // Replace with your API URL
    private tokenKey = 'authToken';
    private loggedIn = new BehaviorSubject<boolean>(this.isAuthenticated()); // Track login status

    get isLoggedIn$() {
        return this.loggedIn.asObservable();
    }

    constructor(private http: HttpClient) {}

    login(credentials: any): Observable<AuthResponse> {
        return this.http.post<AuthResponse>(`${this.apiUrl}/login`, credentials).pipe(
            tap((response: AuthResponse) => {
                this.storeToken(response.token, response.expiresIn);
                this.loggedIn.next(true); // Update login status
            }),
            catchError(this.handleError)
        );
    }

    logout(): void {
        localStorage.removeItem(this.tokenKey);
        this.loggedIn.next(false); // Update login status
    }

    isAuthenticated(): boolean {
        return !!localStorage.getItem(this.tokenKey);
    }

    getToken(): string | null {
        return localStorage.getItem(this.tokenKey);
    }

    private storeToken(token: string, expiresIn: number): void {
        localStorage.setItem(this.tokenKey, token);
        // You might also want to store an expiry timestamp
        const expiresAt = new Date(Date.now() + expiresIn * 1000); // Convert seconds to milliseconds
        localStorage.setItem('tokenExpiration', expiresAt.toISOString());
    }

    private handleError(error: any) {
        let errorMessage = 'An error occurred';
        if (error.error instanceof ErrorEvent) {
            // Client-side error
            errorMessage = `Error: ${error.error.message}`;
        } else {
            // Server-side error
            errorMessage = `Error Code: ${error.status}\nMessage: ${error.message}`;
        }
        return throwError(errorMessage);
    }
}
```

#### 4. Creating a Login Component
- Create a component with a form for the user to enter their credentials.
- In the component, inject the `AuthService` and use it to send the login request.
- Handle the response from the server (success or error).
- Upon successful login, you'll typically want to:
  - Store the token.
  - Redirect the user to a protected area of the application.

```javascript
import { Component } from '@angular/core';
import { Router } from '@angular/router';
import { AuthService } from '../auth.service';

@Component({
    selector: 'login',
    template: `
      <form (ngSubmit)="onSubmit()" #loginForm="ngForm">
        <div>
          <label for="username">Username</label>
          <input type="text" id="username" name="username" [(ngModel)]="credentials.username" required />
        </div>
        <div>
          <label for="password">Password</label>
          <input type="password" id="password" name="password" [(ngModel)]="credentials.password" required />
        </div>
        <button type="submit" [disabled]="loginForm.invalid">Login</button>
        <div *ngIf="error" style="color: red;">{{ error }}</div>
      </form>
    `,
})
export class LoginComponent {
    credentials = { username: '', password: '' };
    error = '';

    constructor(private authService: AuthService, private router: Router) {}

    onSubmit() {
        this.authService.login(this.credentials).subscribe(
            (response) => {
                // Handle successful login (e.g., redirect)
                this.router.navigate(['/dashboard']);
            },
            (errorMessage) => {
                this.error = errorMessage;
            }
        );
    }
}
```

#### 5. Creating an Auth Guard
- Create an Angular route guard to protect routes that should only be accessible to authenticated users.
- In the guard, inject the `AuthService` and use the `isAuthenticated()` method to check if the user is logged in.
- If the user is not authenticated, redirect them to the login page.

```javascript
import { Injectable } from '@angular/core';
import { CanActivate, Router, ActivatedRouteSnapshot, RouterStateSnapshot } from '@angular/router';
import { AuthService } from '../auth.service';
import { Observable } from 'rxjs';

@Injectable({
    providedIn: 'root',
})
export class AuthGuard implements CanActivate {
    constructor(private authService: AuthService, private router: Router) {}

    canActivate(route: ActivatedRouteSnapshot, state: RouterStateSnapshot): Observable<boolean> | Promise<boolean> | boolean {
        if (!this.authService.isAuthenticated()) {
            this.router.navigate(['/login'], { queryParams: { returnUrl: state.url } });
            return false;
        }
        return true;
    }
}
```
_Register the guard in your routing module:_
```javascript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { LoginComponent } from './login.component';
import { DashboardComponent } from './dashboard.component'; // Example protected component
import { AuthGuard } from './auth.guard';

const routes: Routes = [
    { path: 'login', component: LoginComponent },
    { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] }, // Protect this route
    { path: '', redirectTo: '/login', pathMatch: 'full' },
];

@NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule],
})
export class AppRoutingModule {}
```

#### 6. Handling HTTP Interceptors (Optional)
- You can use an HTTP interceptor to automatically add the authentication token to the headers of outgoing HTTP requests to your backend API. This simplifies your code, as you don't have to manually add the token to every request.
```javascript
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { Observable } from 'rxjs';
import { AuthService } from './auth.service';

@Injectable()
export class AuthInterceptor implements HttpInterceptor {
    constructor(private authService: AuthService) {}

    intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
        const token = this.authService.getToken();
        if (token) {
            const clonedRequest = request.clone({
                setHeaders: {
                    Authorization: `Bearer ${token}`, // Or whatever your server expects
                },
            });
            return next.handle(clonedRequest);
        } else {
            return next.handle(request);
        }
    }
}
```
_Register the interceptor in your app.module.ts:_
```typescript
import { NgModule } from '@angular/core';
import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
import { AuthInterceptor } from './auth.interceptor';

@NgModule({
    // ...
    imports: [
        // ...
        HttpClientModule,
    ],
    providers: [
        // ...
        {
            provide: HTTP_INTERCEPTORS,
            useClass: AuthInterceptor,
            multi: true,
        },
    ],
    // ...
})
export class AppModule {}
```

#### Link:
**[Authentication and JWT in Node.js](https://dev.to/eidorianavi/authentication-and-jwt-in-node-js-4i13)**


---
## Q. Optimizing Your Angular Application
Optimizing your Angular application is crucial for achieving better performance, faster load times, and a smoother user experience. Here's a comprehensive guide to help you optimize your Angular application:

#### 1. Lazy Loading Modules
- **What it is:** Lazy loading is a technique that loads parts of your application on demand, rather than loading everything upfront. This can significantly reduce the initial load time of your application.
- **How to implement:** Use the `loadChildren` property in your route definitions to specify modules that should be loaded lazily.
```
const routes: Routes = [
  {
    path: 'lazy',
    loadChildren: () =>
      import('./lazy/lazy.module').then((m) => m.LazyModule),
  },
];
```

#### 2. Ahead-of-Time (AOT) Compilation
**What it is:** AOT compilation compiles your Angular templates and components at build time, rather than in the browser at runtime. This results in smaller bundle sizes and faster rendering.
**How to enable:** AOT is enabled by default in production builds (`ng build --prod`).  For Angular CLI versions prior to 8, use `ng build --aot`.

#### 3. Production Mode
**What it is:** Running your Angular application in production mode disables development-mode checks and optimizations, resulting in improved performance.How to enable:Use the --prod flag when building your application: `ng build --prod`

#### 4. Bundle Optimization
**What it is:** Reducing the size of your application's bundles is crucial for faster loading.
**How to optimize:**
- _Tree Shaking:_ Eliminate unused code.  Angular CLI and modern bundlers like Webpack do this automatically.
- _Minification:_ Reduce the size of your code by removing whitespace and shortening variable names.  Enabled in production builds.
- _Code Splitting:_ Split your code into smaller chunks that can be loaded on demand.  Lazy loading is a form of code splitting.

#### 5. Caching
**What it is:** Caching can significantly improve performance by storing frequently accessed data or resources.
**How to implement:** 
- _HTTP caching:_ Configure your server to set appropriate HTTP headers (e.g., `Cache-Control`) to enable browser caching of static assets and API responses.
- _In-memory caching:_ Use services to cache data within your Angular application (e.g., using `localStorage`, `sessionStorage`, or a custom service with a `BehaviorSubject`).
- _Service Workers:_ For more advanced caching, you can use service workers to cache assets and even enable offline functionality.  Use `@angular/service-worker`.

#### 6. Change Detection Optimization
**What it is:** Angular's change detection mechanism can be a performance bottleneck if not used carefully.
**How to optimize:**
- `ChangeDetectionStrategy.OnPush`: Use this change detection strategy for components whose templates only depend on their `@Input()` properties. This tells Angular to only check for changes when the input properties change.
```
import { Component, Input, ChangeDetectionStrategy } from '@angular/core';

@Component({
  selector: 'my-component',
  template: `<div>{{ data }}</div>`,
  changeDetection: ChangeDetectionStrategy.OnPush,
})
export class MyComponent {
  @Input() data: any;
}
```
- _trackBy:_ Use the trackBy function in *ngFor loops to help Angular identify which items in a list have changed, allowing it to update only the changed items.
- 
```
<li *ngFor="let item of items; trackBy: trackById">
  {{ item.name }}
</li>

export class MyComponent {
  items = [{ id: 1, name: 'A' }, { id: 2, name: 'B' }];
  trackById(index: number, item: any) {
    return item.id;
  }
}
```
- _Detach Change Detector:_ If you have a component whose subtree you know doesn't need to be checked, you can detach its change detector.
```
constructor(private cd: ChangeDetectorRef) {}

ngOnInit() {
  this.cd.detach();
}
```

#### 7. Optimize Images
**What it is:** Large image files can significantly slow down your application.
**How to optimize:**
- _Use appropriate formats:_ Use modern image formats like WebP, which offer better compression than JPEG or PNG.
- _Compress images:_ Use tools to compress images without significant loss of quality.
- _Use responsive images:_  Serve different sized images based on the user's device and screen size using the `<picture>` element or the `srcset` attribute of the `<img>` tag.
- _Lazy load images:_  Load images only when they are about to become visible in the viewport using libraries or native lazy loading (`loading="lazy"`).

#### 8. Optimize Dependencies
**What it is:** Unnecessary or large dependencies can increase your bundle size and slow down your application.
**How to optimize:** 
- _Analyze your dependencies:_ Use tools to identify large or unused dependencies.
- _Remove unused dependencies:_  Get rid of any dependencies that you are not using.
- _Use smaller alternatives:_  Look for smaller alternatives to large libraries.
- _Tree shaking:_  Ensure that your dependencies are tree-shakable.


#### 9. Virtualization/Windowing
**What it is:** For lists with a very large number of items, rendering all of them at once can be very slow. Virtualization or windowing is a technique that only renders the items that are currently visible in the viewport.
**How to implement:**
- Use libraries like `ngx-virtual-scroll`, `@angular/cdk Virtual Scroll`, or `react-virtualized` (if using React within Angular) to implement virtualization.

#### 10. Web Worker
**What it is:** Web workers allow you to run JavaScript code in a background thread, freeing up the main thread to handle UI updates and other tasks.
**How to implement:** 
- Use Angular CLI to generate a web worker:  `ng generate web-worker my-worker`
- Offload computationally intensive tasks to the web worker.

By implementing these optimizations, you can significantly improve the performance of your Angular application, resulting in a faster, more responsive, and more enjoyable user experience.

---
## Q. AOT vs JIT
Angular applications require compilation because browsers cannot directly understand Angular components and templates. The two primary compilation methods are _Ahead-of-Time (AOT)_ and _Just-in-Time (JIT)_. 

1. **Ahead-of-Time (AOT)** 
- AOT compilation occurs during the build process. It translates Angular HTML and TypeScript code into efficient JavaScript code before the browser downloads and runs it.  

**Advantages of AOT:** 
• _Faster rendering:_ The browser renders the UI immediately upon loading, without waiting for compilation. 
• _Smaller bundle size:_ AOT eliminates the need to ship the Angular compiler in the production bundle, reducing the overall size. [2]  
• _Improved security:_ Pre-compilation mitigates the risk of client-side code injection attacks. 
• _Template type checking:_ AOT performs template type checking during compilation, catching errors early in the development cycle. 

2. **Just-in-Time (JIT)** 
JIT compilation occurs at runtime in the browser. The Angular compiler translates the application code into JavaScript as it's needed. 

**Advantages of JIT:**
• _Faster development cycle:_ JIT allows for rapid iteration during development, as changes are quickly reflected without a full rebuild. 
• _Easier debugging:_ Source maps are used for debugging, making it easier to trace errors back to the original code. 

**Key Differences Summarized**

| Feature | AOT | JIT  |
| --- | --- | --- |
| Compilation Time | Build time | Runtime  |
| Initial Load Time | Faster | Slower  |
| Bundle Size | Smaller | Larger  |
| Security | Improved | Less secure  |
| Development Speed | Slower build times | Faster iteration  |
| Debugging | More challenging | Easier  |
| Use Cases | Production builds | Development  |

**Conclusion**
- AOT is generally preferred for production environments due to its performance and security benefits. JIT is useful during development for its rapid iteration capabilities. In recent Angular versions, AOT is the default compilation mode.

---
## Q. Create Dynamic Table column in angular

```html
<div class="container">
  <h2>Dynamic Table Example</h2>
  
  <table border="1">
    <thead>
      <tr>
        <th *ngFor="let column of columns">{{ column.header }}</th>
      </tr>
    </thead>
    <tbody>
      <tr *ngFor="let row of data">
        <td *ngFor="let column of columns">{{ row[column.key] }}</td>
      </tr>
    </tbody>
  </table>
</div>
  `
```

```javascript
interface DynamicColumn {
  key: string;
  header: string;
}

interface DataRow {
  [key: string]: any;
}

export class App implements OnInit {
  columns: DynamicColumn[] = [];
  data: DataRow[] = [
    { name: 'John', age: 30, city: 'New York' },
    { name: 'Jane', age: 25, city: 'London', occupation: 'Engineer' },
    { name: 'Jane', age: 25, city: 'London', occupation: 'Engineer', sex: 'male' }
  ];

  ngOnInit() {
    // get unique keys from the data
    this.columns = this.getUniqueKeys(this.data).map(key => ({
      key: key,
      header: this.capitalizeFirstLetter(key)
    }));
  }

  private getUniqueKeys(data: DataRow[]): string[] {
    const keys = new Set<string>();
    data.forEach(row => {
      Object.keys(row).forEach(key => keys.add(key));
    });
    return Array.from(keys);
  }

  private capitalizeFirstLetter(str: string): string {
    return str.charAt(0).toUpperCase() + str.slice(1);
  }

}
```
---
## Q. Here are **Angular best practices** to implement **efficient and reusable frontend components**, focusing on maintainability, scalability, and performance:

---

## ✅ 1. **Use Presentational & Container Component Pattern**

* **Container Components**: Handle data-fetching and business logic.
* **Presentational Components**: Focus only on UI and accept inputs/emit outputs.
* This separation promotes reusability and clean code architecture.

```ts
// Presentational: expense-card.component.ts
@Input() expense: Expense;
@Output() delete = new EventEmitter<number>();

// Container: expense-list.component.ts
<app-expense-card
  *ngFor="let exp of expenses"
  [expense]="exp"
  (delete)="deleteExpense($event)">
</app-expense-card>
```

## ✅ 2. **Keep Components Small and Focused**

* Follow the **Single Responsibility Principle**: each component should do one thing well.
* Split large components into smaller ones, especially when dealing with complex UIs.

## ✅ 3. **Use `@Input()` and `@Output()` Smartly**

* Use `@Input()` to pass data *into* a component.
* Use `@Output()` with `EventEmitter` to communicate *out*.
* Avoid tightly coupling components; use shared services only when needed.

## ✅ 4. **Use Angular Reactive Forms for Complex Forms**

* More scalable than template-driven forms.
* Easier to unit test and dynamically control validation, visibility, and nested structures.

## ✅ 5. **Avoid Logic in Templates**

* Move complex expressions to the component class.
* It improves readability and simplifies testing.

```html
<!-- Bad -->
<div *ngIf="items.length > 0 && !loading">...</div>

<!-- Good -->
<div *ngIf="hasItems">...</div>
```

```ts
get hasItems(): boolean {
  return this.items.length > 0 && !this.loading;
}
```

## ✅ 6. **Use `trackBy` in `*ngFor` Loops**

Improves performance by preventing unnecessary re-renders:

```html
<li *ngFor="let user of users; trackBy: trackById">{{ user.name }}</li>
```

```ts
trackById(index: number, item: User): number {
  return item.id;
}
```

## ✅ 7. **Modularize Your App**

* Create **feature modules** (`ExpenseModule`, `AuthModule`, etc.).
* Use **shared modules** for reusable components, directives, and pipes.

## ✅ 8. **Style Components with View Encapsulation**

* Keep styles scoped with Angular’s encapsulation (default is `Emulated`).
* Use component-specific SCSS/CSS files for maintainability.

## ✅ 9. **Lazy Load Feature Modules**

* Improve initial load performance.
* Use Angular routing to lazy-load modules when needed.

```ts
{ path: 'expenses', loadChildren: () => import('./expenses/expenses.module').then(m => m.ExpensesModule) }
```

## ✅ 10. **Use Services and Dependency Injection (DI)**

* Extract business logic and API calls into services.
* Inject services into components via DI to promote reusability and testing.

## ✅ 11. **Use Angular CLI and Linting Tools**

* Follow style guides and enforce standards using ESLint.
* Use CLI to generate code scaffolds with best practices in place.

## ✅ 12. **Write Unit and Integration Tests**

* Use `TestBed`, mocks, and spies to ensure component behavior is predictable.
* Keep test coverage high, especially for reusable components.

---
## Q. When to use ngoninit and constructor in Angular
#### Constructor:
- Primarily used for dependency injection.
- Initializes class members and sets up the class.
- Avoid placing complex logic or operations that might cause side effects.
- It's a TypeScript feature that is called when a new instance of the class is created.

#### ngOnInit:
- A lifecycle hook called after Angular has initialized the component's inputs and bindings.
- Suitable for tasks that require the component to be fully initialized, such as fetching data, setting up subscriptions, or performing calculations based on input properties.
- It is specific to Angular and part of the component's lifecycle.

```typescript
import { Component, OnInit } from '@angular/core';
import { MyService } from './my.service';

@Component({
  selector: 'app-my-component',
  template: `...`,
})
export class MyComponent implements OnInit {
  constructor(private myService: MyService) {
    // Dependency injection and basic initialization
  }

  ngOnInit() {
    // Fetch data, set up subscriptions, etc.
    this.myService.getData().subscribe(data => {
      // Process data
    });
  }
}
```
---
## Q. Angular form vs Reactive form
Here's a comprehensive overview of **Angular Forms** with a focus on **Reactive Forms**, including comparison, examples, and best practices.

---

## ✅ Angular Forms Overview

Angular offers **two types of forms**:

| Form Type                 | Description                                                                                  |
| ------------------------- | -------------------------------------------------------------------------------------------- |
| **Template-driven forms** | Simpler to use, defined mostly in HTML using `ngModel`, suitable for basic use cases         |
| **Reactive forms**        | More scalable, defined in the component class, offers better testability and dynamic control |

---

## ✅ Reactive Forms – Key Features

* Defined and controlled in **TypeScript class**.
* Built using `FormGroup`, `FormControl`, and `FormArray`.
* Easy to **dynamically add/remove fields**, handle **complex validations**, and **unit test**.

---

## 🔧 Setup

First, import the necessary module:

```ts
import { ReactiveFormsModule } from '@angular/forms';
```

In `app.module.ts`:

```ts
@NgModule({
  imports: [
    ReactiveFormsModule
  ]
})
export class AppModule {}
```

---

## ✨ Reactive Forms Example (Expense Form)

### 📁 **expense-form.component.ts**

```ts
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-expense-form',
  templateUrl: './expense-form.component.html'
})
export class ExpenseFormComponent implements OnInit {
  expenseForm!: FormGroup;

  constructor(private fb: FormBuilder) {}

  ngOnInit() {
    this.expenseForm = this.fb.group({
      title: ['', Validators.required],
      amount: [null, [Validators.required, Validators.min(1)]],
      category: ['Food', Validators.required],
      date: [new Date(), Validators.required]
    });
  }

  onSubmit() {
    if (this.expenseForm.valid) {
      console.log('Form Submitted:', this.expenseForm.value);
    }
  }
}
```

---

### 🧾 **expense-form.component.html**

```html
<form [formGroup]="expenseForm" (ngSubmit)="onSubmit()">
  <label>Title:</label>
  <input type="text" formControlName="title" />
  <div *ngIf="expenseForm.get('title')?.invalid && expenseForm.get('title')?.touched">
    Title is required.
  </div>

  <label>Amount:</label>
  <input type="number" formControlName="amount" />
  <div *ngIf="expenseForm.get('amount')?.errors?.['min']">
    Amount must be at least 1.
  </div>

  <label>Category:</label>
  <select formControlName="category">
    <option value="Food">Food</option>
    <option value="Travel">Travel</option>
    <option value="Bills">Bills</option>
  </select>

  <label>Date:</label>
  <input type="date" formControlName="date" />

  <button type="submit" [disabled]="expenseForm.invalid">Submit</button>
</form>
```

---

## ✅ Best Practices with Reactive Forms

1. **Use FormBuilder**: Simplifies syntax for creating nested forms.
2. **Group Fields Logically**: Use `FormGroup` for related controls (e.g., address fields).
3. **Custom Validators**: For complex business logic.
4. **Async Validators**: For backend validations like checking username availability.
5. **Reactive Form Hooks**: Use `valueChanges` and `statusChanges` to react to form changes.

---

## 🔍 Template-Driven Form (Quick Example)

> Not ideal for dynamic or complex forms.

```html
<form #form="ngForm" (ngSubmit)="submit(form.value)">
  <input name="name" ngModel required />
  <input type="email" name="email" ngModel />
  <button type="submit">Submit</button>
</form>
```

---

## 🚀 Summary

| Feature                     | Reactive Forms ✅ | Template-driven Forms ❌ |
| --------------------------- | ---------------- | ----------------------- |
| Suitable for large forms    | ✅                | ❌                       |
| Unit test friendly          | ✅                | ❌                       |
| Complex validation handling | ✅                | ❌                       |
| Dynamic form controls       | ✅                | ❌                       |
| Simpler syntax              | ❌                | ✅                       |

---
## Q. How to migrate from Angular version 10 to 17? 

- **Update Node.js and npm:** Ensure you have a compatible version of Node.js (v18.13.0 or later) and npm (v10 or later). You can update Node.js from the official website and npm using the command `npm install -g npm@latest`. 
- **Update Angular CLI:** Update the Angular CLI globally using `npm install -g @angular/cli@latest`. 
- **Update Angular Packages:** Navigate to your project directory in the command line and `run ng update @angular/core@latest @angular/cli@latest`. This command updates all Angular packages to the latest version. You might also need to update other packages like `@angular/material` and `@angular/cdk` if you are using them. 
- **Address Breaking Changes:** Review the Angular update guide for each version between 10 and 17 to identify and address breaking changes. This might involve changes in APIs, templates, or configurations. Pay special attention to changes related to: 
  - **Modules:** Angular 17 encourages the use of standalone components, directives, and pipes. Consider migrating your modules to this new approach. 
	- **Control Flow Syntax:** Angular 17 introduces a new built-in control flow syntax in templates. Update your templates to use the new syntax (`@if`, `@for`, `@switch`). 
	- **Forms:** If you are using reactive forms, you might need to adjust your code due to changes in type definitions and form handling. 

- **Test Thoroughly:** 
  - After the update, run all your tests to ensure that the application is working as expected. Pay attention to both unit and end-to-end tests. 
- **Address Deprecations:** 
  - Angular might have deprecated some features in older versions. Replace any deprecated code with the recommended alternatives. 
- **Update Third-Party Libraries:** 
  - Ensure that your third-party libraries are compatible with Angular 17. Update them to the latest versions if necessary. 
- **Code Cleanup:** 
  - Remove any unused code, modules, or dependencies. This is a good time to refactor and improve the overall structure of your application. 
- **Commit Changes:** 
  - Commit your changes regularly throughout the migration process. This makes it easier to revert to a previous state if necessary. 
- **Consider Incremental Updates:** 
  - For large applications, consider updating one major version at a time (e.g., `10 to 11`, then `11 to 12`, and so on). This can help to manage the complexity of the migration. 

---
### Q. RxJS vs NgRx 
RxJS is a reactive programming library in JavaScript that helps manage asynchronous operations using observables, while NgRx is an Angular library built on top of RxJS that provides a structured approach to state management in Angular applications. NgRx implements the Redux pattern, which uses a centralized store, actions, reducers, and selectors, to manage the application state. 
  
Here's a more detailed breakdown:  

### RxJS:

### Purpose: 
Primarily used for handling asynchronous data, creating streams of data (observables), and composing asynchronous or callback-based code.

### Features: 
Observables, operators (like `map`, `filter`, `subscribe`), subjects, and more. 

### Use Cases:
	• Handling API requests.
	• Managing events.  
	• Creating shared services that expose observables.
	• Building custom reactive components or services.  

### NgRx: 

### Purpose: 
A library for managing the state of an Angular application, providing a structured and consistent way to handle state changes using the Redux pattern.

### Features:  
	- Store: A central repository for the application state.
	- Actions: Plain JavaScript objects that describe a change to the state.
	- Reducers: Pure functions that take the current state and an action, and return a new state.
	- Selectors: Functions that extract data from the store.
	- Effects: Side effects that can be triggered by actions, such as making API calls or navigating to different pages.

### Use Cases:
- Managing global application state.
- Handling complex state changes.
- Making applications more predictable and testable.

### In essence:

- NgRx is a higher-level library that provides a framework for managing state within Angular, while RxJS is a foundational library for reactive programming in JavaScript.
- NgRx relies heavily on RxJS under the hood, using observables to handle asynchronous operations and track state changes.
- Choose NgRx when you need a centralized and well-structured approach to state management, particularly in larger and more complex Angular applications.
- Use RxJS for more general asynchronous tasks and when you need a more flexible and lower-level approach to reactive programming.

### When to use which:  

- **RxJS:** Suitable for small applications, local component state, or when you need fine-grained control over asynchronous operations. 
- **NgRx:** Best for larger, more complex applications where managing a single global state and ensuring a predictable data flow is crucial.

---
## Q. Remove Duplicate Elements from TypeScript Array

### Approach 1: Using `filter()` method
```typescript
let arr = [1, 2, 2, 3, 4, 3, 5, 4, 6, 5];
 
const removeDups = (arr: number[]): number[] => {
    return arr.filter((item,
        index) => arr.indexOf(item) === index);
}
console.log(removeDups(arr));
```

### Approach 2: Using `forEach()` method
```typescript
let arr = [1, 2, 2, 3, 4, 3, 5, 4, 6, 5];

const removeDups = (arr: number[]) : number[] => {
    let unique: number[] = [];
    arr.forEach(element => {
        if (!unique.includes(element)) {
            unique.push(element);
        }
    });
    return unique;
}
console.log(removeDups(arr));
```

### Approach 3: Using `map() ` method
```typescript
let arr = [1, 2, 2, 3, 4, 3, 5, 4, 6, 5];

const removeDups = (arr: number[]): number[] => {
    const map = new Map<number, boolean>();
    const unique: number[] = [];

    arr.forEach(item => {
        if (!map.has(item)) {
            map.set(item, true);
            unique.push(item);
        }
    });

    return unique;
}

console.log(removeDups(arr));
```

### Approach 3: Using `map() ` method
```typescript
let arr = [1, 2, 2, 3, 4, 3, 5, 4, 6, 5];

const removeDups = (arr: number[]): number[] => {
    return [...new Set(arr)];
}

const uniqueNumbers = [...new Set(numbers)];
 
console.log(removeDups(arr));
```

#### Output: Same for all approached
```
[ 1, 2, 3, 4, 5, 6]
```

---
## Q. Micro frontend in Angular
In Angular, micro frontends are an architectural pattern where a large web application is broken down into smaller, independently deployable modules, also known as micro-applications. Each micro-application handles specific features and can be developed, deployed, and maintained separately. 

Here's a more detailed explanation: 

### Key Concepts: 

- Independent Modules: Each micro-application is self-contained and doesn't rely on the code of other modules. 
- Independent Development: Different teams can work on different micro-applications concurrently, minimizing development conflicts.  
- Independent Deployment: Each micro-application can be deployed independently, allowing for faster releases of new features.  
- Composability: Micro-applications can be combined and integrated into a larger application using techniques like routing or web components.  

### Benefits of using Micro Frontends in Angular: 

- Improved Scalability: Micro-applications allow for a more modular approach to building and maintaining large applications. 
- Faster Development Cycles: Teams can work independently on smaller parts of the application, leading to faster development and release cycles.  
- Easier Maintenance: By isolating features into separate micro-applications, it becomes easier to identify, fix, and update specific functionalities.   
- Better Team Collaboration: Different teams can work on different micro-applications without interfering with each other's work.
- Enhanced Reliability: If one micro-application fails, it doesn't necessarily affect the rest of the application. 
- Reduced Code Duplication: Micro-applications can share common code and components, reducing code duplication and improving code reuse.

### Implementation in Angular:

- Module Federation: Webpack's Module Federation feature is often used to enable dynamic loading and sharing of modules between different micro-applications.  
- Angular Elements: Angular Elements allow you to create reusable components that can be used across different micro-applications.  
- Single SPA: Single SPA is a framework that simplifies the integration of multiple, independently developed front-end applications.

In essence, Angular micro frontends enable a more modular, scalable, and maintainable approach to building large, complex web applications by breaking them down into smaller, independent units.

---
## Q. Angular 19 features

---
## Q. View encapsulation in Angular
View encapsulation in Angular is a feature that controls how the CSS styles defined within a component affect other elements in the application. It helps to prevent CSS styles from "leaking" out of a component and affecting other components, and vice versa.

Angular provides three options for view encapsulation:

### 1. `Emulated` (Default)
- Angular emulates CSS encapsulation by adding unique attributes to the HTML elements in the component's template and prefixing the CSS selectors with these attributes.
- This ensures that the styles defined in a component apply only to the elements within that component's view.
- It's called "emulated" because the browser doesn't natively support this behavior. Angular achieves it through its own manipulation of the DOM and CSS.
Example:
```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-component',
  template: `
    <div class="my-class">
      <p>This is my component content.</p>
    </div>
  `,
  styles: [`
    .my-class {
      color: red;
    }
    p {
      font-size: 16px;
    }
  `],
  encapsulation: ViewEncapsulation.Emulated // Default
})
export class MyComponent { }
```
In the generated HTML, Angular might add a unique attribute like `_ngcontent-c0` to the elements:
```html
<div _ngcontent-c0="" 
class="my-class">
  <p _ngcontent-c0="">This is my component content.</p>
</div>
```
And the styles are transformed to:
```css
.my-class[_ngcontent-c0] {
  color: red;
}
p[_ngcontent-c0] {
  font-size: 16px;
}
```
As you can see, the styles are scoped to the component's elements.

### 2. `ShadowDom`
- Angular uses the browser's native Shadow DOM API to encapsulate the component's view.
- Shadow DOM creates a separate DOM tree for the component, effectively isolating its styles and markup from the rest of the application.
- This provides the strongest form of encapsulation, as styles and DOM structure are completely isolated.
- Example:
```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-component',
  template: `
    <div class="my-class">
      <p>This is my component content.</p>
    </div>
  `,
  styles: [`
    .my-class {
      color: red;
    }
    p {
      font-size: 16px;
    }
  `],
  encapsulation: ViewEncapsulation.ShadowDom
})
export class MyComponent { }
```
The HTML structure will be like this
```html
<my-component>
 #shadow-root
   <div class="my-class">
     <p>This is my component content.</p>
   </div>
</my-component>
```
- Any style defined in the component will be applied inside the `#shadow-root`

### 3. `None`
- Angular does not provide any view encapsulation.
- The styles defined in the component will apply globally to the entire application.
- This can be useful in some cases, such as when you want to use a global CSS library, but it can also lead to style conflicts if you're not careful.
- Example:
```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-component',
  template: `
    <div class="my-class">
      <p>This is my component content.</p>
    </div>
  `,
  styles: [`
    .my-class {
      color: red;
    }
    p {
      font-size: 16px;
    }
  `],
  encapsulation: ViewEncapsulation.None
})
export class MyComponent { }
```
The styles will apply to any element in the application with the class `my-class` or any `<p>` tag.

### Choosing an Encapsulation Mode
- `Emulated`:  The default and generally recommended option. It provides good encapsulation while maintaining compatibility with most browsers.
- `ShadowDom`: Provides the strongest encapsulation and aligns with web standards. Use this when you want complete style isolation, but be aware of limited support in older browsers.
- `None`: Use this option sparingly when you need global styles or are integrating with a CSS framework that requires global styles. Be very cautious about style collisions.

In most cases, you should stick with the default `Emulated` encapsulation. If you need stronger isolation and are targeting modern browsers, `ShadowDom` is a good choice. Use `None` only when absolutely necessary.


---
## Q. Approach to create application in angular (top down, down to up or component based or module based)?
Angular applications are typically developed using a **component-based** approach, which naturally leads to a **bottom-up** development style. Let's break down what this means:

### **Component-Based Architecture**

* Angular applications are built as a tree of reusable components. Each component encapsulates a specific part of the user interface and its associated logic.
* This promotes modularity, reusability, and maintainability.

### **Bottom-Up Development**

* You start by building the smaller, individual components first. These are the building blocks of your application (e.g., buttons, input fields, cards).
* Once the smaller components are ready, you compose them together to build larger components or views.
* Finally, you assemble the entire application by combining these views and components.

### **Why this approach?**

* **Reusability:** Components can be used in multiple places within the application, saving development time and ensuring consistency.
* **Maintainability:** Changes to one component are less likely to break other parts of the application.
* **Testability:** Individual components can be tested in isolation.
* **Parallel Development:** Different developers can work on different components simultaneously.
* **Scalability:** Component-based architecture makes it easier to scale the application as it grows.

### **Module-Based Architecture**

* Angular also uses modules, which are containers for components, services, and other related code.
* While applications are component-based, modules help organize the application into logical groups of functionality.
* You might have a `SharedModule` for reusable components, a `FeatureModule` for a specific feature, and so on.
* Modules work in conjunction with components.

### **Top-Down Development**

* While the overall approach is bottom-up, some initial high-level planning (which can be considered top-down) is beneficial.
* You might start by defining the main modules and routing structure of your application.
* However, the actual implementation of the UI and logic within those modules is still done in a bottom-up, component-based manner.

### **In summary**

The most effective approach for creating applications in Angular is a **component-based** approach, implemented using a **bottom-up** development style, and organized with **modules**.

---
## Q. Singleton in Angular
In Angular, a singleton is a service that is instantiated only once throughout the application's lifetime. This means that when the service is injected into different components or other services, they all receive the same instance.

Here's how singletons are typically created and used in Angular:

### **1. Using `@Injectable()` with `providedIn: 'root'`**

   -  The most common and recommended way to create a singleton in Angular is by using the `@Injectable()` decorator with the `providedIn: 'root'` option.

   -  When you specify `providedIn: 'root'`, Angular registers the provider with the root injector. The root injector is available to the entire application, ensuring that only one instance of the service is created.

   ```typescript
   import { Injectable } from '@angular/core';

   @Injectable({
     providedIn: 'root',
   })
   export class MySingletonService {
     private data: string[] = [];

     constructor() {
       console.log('MySingletonService constructor called'); // Called only once
     }

     addData(item: string) {
       this.data.push(item);
     }

     getData() {
       return this.data;
     }
   }
   ```

   -   In this example, `MySingletonService` will be created only once.  Any component or service that injects `MySingletonService` will receive the same instance.  The constructor will only be called a single time for the entire application.

### **2.  Registering in a Module (Not Recommended for Singletons)**

   -   You can also provide a service by adding it to the `providers` array of an Angular module. However, this can lead to multiple instances of the service if the module is loaded in multiple contexts (e.g., lazy-loaded modules).

   ```typescript
   import { NgModule } from '@angular/core';

   @NgModule({
     providers: [MySingletonService], // Potentially creates multiple instances
   })
   export class MyModule {}
   ```

   -   While this method *can* create a singleton within a specific module, it does not guarantee a single instance across the entire application, especially in applications with lazy loading.  Therefore, `providedIn: 'root'` is the preferred way to ensure a true application-wide singleton.

### **3.  `@Optional()` and `@SkipSelf()`**

   -   These decorators are used in the constructor of a service to control how Angular resolves dependencies. They are more related to hierarchical injection and preventing circular dependencies than creating singletons, but it's worth knowing about them in the context of service instantiation.
   -   `@Optional()`:  Allows Angular to inject a service even if it's not available. The injected parameter will be `null` if the service is not found.
   -   `@SkipSelf()`:  Tells Angular to start the dependency lookup from the parent injector, rather than the current injector.  This is used to avoid circular dependencies in certain scenarios.

### **Key Points about Angular Singletons:**

* **Application-Wide Instance:** A true singleton in Angular ensures that only one instance of the service exists for the entire application.
* **State Management:** Singletons are often used to manage shared state across different parts of an application.
* **Communication:** They can facilitate communication between components that don't have a direct parent-child relationship.
* **Services:** In Angular, singletons are implemented as services.
* **`providedIn: 'root'`:** This is the key to creating a reliable, application-wide singleton.

### **In summary:** 
To create a proper singleton in Angular, use the `@Injectable()` decorator with `providedIn: 'root'`. This ensures that your service is instantiated only once and that the same instance is shared throughout your application.

---
## Q. Making TypeScript Browser Compatible in Angular
TypeScript itself isn't directly executed by browsers. Browsers only understand JavaScript. Therefore, the Angular build process involves compiling your TypeScript code into JavaScript that browsers can understand.  Here's how you ensure that this generated JavaScript is compatible across different browsers:

### 1. Target the Right ECMAScript Version
- TypeScript allows you to specify which version of ECMAScript (the standard that JavaScript is based on) you want your code to be compiled to.  This is done in the `tsconfig.json` file.
- The target property in tsconfig.json determines the ECMAScript version.
```javascript
{
  "compilerOptions": {
    "target": "es2017", // Or "es5", "es6", "es2015", etc.
    // ... other options
  }
}
```

- Choosing a Target:
  - `es5`:  The oldest target, but has the widest browser support (including older browsers like Internet Explorer 11).  This will result in the largest output JavaScript file, as modern syntax needs to be converted to older, more verbose syntax.
  - `es2015` (ES6): A good balance of modern syntax and decent browser support.
  - `es2017` and later: Uses more modern JavaScript features, but may not be supported by older browsers.
  - `esnext`: uses the latest features.
  
- Best Practice:
  - Start with a higher target (e.g., es2015 or es2017) for better performance and smaller output size.
  - If you need to support older browsers, use a tool like Babel (see below) or set the target to `es5`. Angular CLI uses Babel.

### 2. Polyfills
- Even when targeting a specific ECMAScript version, some browsers might not support all the features used in your code (or in the libraries you use, including Angular itself).
- Polyfills are pieces of code that provide implementations for these missing features.Angular includes core polyfills for essential features.  You can find these in the `polyfills.ts` file in your Angular project.
- Important Polyfills:
  - `zone.js`: Required for Angular's change detection to work.
  - `reflect-metadata`: Used for Angular's dependency injection.
  - ES6 features (e.g., `Map`, `Set`, `Promise`) are included if you uncomment the relevant imports in `polyfills.ts`.
- Example `polyfills.ts`:
```javasctipt
/**
 * This file includes polyfills needed by Angular and is loaded before the app.
 * You can add your own extra polyfills to this file.
 */

import 'zone.js/node';  // Included with Angular CLI.
import 'zone.js/browser';  // Included with Angular CLI.

// If you need to support older browsers, include specific polyfills here.
// import 'core-js/es6/symbol';
// import 'core-js/es6/reflect';
// import 'core-js/es7/reflect';
// import 'zone.js/dist/zone';  // Included with Angular CLI.

/** Application is running with production mode. */
// if (environment.production) {
//   enableProdMode();
// }
```
- For broadest compatibility uncomment the needed polyfills in `polyfills.ts`

### 3. Babel (Handled by Angular CLI)
- Babel is a JavaScript compiler that can transform modern JavaScript code into a version that older browsers can understand.
- Angular CLI uses Babel under the hood (with `@babel/preset-env`) to handle this transformation.
- You don't usually need to configure Babel directly in Angular projects. The Angular CLI and its build process take care of it for you.
- Babel uses the target setting from your `tsconfig.json` to determine how to transform your code. It also uses browserlist (see below).

### 4. Browserlist (Handled by Angular CLI)
- Browserlist is a configuration that specifies which browsers your project needs to support.
- Angular CLI uses Browserlist to tell Babel which transformations are needed for your target browsers.
- The Browserlist configuration is usually in a file named .browserslistrc at the root of your project, or within the `package.json` file.
```
Example `.browserslistrc`:
```
> 1%
last 2 versions
not dead
```
This configuration targets:
    * Browsers with more than 1% global usage
    * The last 2 versions of each browser
    * Browsers that are not dead (no longer maintained)
```
- Example in `package.json`:
`json "browserslist": [ "> 1%", "last 2 versions", "not dead" ]` 

### 5. Angular CLI Build Process
- When you build your Angular application using ng build, the following happens:
  - TypeScript code is compiled to JavaScript, according to the target setting in tsconfig.json.
  - Babel (via Angular CLI) transforms the resulting JavaScript code based on your `.browserslistrc` configuration, adding any necessary transformations to ensure compatibility with your target browsers.
  - Webpack (or other bundler) bundles the JavaScript files, along with other assets (CSS, images, etc.), into a set of files that can be deployed to a web server.
  - Polyfills from `polyfills.ts` are included in the bundle.
  
### In Summary
To make your Angular application compatible with different browsers:
1. Set the `target` in `tsconfig.json`: Choose an appropriate ECMAScript version.
2. Configure Polyfills: Ensure necessary polyfills are included in `polyfills.ts`.
3. Use Angular CLI: The Angular CLI handles Babel and Browserlist configuration for you, ensuring that your code is transformed correctly for your target browsers.

By following these steps, you can ensure that your Angular application works across a wide range of browsers, including older ones.

---
## Q. How do you prevent the form on back of a browser in angular using canActivate?
```typescript
import { Injectable } from '@angular/core';
import { CanActivate, Router } from '@angular/router';
import { FormComponent } from '../components/form/form.component';

@Injectable({
  providedIn: 'root'
})
export class FormGuard implements CanActivate {
  constructor(private router: Router) {}

  canActivate(component: FormComponent): boolean {
    if (component.hasUnsavedChanges()) {
      return window.confirm('You have unsaved changes. Do you really want to leave?');
    }
    return true;
  }
}
```
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-form',
  templateUrl: './form.component.html',
  styleUrls: ['./form.component.css']
})
export class FormComponent {
  private unsavedChanges = false;

  // Call this method when form data changes
  onFormChange() {
    this.unsavedChanges = true;
  }

  // Call this method when form is submitted
  onSubmit() {
    // Handle form submission logic
    this.unsavedChanges = false;
  }

  hasUnsavedChanges(): boolean {
    return this.unsavedChanges;
  }
}
```
```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { FormComponent } from './components/form/form.component';
import { FormGuard } from './guards/form.guard';

const routes: Routes = [
  { path: 'form', component: FormComponent, canActivate: [FormGuard] },
  // other routes
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### Summary of Steps:

- Create a guard that checks for unsaved changes.
- Implement a method in your form component to track changes.
- Use the guard in your routing configuration to protect the form route.


---
## Q. When does renderer calls in angular using example
Renderer calls in Angular are invoked during the component's lifecycle, specifically when changes occur that affect the view. These calls are essential for updating the DOM and ensuring the UI reflects the current state of the application. The `Renderer2` service in Angular provides an abstraction layer for manipulating the DOM, promoting platform independence and testability. 

### Change Detection 
Angular's change detection mechanism plays a crucial role in triggering renderer calls. After each asynchronous event, such as user interactions (e.g., clicks, input changes), HTTP requests, or timers, Angular runs change detection to check for updates in the component tree. If changes are detected, the renderer is invoked to update the DOM accordingly. 

### Lifecycle Hooks 
#### Several lifecycle hooks can trigger renderer calls: 

- `ngAfterViewInit`: Called after the component's view and child views have been initialized. This is a common place to perform DOM manipulations using the renderer. 
- `ngAfterViewChecked`: Called after the component's view and child views have been checked. It's invoked after `ngAfterViewInit` and on subsequent change detection cycles. 
- `afterRender`: Invoked after Angular has finished rendering all components on the page into the DOM. It is executed in the order it was registered and once per render.  
- `afterNextRender`: Registers a callback that executes only once after the next render cycle, when the DOM is loaded.

#### Example 
```typescript
import { Component, Renderer2, ElementRef, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-example',
  template: '<div #myElement>Hello</div>',
})
export class ExampleComponent implements AfterViewInit {
  constructor(private renderer: Renderer2, private el: ElementRef) {}

  ngAfterViewInit() {
    // Access the element using ElementRef
    const myElement = this.el.nativeElement.querySelector('#myElement');

    // Use Renderer2 to modify the element
    this.renderer.setStyle(myElement, 'color', 'blue');
    this.renderer.setAttribute(myElement, 'title', 'My Element');
  }
}
```
In this example, the `Renderer2` is used within the `ngAfterViewInit` lifecycle hook to modify the style and attributes of a DOM element. This ensures that the DOM manipulation occurs after the view has been initialized. 

#### Directives 
Custom directives can also utilize the `Renderer2` to interact with the DOM. Structural directives like `@if` and `@for` modify the DOM structure, implicitly using the renderer. 

#### Programmatic Rendering 
Angular allows for programmatically creating and rendering components using `ViewContainerRef`. This mechanism also relies on the renderer to insert the new components into the DOM. 
```typescript
import { Component, ViewContainerRef, ComponentFactoryResolver } from '@angular/core';

@Component({
  selector: 'app-host',
  template: '<div #container></div>'
})
export class HostComponent {
  constructor(
    private viewContainerRef: ViewContainerRef,
    private componentFactoryResolver: ComponentFactoryResolver
  ) {}

  createComponent() {
    const factory = this.componentFactoryResolver.resolveComponentFactory(DynamicComponent);
    this.viewContainerRef.createComponent(factory);
  }
}

@Component({
  selector: 'app-dynamic',
  template: '<p>Dynamic Component</p>'
})
export class DynamicComponent {}
```
In the code above, the `createComponent` method uses the `ViewContainerRef` and `ComponentFactoryResolver` to dynamically create and render the `DynamicComponent`. Angular then uses the renderer to add the component to the DOM. 


---
## Q. Creating a custom directive in Angular.
Creating a custom directive in Angular involves defining a class with the `@Directive` decorator and implementing the desired logic. Here's a step-by-step guide: 

- **Generate the Directive**: Use the Angular CLI to generate the directive files: 
```
ng generate directive my-directive
```
This command creates two files: `my-directive.directive.ts` and `my-directive.directive.spec.ts`. 

- **Implement the Directive Logic**: Open the `my-directive.directive.ts` file and add the following code: 
```typescript
import { Directive, ElementRef, HostListener, Input } from '@angular/core';

@Directive({
  selector: '[appMyDirective]'
})
export class MyDirectiveDirective {
  @Input('appMyDirective') highlightColor: string = 'yellow';

  constructor(private el: ElementRef) {}

  @HostListener('mouseenter') onMouseEnter() {
    this.highlight(this.highlightColor);
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.highlight('');
  }

  private highlight(color: string) {
    this.el.nativeElement.style.backgroundColor = color;
  }
}
```

- `@Directive` decorator defines the directive and its selector ([appMyDirective]). 
- `@Input` allows passing a value to the directive. 
- `ElementRef` provides access to the DOM element. 
- `@HostListener` listens for events on the host element. 

- **Use the Directive**: In your component's HTML file, add the directive to an element: 
```html
<p appMyDirective="lightblue">Hover over this text to see the highlight effect.</p>
<p appMyDirective="pink">This text will highlight in pink on hover.</p>
```

The directive will highlight the element when the user hovers over it. 

- **Declare the Directive**: Add the directive to the declarations array in your module (e.g., `app.module.ts`): 
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { MyDirectiveDirective } from './my-directive.directive';

@NgModule({
  declarations: [
    AppComponent,
    MyDirectiveDirective
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

---
## Q. 
Debouncing in Angular is a technique used to limit the rate at which a function is executed, particularly in response to user input events. It ensures that a function is only called after a specified delay, preventing excessive calls during rapid input changes, such as typing in a search box. 

### What is Debouncing?

- **Definition**: Debouncing is a programming pattern that delays the execution of a function until a certain amount of time has passed since the last triggering event. This is particularly useful in scenarios where rapid events can overwhelm the system or degrade user experience.

- **Use Case**: For example, in a search bar, debouncing can help execute a search query only after the user has stopped typing, rather than making multiple API calls for each keystroke.

### Benefits of Debouncing

1. **Prevent Excessive API Calls**: Reduces the number of requests sent to the server, which can help avoid overwhelming the backend and improve response times.

2. **Improve App Performance**: Minimizes resource utilization by reducing the frequency of function executions, ensuring that the application remains responsive.

3. **Enhanced User Experience**: Creates a smoother interface by reducing interruptions, allowing users to interact seamlessly with the application.

### Implementing Debouncing in Angular

To implement debouncing in Angular, you can use the `debounceTime` operator from RxJS. Here’s a step-by-step guide:

#### Step 1: Import Required Modules

```javascript
import { Component } from '@angular/core';
import { Subject } from 'rxjs';
import { debounceTime } from 'rxjs/operators';
```

#### Step 2: Create the Component

```javascript
@Component({
  selector: 'app-search',
  template: `<input (input)="onSearch($event)" placeholder="Search...">`
})
export class SearchComponent {
  private searchSubject = new Subject<string>();

  constructor() {
    this.searchSubject.pipe(debounceTime(300)).subscribe(query => {
      this.search(query);
    });
  }

  onSearch(event: Event): void {
    const query = (event.target as HTMLInputElement).value;
    this.searchSubject.next(query);
  }

  search(query: string): void {
    console.log(`Searching for: ${query}`);
    // Implement API call or other logic here
  }
}
```

### Explanation of the Code

- **Subject**: A `Subject` is used to capture and emit input events as observable streams.

- **debounceTime(300)**: This operator ensures that the `search()` function is executed only if 300 milliseconds have passed since the last keystroke, filtering out rapid successive events.

- **onSearch Method**: This method captures the input event and pushes the value to the `searchSubject`.

- **search Method**: This method is where the actual search logic or API call would be implemented.

### Conclusion

Debouncing is a powerful technique in Angular that can significantly enhance the performance and usability of applications. By implementing debouncing in scenarios like search bars, you can ensure that your application remains responsive while efficiently managing user input.

---
## Q. Debouncing in Angular
Debouncing in Angular is a technique used to limit the rate at which a function is executed, particularly in response to user input events. It ensures that a function is only called after a specified delay, preventing excessive calls during rapid input changes, such as typing in a search box. 

### What is Debouncing?

- **Definition**: Debouncing is a programming pattern that delays the execution of a function until a certain amount of time has passed since the last triggering event. This is particularly useful in scenarios where rapid events can overwhelm the system or degrade user experience.

- **Use Case**: For example, in a search bar, debouncing can help execute a search query only after the user has stopped typing, rather than making multiple API calls for each keystroke.

### Benefits of Debouncing

1. **Prevent Excessive API Calls**: Reduces the number of requests sent to the server, which can help avoid overwhelming the backend and improve response times.

2. **Improve App Performance**: Minimizes resource utilization by reducing the frequency of function executions, ensuring that the application remains responsive.

3. **Enhanced User Experience**: Creates a smoother interface by reducing interruptions, allowing users to interact seamlessly with the application.

### Implementing Debouncing in Angular

To implement debouncing in Angular, you can use the `debounceTime` operator from RxJS. Here’s a step-by-step guide:

#### Step 1: Import Required Modules

```javascript
import { Component } from '@angular/core';
import { Subject } from 'rxjs';
import { debounceTime } from 'rxjs/operators';
```

#### Step 2: Create the Component

```javascript
@Component({
  selector: 'app-search',
  template: `<input (input)="onSearch($event)" placeholder="Search...">`
})
export class SearchComponent {
  private searchSubject = new Subject<string>();

  constructor() {
    this.searchSubject.pipe(debounceTime(300)).subscribe(query => {
      this.search(query);
    });
  }

  onSearch(event: Event): void {
    const query = (event.target as HTMLInputElement).value;
    this.searchSubject.next(query);
  }

  search(query: string): void {
    console.log(`Searching for: ${query}`);
    // Implement API call or other logic here
  }
}
```

### Explanation of the Code

- **Subject**: A `Subject` is used to capture and emit input events as observable streams.

- **debounceTime(300)**: This operator ensures that the `search()` function is executed only if 300 milliseconds have passed since the last keystroke, filtering out rapid successive events.

- **onSearch Method**: This method captures the input event and pushes the value to the `searchSubject`.

- **search Method**: This method is where the actual search logic or API call would be implemented.

### Conclusion

Debouncing is a powerful technique in Angular that can significantly enhance the performance and usability of applications. By implementing debouncing in scenarios like search bars, you can ensure that your application remains responsive while efficiently managing user input.

---

---
## Q. Throtteling in Angular
Throttling in Angular is a technique that limits the number of times a function can be executed over a specified time period. It ensures that a function is called at controlled intervals, making it useful for scenarios like handling scroll events or resizing, where frequent calls can lead to performance issues. 

**Key Concepts of Throttling in Angular**

- **Definition**: Throttling is a method to control the execution frequency of a function, ensuring it runs at a specified interval regardless of how often the triggering event occurs.

- **Use Cases**:
  - **Scroll Events**: When a user scrolls quickly, throttling can prevent excessive function calls that may lead to performance degradation.
  - **Resize Events**: Similar to scroll events, resizing a window can trigger multiple events rapidly, and throttling helps manage these calls efficiently.

**Implementation in Angular with RxJS**

- **Using `throttleTime`**: This operator from RxJS can be utilized to implement throttling in Angular applications. It delays the values emitted by a source for a specified duration.

- **Example Code**:
```javascript
import { fromEvent } from 'rxjs';
import { throttleTime, map } from 'rxjs/operators';

const inputElement = document.createElement('input');
document.body.appendChild(inputElement);

fromEvent(inputElement, 'input')
  .pipe(
    throttleTime(500), // Throttle input events to every 500 milliseconds
    map((event: any) => event.target.value)
  )
  .subscribe(val => console.log(val));
```

**Configuration Options**

- **Leading and Trailing**: The `throttleTime` operator can be configured with options:
  - **Leading**: Emit the first value immediately when the event occurs.
  - **Trailing**: Emit the last value after the throttle period ends.

- **Default Behavior**: By default, `throttleTime` emits the leading value and ignores subsequent values until the throttle period is over.

**Benefits of Throttling**

- **Performance Improvement**: Reduces the number of function calls, which can enhance application performance, especially during high-frequency events.
- **User  Experience**: Maintains a smooth user experience by preventing lag or jank caused by excessive function executions.

---
## Q.

---
## Q.

---
## Q.

---
## Q.

---
## Q.

---





---
## Q. **What is Angular and why is it used?**  
   Angular is a TypeScript-based frontend framework used for building dynamic single-page applications (SPAs). It offers tools for two-way binding, dependency injection, routing, and more.

## Q2. **What are components in Angular?**  
   Components are the building blocks of Angular apps. Each component has a TypeScript file, HTML template, CSS for styling, and metadata defined in a decorator.

## Q3. **Difference between Template-driven and Reactive forms?**  
   - *Template-driven*: Easy to use, suitable for simple forms. Uses directives in HTML.
   - *Reactive*: More scalable, uses explicit form model in TypeScript.

## Q4. **What is data binding in Angular?**  
   Connecting the template and the component. Types include:
   - Interpolation (`{{ }}`)
   - Property binding (`[property]`)
   - Event binding (`(event)`)
   - Two-way binding (`[(ngModel)]`)

## Q5. **What are services and dependency injection in Angular?**  
   Services hold business logic and can be injected into components using Angular’s dependency injection system.

## Q6. **What is a directive in Angular?**
   - *Structural*: Changes DOM layout (e.g. `*ngIf`, `*ngFor`)
   - *Attribute*: Changes appearance or behavior (e.g. `ngClass`, `ngStyle`)

## Q7. **What is Angular CLI and its advantages?**  
   Angular CLI automates project scaffolding, building, serving, testing, and more.

## Q8. **How does routing work in Angular?**  
   The `RouterModule` maps URLs to components using `Routes`.

## Q9. **How does change detection work in Angular?**  
   Angular’s change detection checks for component data changes and updates the DOM accordingly.

## Q10. **What is Lazy Loading in Angular?**  
    It loads modules only when required, improving performance.

## 11. **What is an observable in Angular?**  
    Part of RxJS, observables represent streams of data used for asynchronous programming.

## 12. **What is the role of `ngOnInit()`?**  
    Lifecycle hook that runs once after component initialization.

## 13. **What is the difference between BehaviorSubject and Subject?**  
    - `Subject`: No initial value, emits to current subscribers.
    - `BehaviorSubject`: Requires initial value and emits last emitted value to new subscribers.

## 14. **What is ViewChild and ContentChild in Angular?**  
    Used to get references to components/elements within the template (`ViewChild`) or projected content (`ContentChild`).

## 15. **What is a pipe? How to create custom pipes?**  
    Pipes transform data in templates. Custom pipes implement `PipeTransform`.

## 16. **How do you test Angular components and services (TDD)?**  
    Use Jasmine/Karma for unit testing, with mocks for services and Angular TestBed.

## 17. **What is AoT and JiT compilation?**  
    - AoT: Ahead-of-Time (compile during build)
    - JiT: Just-in-Time (compile during runtime)

## 18. **What is the difference between promises and observables?**  
    - Promise resolves once.  
    - Observable supports multiple values over time and operators like `map`, `filter`.

## 19. **Explain `switchMap` in RxJS.**  
    Cancels previous observable and switches to new one. Useful in search/autocomplete.

## 20. **How do you manage state in Angular apps?**  
    Use services or libraries like NgRx, Akita for centralized state management.

## 21. **What is HttpClient in Angular?**  
    Built-in service to make HTTP calls. Supports interceptors for auth/logging.

## 22. **What are Angular lifecycle hooks?**  
    Hooks like `ngOnInit`, `ngOnDestroy`, `ngAfterViewInit` let you tap into component life stages.

## 23. **How do you handle forms validation?**  
    Use `Validators` (required, minLength, pattern etc.) in template-driven or reactive forms.

## 24. **What are guards in Angular?**  
    Control navigation using `CanActivate`, `CanDeactivate`, `Resolve` etc.

## 25. **How do you optimize Angular app performance?**  
    Lazy loading, `OnPush` change detection, trackBy in `*ngFor`, reduce DOM operations.

## 26. **What is SSR in Angular?**  
    Server-Side Rendering improves SEO and initial load performance (via Angular Universal).

## 27. **How do you manage modules and shared components?**  
    Break into feature modules and use `SharedModule` for reusable components/pipes.

## 28. **How do you handle authentication in Angular?**  
    JWT tokens stored in cookies/localStorage, guarded routes, interceptors for attaching tokens.

## 29. **What is the use of `Renderer2`?**  
    Provides abstraction for DOM manipulation in a safe, platform-independent way.

## 30. **What’s your experience with Angular 8+ specific features?**  
    Includes Ivy compiler, differential loading, lazy loading with dynamic imports, etc.

## n. Best Websites to Practice JavaScript Output-Based Questions

1. **[JSitor](https://jsitor.com/)**
2. **[JSBench.me](https://jsbench.me/)**
3. **[W3Schools JavaScript Quiz](https://www.w3schools.com/js/js_quiz.asp)**
4. **[GeeksforGeeks JavaScript Quiz](https://www.geeksforgeeks.org/javascript-quiz-set-1/)**
5. **[Codewars](https://www.codewars.com/)**
6. **[Edabit](https://edabit.com/challenges)**
7. **[LeetCode JavaScript Challenges](https://leetcode.com/tag/javascript/)**
8. **[HackerRank JavaScript Challenges](https://www.hackerrank.com/domains/tutorials/10-days-of-javascript)**
9. **[Node.js Interview Questions](https://gist.github.com/paulfranco/9f88a2879b7b7d88de5d1921aef2093b)**
