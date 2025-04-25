## Basic JavaScript - Interview Answers
### Q. What are the different data types in JavaScript?
JavaScript has:
- Primitive Types: String, Number, Boolean, Undefined, Null, BigInt, and Symbol.
- Non-Primitive Type: Object (includes Arrays, Functions, etc.)

### Q. What is the difference between var, let, and const?
- var is function-scoped, can be re-declared and updated.
- let is block-scoped, cannot be re-declared but can be updated.
- const is block-scoped, cannot be re-declared or updated (though objects/arrays can be mutated).

### Q. What is hoisting in JavaScript?
Hoisting is a behavior where variable and function declarations are moved to the top of their scope before code execution.
- var is hoisted with undefined.
- let and const are hoisted but not initialized (they stay in a temporal dead zone until declared).

### Q. What are truthy and falsy values?
- Falsy values: false, 0, '', null, undefined, NaN
- Everything else is truthy (e.g., '0', [], {}, 'false', etc.)

### Q. What is the difference between == and ===?
- == compares values with type coercion.
- === compares values and types strictly (no coercion).
 ```
 2 == '2'  // true
 2 === '2' // false
 ```
### Q. What is a closure in JavaScript?
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

### Q. How does the this keyword work?
- In regular functions, this refers to the object that calls the function.
- In arrow functions, this is lexically bound (refers to this of the outer scope).
- In the global context (non-strict mode), this refers to window in browsers.

### Q. What is the difference between null and undefined?
- null: Explicitly means “no value”.
- undefined: A variable declared but not assigned a value.

### Q. What is event bubbling and event capturing?
- Bubbling: Event starts from the target element and bubbles up to the parent.
- Capturing: Event starts from the parent and goes down to the target element.
- Default behavior is bubbling.

### Q. How does the typeof operator work?
typeof is used to get the data type of a variable.
 ```
 Example:
  typeof "hello"  // "string"
  typeof 123       // "number"
  typeof undefined // "undefined"
  typeof null      // "object" (quirk in JS)
  ```

## Functions & Scope – Interview Answers
### Q. What are arrow functions and how are they different from regular functions?
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

### Q. What is a callback function?
A callback is a function passed as an argument to another function, which is then called after a task is completed.
 ```
 function greet(name, callback) {
    console.log("Hi " + name);
    callback();
 }

 greet("John", () => console.log("Callback executed"));
 ```

### Q. What is a higher-order function?
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

### Q. What is the scope of a variable in JavaScript?
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
### Q. What is the difference between function declaration and function expression?
- Function Declaration: Can be hoisted.
 ```
 function greet() {
    console.log("Hello");
 }
 ```

- Function Expression: Not hoisted. #### Stored in a variable.
 ```
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
 ```
 setTimeout(() => console.log("Once"), 1000);
 setInterval(() => console.log("Repeat"), 1000);
 ```
### Q. What are Promises and how do they work?
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

### Q. What is async/await and how does it improve asynchronous code?
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

### Q. What is the difference between microtask and macrotask queues?
- Microtasks: Include Promises (.then()), MutationObserver.
- Macrotasks: Include setTimeout, setInterval, setImmediate, and I/O.
  Microtasks are prioritized and executed before the next macrotask.

## Objects, Arrays & ES6 Features – Interview Answers
### Q. What are the different ways to clone an object in JavaScript?
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

### Q. What are destructuring assignments?
Destructuring allows you to extract values from arrays or objects into variables.

 ```
 const user = { name: "Alice", age: 25 };
 const { name, age } = user; // name = "Alice", age = 25

 const arr = [1, 2, 3];
 const [a, b] = arr; // a = 1, b = 2
 ```

### Q. What are template literals?
Template literals are string literals that allow embedded expressions using backticks (`).
```
const name = "John";
console.log(`Hello, ${name}!`); // Hello, John!
```

### Q. What is the spread operator (...) and rest parameter?
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

### Q. What is the difference between map(), filter(), and reduce() methods?
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
### Q. What is the DOM and how do you manipulate it with JavaScript?
- The DOM (Document Object Model) is a tree structure representation of the HTML document.
- JavaScript can access and manipulate it using methods like:
 ```
 document.getElementById("id");
 document.querySelector(".class");
 element.innerHTML = "new content";
 element.style.color = "red";
 ```

