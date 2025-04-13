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

### Q. #### What are truthy and falsy values?
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
### Q. Handle Exception in Angular  

```typescript
@Injectable()
export class GlobalErrorHandler implements ErrorHandler {
  handleError(error: any): void {
    console.error('An error occurred:', error);
  }
}
```
---

### Q. Signal in Angular  

Signals help manage reactive state.

---

### Q. Zone.js  

Manages asynchronous operations in Angular.

---

## SwitchMap
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

## What is component in angular?
A component in Angular is a fundamental building block for creating user interfaces. It encapsulates a portion of the user interface's logic and presentation. Each component consists of three main parts:
- Template: Defines the HTML structure and layout of the component's view.
- Class: Contains the logic, data, and methods that control the component's behavior.
- Metadata: Provides information about the component, such as its selector, template, and styles.
Components are designed to be reusable and modular, promoting a structured and maintainable application architecture. They facilitate the separation of concerns, making it easier to develop, test, and update different parts of the application independently.

---

## What is template driven form vs reactive driven form.
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
- **Template-Driven Form:**  
  ```html
  <form #userForm="ngForm">
    <input type="text" name="username" ngModel required />
  </form>
  ```
- **Reactive Form:**  
  ```typescript
  userForm = new FormGroup({
    username: new FormControl('', Validators.required)
  });
  ```
**Note:** Reactive Forms are recommended for most real-world applications due to better flexibility and maintainability.

---

## What is SPA?
A **Single Page Application (SPA)** loads a single HTML page and dynamically updates content **without full page reloads**. It improves performance and user experience by using **JavaScript frameworks (Angular, React, Vue)** to handle UI updates and fetch data via APIs.  

### **Key Features:**  
- Faster navigation, no flickering.  
- Uses **AJAX/REST API/GraphQL** for data fetching.  
- Examples: **Gmail, Facebook, Google Maps**.  

🔹 **Efficient but needs SEO optimization & initial load handling.**

---

## How Angular works?
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
##  nth Highest salary
#### Approach 1: 
	SELECT DISTINCT salary 
	FROM employees 
	ORDER BY salary DESC 
	LIMIT 1 OFFSET N-1;

#### In MongoDB:
db.employees.aggregate([
  { $group: { _id: "$salary" } },   // Group by salary
  { $sort: { _id: -1 } },           // Sort salaries in descending order
  { $limit: N },                    // Limit to top N salaries
  { $skip: N-1 }                    // Skip (N-1) results to get the Nth
])
