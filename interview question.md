# Angular, Java & Spring Boot Interview Questions  

## 1. Difference Between Parallelism and Concurrency  

| S.NO | Concurrency | Parallelism |
|:----:|:-------------------------------------------------------------------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------:|
|  1.  | Concurrency is the task of running and managing multiple computations at the same time. | Parallelism is the task of running multiple computations simultaneously. |
|  2.  | Concurrency is achieved through interleaving operations of processes on the CPU or by context switching. | Parallelism is achieved through multiple CPUs. |
|  3.  | Concurrency can be done using a single processing unit. | Parallelism requires multiple processing units. |
|  4.  | Concurrency increases the amount of work finished at a time. | Parallelism improves throughput and computational speed. |
|  5.  | Concurrency deals with many tasks simultaneously. | Parallelism does many things simultaneously. |
|  6.  | Concurrency follows a non-deterministic control flow. | Parallelism follows a deterministic control flow. |
|  7.  | Debugging concurrency issues is very hard. | Debugging parallelism is also hard but simpler than concurrency. |

## 2. List vs Set  

| S.NO | List | Set |
|:----:|:-----------------------------------------:|:-------------------------------------------:|
|  1.  | Allows duplicate elements | Does not allow duplicate elements |
|  2.  | Elements are ordered (insertion order) | Elements are unordered (HashSet) or ordered (TreeSet) |
|  3.  | Allows multiple null values | Allows only one null value |
|  4.  | Access elements by index | No index-based access |
|  5.  | Implementations: ArrayList, LinkedList | Implementations: HashSet, TreeSet, LinkedHashSet |

## 3. Creating an Immutable Class in Java  

```java
public final class ImmutableExample {
    private final String name;
    private final int age;

    public ImmutableExample(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

## 4. Validation in Spring Boot  

Spring Boot provides `javax.validation` and `Spring Validator` for validation.

Example using `@Valid`:

```java
public class User {
    @NotBlank
    private String name;
    
    @Email
    private String email;
}
```

In a Controller:

```java
@PostMapping("/users")
public ResponseEntity<String> addUser(@Valid @RequestBody User user, BindingResult result) {
    if (result.hasErrors()) {
        return ResponseEntity.badRequest().body("Invalid data");
    }
    return ResponseEntity.ok("User added");
}
```

## 5. Questions on Stream API  

Examples:

```java
List<Integer> evenNumbers = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());

List<String> stringList = numbers.stream()
    .map(String::valueOf)
    .collect(Collectors.toList());
```

## 6. Functional Interface  

A **functional interface** has exactly one abstract method.

```java
@FunctionalInterface
interface MyFunction {
    void sayHello();
}
```

## 7. SOLID Principles  

1. **Single Responsibility** - A class should have only one reason to change.  
2. **Open/Closed** - Open for extension, closed for modification.  
3. **Liskov Substitution** - Subtypes must be substitutable for base types.  
4. **Interface Segregation** - Prefer multiple small interfaces.  
5. **Dependency Inversion** - Depend on abstractions, not concretions.  

## 8. Difference Between Hibernate and JDBC  

| Feature | Hibernate | JDBC |
|---------|----------|------|
| ORM | Yes | No |
| Query Language | HQL | SQL |
| Caching | Yes | No |
| Lazy Loading | Yes | No |
| Database Independence | Yes | No |

## 9. Annotations Used in Java  

- `@Override`
- `@FunctionalInterface`
- `@Deprecated`
- `@SpringBootApplication`
- `@RestController`

## 10. Find Longest Substring Without Repeating Characters  

```java
public int lengthOfLongestSubstring(String s) {
    Set<Character> set = new HashSet<>();
    int maxLength = 0, left = 0;

    for (int right = 0; right < s.length(); right++) {
        while (set.contains(s.charAt(right))) {
            set.remove(s.charAt(left));
            left++;
        }
        set.add(s.charAt(right));
        maxLength = Math.max(maxLength, right - left + 1);
    }
    return maxLength;
}
```

## 11. Technical Architecture  

Spring Boot follows **Microservices architecture** and includes:
- **Controller Layer** - API Handling
- **Service Layer** - Business Logic
- **Repository Layer** - Database Interaction  

## 12. SQL vs NoSQL  

| SQL | NoSQL |
|-----|-------|
| Structured | Unstructured |
| Fixed Schema | Dynamic Schema |
| ACID | BASE |

## 13. Factory Design Pattern  

```java
class Factory {
    static Car getCar(String type) {
        if (type.equals("Sedan")) return new Sedan();
        else return new SUV();
    }
}
```

## 14. Algorithm Behind `Collections.sort()`  

It uses **TimSort**, which is a hybrid of **MergeSort and InsertionSort**.

## 15. Challenges Faced as an Engineer  

- **Performance Issues** → Optimized SQL Queries  
- **Scalability** → Used Caching Mechanisms  

## 16. How JVM Works?  

JVM Components:
- **Class Loader**
- **Heap Memory**
- **Execution Engine**
- **Garbage Collector**

## 17. Spring Actuator  

It provides health checks, metrics, and monitoring.

Enable Actuator:

```yaml
management:
  endpoints:
    web:
      exposure:
        include: "*"