### Q. What are event listeners and how are they used?
- Event listeners allow you to execute code when a specific event occurs.
 ```
 const button = document.querySelector("button");
 button.addEventListener("click", () => {
    alert("Button clicked!");
 });
 ```

### Q. What is the difference between innerHTML, innerText, and textContent?
- innerHTML: Gets/sets HTML content (includes tags).
- innerText: Gets/sets visible text content (excludes hidden elements and formatting).
- textContent: Gets/sets all text content (includes hidden elements, faster than innerText).
 ```
 element.innerHTML = "<b>Bold</b>";
 element.innerText = "<b>Bold</b>";     // displays tags as text
 element.textContent = "<b>Bold</b>";   // same as above
 ```
### Q. How do you prevent default behavior in an event handler?
Use event.preventDefault() inside the event listener to prevent the default action (like form submission, link redirect).
 ```
 document.querySelector("form").addEventListener("submit", function(e) {
    e.preventDefault();
  console.log("Form submission prevented!");
 });
 ```

### Q. What is event delegation?
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
### Q. What is a prototype in JavaScript?
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

### Q. What is prototypal inheritance?
- It’s a feature in JavaScript where an object can inherit properties and methods from another object using its prototype chain.
- This is done through Object.create(), constructor functions, or ES6 class syntax.
 ```
 const parent = { greet() { console.log("Hello!"); } };
 const child = Object.create(parent);
 child.greet(); // Hello!
 ```

### Q. What is the difference between deep copy and shallow copy?
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
 ```
 console.log(a);
 var a = 10;
 ```
 _**Output:**_ undefined
 
 ```
 console.log(b);
 let b = 10;
 ```
 _**Output:**_ d is not defined
 ```
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
 ```
 console.log(1);
 await new Promise(resolve => setTimeout(resolve, 3000)); // 3 sec
 console.log(2);
 ```
---

### Q. Find Output
    let obj1 = { key: "value" };
    let obj2 = obj1;
    let obj3 = obj2;
    obj1.key = "new value";
    obj2 = { key: "another value" };
    console.log(obj1.key); 
    console.log(obj2.key); 
    console.log(obj3.key); 
    
    Output=>
    new value
    another value
    new value

---

### Q. Reverse string and remove duplicate in javascript
```
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

```
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
```
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
```
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
```
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
## Q. 

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
```
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
```
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
```
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
```
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
```
Creating a Signal:
import { signal } from '@angular/core';
const count = signal(0);
```
```
Reading a Signal: 
const currentCount = count(); // Access the value
```
```
Updating a Signal:
count.set(1); // Sets the value to 1
count.update(value => value + 1); // Increments the value
count.mutate(value => value.push(newValue)); // Mutates the value
```
```
Computed Signals: 
import { computed, signal } from '@angular/core';
const firstName = signal('John');
const lastName = signal('Doe');
const fullName = computed(() => `${firstName()} ${lastName()}`);
  
console.log(fullName()); // Output: John Doe
```
```
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
```
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
```
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
```
db.employees.aggregate([
  { $group: { _id: "$salary" } },   // Group by salary
  { $sort: { _id: -1 } },           // Sort salaries in descending order
  { $limit: N },                    // Limit to top N salaries
  { $skip: N-1 }                    // Skip (N-1) results to get the Nth
])
```

---
## Q. Service injection in Angular
Service injection in Angular can be achieved through constructor injection or by using the `@Inject` decorator or the inject() function. Here's a breakdown of the differences:

**1. Constructor Injection**
This is the most common and traditional way to inject dependencies.
_Mechanism:_ Dependencies are declared as parameters in the class constructor. Angular's dependency injection system automatically resolves and provides these dependencies when the class is instantiated.
    ```
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
```
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
```
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
```
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
```
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
```
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
```
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
```
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
## Q. TODO
- viewchild and @output
- rxjs vs ngrx
- typescript methods for filter duplicate elements in an array
- 17 features
- 19 features





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