```

## 18. Abstract Class vs Interface  

| Abstract Class | Interface |
|---------------|----------|
| Can have method implementations | Only method signatures (before Java 8) |
| Can have constructors | Cannot have constructors |

## 19. Understanding Browser Caching  

- **Cache-Control: max-age=3600**  
- **ETag for validation**  

## 20. UX Design Principles  

- Simplicity  
- Consistency  
- Accessibility  

## 21. Event-Driven Implementation Using Kafka  

- **Producer** sends message to **Kafka Topic**  
- **Consumer** reads message from topic  

## 22. HTML5 & CSS  

- **HTML5** → Semantic tags (`<article>`, `<section>`)  
- **CSS** → Flexbox, Grid, Animations  

## 23. Angular 17 Features  

- Improved Hydration  
- Signal-based reactivity  

## 24. Lazy Loading in Hibernate  

```java
@OneToMany(fetch = FetchType.LAZY)
private List<Order> orders;
```

## 25. Reverse a String  

```java
String reversed = new StringBuilder(str).reverse().toString();
```

## 26. Handle Exception in Angular  

```typescript
@Injectable()
export class GlobalErrorHandler implements ErrorHandler {
  handleError(error: any): void {
    console.error('An error occurred:', error);
  }
}
```

## 27. Signal in Angular  

Signals help manage reactive state.

## 28. Zone.js  

Manages asynchronous operations in Angular.

## 29. Second Highest Salary in SQL  

```sql
SELECT salary FROM employees ORDER BY salary DESC LIMIT 1 OFFSET 1;
```

## 30. Shift an Array by 3 to the Right  

```java
public static void rotateRight(int[] arr, int k) {
    Collections.rotate(Arrays.asList(arr), k);
}
```

## 31. Stream API in Java  

Used for processing collections efficiently.

## 32. First Repeating Character in a String  

```java
public static Optional<Character> findFirstRepeatedCharacter(String input) {
    Set<Character> seen = new HashSet<>();
    return input.chars().mapToObj(c -> (char) c).filter(c -> !seen.add(c)).findFirst();
}
```

## 33. Find Employees Who Are Managers  

```sql
SELECT e1.name FROM emp e1 JOIN emp e2 ON e1.emp_id = e2.emp_mgr_id;
```

---

## 34. Common HTTP Status Codes

- **200**: OK  
- **201**: Created  
- **403**: Forbidden  
- **500**: Internal Server Error  
- **502**: Bad Gateway  

---

## 35. Output
let obj1 = { key: "value" };
let obj2 = obj1;
let obj3 = obj2;
obj1.key = "new value";
obj2 = { key: "another value" };
console.log(obj1.key); 
console.log(obj2.key); 
console.log(obj3.key); 

**Output**=> new value
another value
new value

## 36. Reverse string and remove duplicate in javascript
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

## 37. SwitchMap

---
## 38. What is component in angular?
A component in Angular is a fundamental building block for creating user interfaces. It encapsulates a portion of the user interface's logic and presentation. Each component consists of three main parts:
 - Template: Defines the HTML structure and layout of the component's view.
- Class: Contains the logic, data, and methods that control the component's behavior.
- Metadata: Provides information about the component, such as its selector, template, and styles.
Components are designed to be reusable and modular, promoting a structured and maintainable application architecture. They facilitate the separation of concerns, making it easier to develop, test, and update different parts of the application independently.

---

## 39. What is template driven form vs reactive driven form.

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

## 40. What is SPA?
A **Single Page Application (SPA)** loads a single HTML page and dynamically updates content **without full page reloads**. It improves performance and user experience by using **JavaScript frameworks (Angular, React, Vue)** to handle UI updates and fetch data via APIs.  

### **Key Features:**  
- Faster navigation, no flickering.  
- Uses **AJAX/REST API/GraphQL** for data fetching.  
- Examples: **Gmail, Facebook, Google Maps**.  

🔹 **Efficient but needs SEO optimization & initial load handling.**

---

## 41. How Angular works?
Angular is a **component-based** frontend framework that uses **TypeScript**. It follows the **MVC** pattern and works by:  

1. **Bootstrapping** – Loads the root module (`AppModule`) and component (`AppComponent`).  
2. **Templates & Data Binding** – Uses **HTML templates** and **binding** (`{{ }}`) to display dynamic data.  
3. **Directives & Components** – Components control the UI, while directives add behavior.  
4. **Dependency Injection** – Services are injected into components for reusability.  
5. **Routing** – `RouterModule` enables navigation between pages.  
6. **Change Detection** – Updates the DOM when data changes, using **Zone.js**.  
7. **RxJS & Observables** – Handles async data streams efficiently.
8. **Compilation & Optimization** –
    Ahead-of-Time (AOT) Compilation improves performance.
    Lazy Loading loads modules only when needed, optimizing performance.  

---


## n. Best Websites to Practice JavaScript Output-Based Questions

1. **[JSitor](https://jsitor.com/)**
2. **[JSBench.me](https://jsbench.me/)**
3. **[W3Schools JavaScript Quiz](https://www.w3schools.com/js/js_quiz.asp)**
4. **[GeeksforGeeks JavaScript Quiz](https://www.geeksforgeeks.org/javascript-quiz-set-1/)**
5. **[Codewars](https://www.codewars.com/)**
6. **[Edabit](https://edabit.com/challenges)**
7. **[LeetCode JavaScript Challenges](https://leetcode.com/tag/javascript/)**
8. **[HackerRank JavaScript Challenges](https://www.hackerrank.com/domains/tutorials/10-days-of-javascript)**

---

Would you like any further refinements or additional topics? 🚀
