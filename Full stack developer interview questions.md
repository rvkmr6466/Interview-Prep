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

---

## 2. List vs Set  

| S.NO | List | Set |
|:----:|:-----------------------------------------:|:-------------------------------------------:|
|  1.  | Allows duplicate elements | Does not allow duplicate elements |
|  2.  | Elements are ordered (insertion order) | Elements are unordered (HashSet) or ordered (TreeSet) |
|  3.  | Allows multiple null values | Allows only one null value |
|  4.  | Access elements by index | No index-based access |
|  5.  | Implementations: ArrayList, LinkedList | Implementations: HashSet, TreeSet, LinkedHashSet |

---

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

---

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

---

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

---

## 6. Functional Interface  

A **functional interface** has exactly one abstract method.

```java
@FunctionalInterface
interface MyFunction {
    void sayHello();
}
```

---

## 7. SOLID Principles  

1. **Single Responsibility** - A class should have only one reason to change.  
2. **Open/Closed** - Open for extension, closed for modification.  
3. **Liskov Substitution** - Subtypes must be substitutable for base types.  
4. **Interface Segregation** - Prefer multiple small interfaces.  
5. **Dependency Inversion** - Depend on abstractions, not concretions.  

---

## 8. Difference Between Hibernate and JDBC  

| Feature | Hibernate | JDBC |
|---------|----------|------|
| ORM | Yes | No |
| Query Language | HQL | SQL |
| Caching | Yes | No |
| Lazy Loading | Yes | No |
| Database Independence | Yes | No |

---

## 9. Annotations Used in Java  

- `@Override`
- `@FunctionalInterface`
- `@Deprecated`
- `@SpringBootApplication`
- `@RestController`

---

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

---

## 11. Technical Architecture  

Spring Boot follows **Microservices architecture** and includes:
- **Controller Layer** - API Handling
- **Service Layer** - Business Logic
- **Repository Layer** - Database Interaction  

---

## 12. SQL vs NoSQL  

| SQL | NoSQL |
|-----|-------|
| Structured | Unstructured |
| Fixed Schema | Dynamic Schema |
| ACID | BASE |

---

## 13. Factory Design Pattern  

```java
class Factory {
    static Car getCar(String type) {
        if (type.equals("Sedan")) return new Sedan();
        else return new SUV();
    }
}
```

---

## 14. Algorithm Behind `Collections.sort()`  

It uses **TimSort**, which is a hybrid of **MergeSort and InsertionSort**.

---

## 15. Challenges Faced as an Engineer  

- **Performance Issues** → Optimized SQL Queries  
- **Scalability** → Used Caching Mechanisms  

---

## 16. How JVM Works?  

JVM Components:
- **Class Loader**
- **Heap Memory**
- **Execution Engine**
- **Garbage Collector**

---

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

---

## 18. Abstract Class vs Interface  

| Abstract Class | Interface |
|---------------|----------|
| Can have method implementations | Only method signatures (before Java 8) |
| Can have constructors | Cannot have constructors |

---

## 19. Understanding Browser Caching  

- **Cache-Control: max-age=3600**  
- **ETag for validation**  

---

## 20. UX Design Principles  

- Simplicity  
- Consistency  
- Accessibility  

---

## 21. Event-Driven Implementation Using Kafka  

- **Producer** sends message to **Kafka Topic**  
- **Consumer** reads message from topic  

---

## 22. HTML5 & CSS  

- **HTML5** → Semantic tags (`<article>`, `<section>`)  
- **CSS** → Flexbox, Grid, Animations  

---

## 23. Angular 17 Features  

- Improved Hydration  
- Signal-based reactivity  

---

## 24. Lazy Loading in Hibernate  

```java
@OneToMany(fetch = FetchType.LAZY)
private List<Order> orders;
```

---

## 25. Reverse a String  

```java
String reversed = new StringBuilder(str).reverse().toString();
```

---

## 26. Handle Exception in Angular  

```typescript
@Injectable()
export class GlobalErrorHandler implements ErrorHandler {
  handleError(error: any): void {
    console.error('An error occurred:', error);
  }
}
```

---

## 27. Signal in Angular  

Signals help manage reactive state.

---

## 28. Zone.js  

Manages asynchronous operations in Angular.

---

## 29. Second Highest Salary in SQL  

```sql
SELECT salary FROM employees ORDER BY salary DESC LIMIT 1 OFFSET 1;
```

---

## 30. Shift an Array by 3 to the Right  

```java
public static void rotateRight(int[] arr, int k) {
    Collections.rotate(Arrays.asList(arr), k);
}
```

---

## 31. Stream API in Java  
Used for processing collections efficiently.

---

## 32. First Repeating Character in a String  

```java
public static Optional<Character> findFirstRepeatedCharacter(String input) {
    Set<Character> seen = new HashSet<>();
    return input.chars().mapToObj(c -> (char) c).filter(c -> !seen.add(c)).findFirst();
}
```

---

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
    
    Output=>
    new value
    another value
    new value

## 36. Reverse string and remove duplicate in javascript
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

## 37. SwitchMap
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
8. **Compilation & Optimization**
    1. Ahead-of-Time (AOT) Compilation improves performance.
    2. Lazy Loading loads modules only when needed, optimizing performance.  

---

## 42. Block vs Inline vs Inline-Block in CSS

| Property      | Block | Inline | Inline-Block |
|--------------|-------|--------|--------------|
| **Starts on a new line?** | ✅ Yes | ❌ No | ❌ No |
| **Takes full width?** | ✅ Yes (by default) | ❌ No (only as wide as content) | ❌ No (only as wide as content) |
| **Supports width & height?** | ✅ Yes | ❌ No | ✅ Yes |
| **Supports margin & padding?** | ✅ Yes (all sides) | 🚫 No (only horizontal) | ✅ Yes (all sides) |


### **Examples for Better Understanding**  

#### **1️⃣ Block Elements (`display: block`)**  
✅ Takes the full width, starts on a new line  
📌 Examples: `<div>`, `<p>`, `<h1>`, `<section>`

```html
<div style="background: lightblue; width: 300px;">I am a block element</div>
<p style="background: lightcoral;">I also take full width</p>
```

#### **2️⃣ Inline Elements (`display: inline`)**  
✅ Stays in line, only takes up as much space as needed  
📌 Examples: `<span>`, `<a>`, `<strong>`

```html
<span style="background: yellow;">I am inline</span>
<a href="#" style="background: orange;">I am also inline</a>
```

#### **3️⃣ Inline-Block Elements (`display: inline-block`)**  
✅ Stays in line **but** supports width & height  
📌 Examples: `<button>`, `<input>`, custom `<span>` styling  

```html
<span style="display: inline-block; width: 150px; background: lightgreen;">I have width & height</span>
<button style="display: inline-block; width: 100px;">Button</button>
```

### **Visual Representation**
```
[BLOCK]          (Takes full width)
[BLOCK]

[INLINE] [INLINE] [INLINE]   (Stays in line)

[INLINE-BLOCK] [INLINE-BLOCK]   (Stays in line but supports width)
```

### **When to Use?**
- **Use `block`** for sections, divs, and paragraphs.
- **Use `inline`** for text elements that should flow naturally (like links & spans).
- **Use `inline-block`** when you need inline elements but want to set width & height.

---

## 43. Class level annotation in spring boot
In Spring Boot, class-level annotations are used to define configurations, components, and behaviors at the class level. Here are some commonly used class-level annotations:

### 1. **[@RestController](w)**
   - Used in Spring MVC to define a RESTful controller.
   ```java
   @RestController
   public class MyController {
       @GetMapping("/hello")
       public String hello() {
           return "Hello, World!";
       }
   }
   ```

### 2. **[@Controller](w)**
   - Marks a class as a Spring MVC controller (typically used with views like Thymeleaf).
   ```java
   @Controller
   public class MyController {
       @GetMapping("/home")
       public String home() {
           return "home";
       }
   }
   ```

### 3. **[@Service](w)**
   - Marks a class as a service component in the business layer.
   ```java
   @Service
   public class MyService {
       public String process() {
           return "Processing data";
       }
   }
   ```

### 4. **[@Repository](w)**
   - Indicates a DAO (Data Access Object) and enables exception translation.
   ```java
   @Repository
   public class MyRepository {
       // Data access logic
   }
   ```

### 5. **[@Component](w)**
   - Generic stereotype for any Spring-managed component.
   ```java
   @Component
   public class MyComponent {
       public void execute() {
           System.out.println("Executing component logic");
       }
   }
   ```

### 6. **[@Configuration](w)**
   - Marks a class as a source of Spring bean definitions.
   ```java
   @Configuration
   public class AppConfig {
       @Bean
       public MyService myService() {
           return new MyService();
       }
   }
   ```

### 7. **[@SpringBootApplication](w)**
   - Combination of `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`.
   ```java
   @SpringBootApplication
   public class MyApplication {
       public static void main(String[] args) {
           SpringApplication.run(MyApplication.class, args);
       }
   }
   ```

### 8. **[@EnableScheduling](w)**
   - Enables scheduling for running scheduled tasks.
   ```java
   @Configuration
   @EnableScheduling
   public class SchedulerConfig {
   }
   ```

These annotations help configure and organize a Spring Boot application efficiently.

## 44. PUT vs PATCH in REST APIs

Both **PATCH** and **PUT** are HTTP methods used to update resources, but they have key differences:

| Feature  | **PUT** | **PATCH** |
|----------|--------|-----------|
| **Purpose** | Replaces the entire resource with a new one | Partially updates specific fields of a resource |
| **Request Body** | Contains the full resource, even unchanged fields | Contains only the fields that need to be updated |
| **Idempotency** | Yes (multiple identical requests produce the same result) | Not necessarily (repeated requests may change the resource differently) |
| **Use Case** | Updating an entire object (e.g., replacing a user profile) | Modifying specific attributes (e.g., changing just the email) |

### **Example**
#### **PUT Request (Full Update)**
```http
PUT /users/1
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "age": 30
}
```
- Requires sending all fields, even if only one needs updating.

#### **PATCH Request (Partial Update)**
```http
PATCH /users/1
Content-Type: application/json

{
  "email": "john.doe@example.com"
}
```
- Updates only the `email` field while keeping other fields unchanged.

### **When to Use What?**
- Use **PUT** when replacing the entire resource.
- Use **PATCH** when modifying only specific attributes.

**PATCH is more efficient** when updating a small part of a resource.

## 45. Second highest element in an Array
    public static void main(String[] args) {
        int[] arr = {21, 2, 43, 114, 45, 6, 32, 54};

        if (arr.length < 2) {
            System.out.println("Array should have at least two elements.");
            return;
        }

        int firstHighest = Integer.MIN_VALUE;
        int secondHighest = Integer.MIN_VALUE;

        for (int n : arr) {
            if (n > firstHighest) {
                secondHighest = firstHighest; // Update secondHighest before changing firstHighest
                firstHighest = n;
            } else if (n > secondHighest && n < firstHighest) {
                secondHighest = n;
            }
        }

        if (secondHighest == Integer.MIN_VALUE) {
            System.out.println("No second highest element found.");
        } else {
            System.out.println("First Highest: " + firstHighest);
            System.out.println("Second Highest: " + secondHighest);
        }
        
    }

**Using Stream API**

    public static void main(String[] args) {
        int[] arr = {21, 2, 43, 114, 45, 6, 32, 54};
        Optional<Integer> secondHighest = Arrays.stream(arr)
                .distinct() // Remove duplicates
                .boxed() // Convert to Integer for sorting
                .sorted((a, b) -> b - a) // Sort in descending order
                .skip(1) // Skip the highest element
                .findFirst(); // Get the second highest

        if (secondHighest.isPresent()) {
            System.out.println("Second Highest: " + secondHighest.get());
        } else {
            System.out.println("No second highest element found.");
        }
    }

---

## 46. Stream vs Parallelstream
In Java, both `stream()` and `parallelStream()` are methods used to create streams from collections, but they have different execution models.

- `stream()`: Creates a sequential stream that processes elements one at a time in a single thread.
- `parallelStream()`: Creates a parallel stream that can process elements concurrently using multiple threads, potentially improving performance for large datasets.

Here is an example demonstrating the difference:

    import java.util.Arrays;
    import java.util.List;
    
    public class Main {
        public static void main(String[] args) {
            List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    
            // Sequential stream
            numbers.stream()
                    .forEach(n -> System.out.println("Sequential: " + n));
    
            // Parallel stream
            numbers.parallelStream()
                    .forEach(n -> System.out.println("Parallel: " + n));
        }
    }

In this example, the `stream()` method processes the elements sequentially, while the `parallelStream()` method processes the elements in parallel, potentially out of order.

**Note**: if I have 1 lakh records then which should use

For processing a large dataset like 1 lakh records, you should consider using `parallelStream()` as it can leverage multiple threads to process the elements concurrently, potentially improving performance.

Here is an example:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Main {
    public static void main(String[] args) {
        // Generate a list of 1 lakh integers
        List<Integer> numbers = IntStream.rangeClosed(1, 100000).boxed().collect(Collectors.toList());

        // Using parallelStream to process the list
        List<Integer> processedNumbers = numbers.parallelStream()
                .map(n -> n * 2) // Example processing: multiply each number by 2
                .collect(Collectors.toList());

        System.out.println("Processed " + processedNumbers.size() + " records.");
    }
}
```

This code demonstrates how to use `parallelStream()` to process a large list of integers concurrently.

## 47. Sort a HashMap on the basis of key
```java
import java.util.*;

public class HashMapSorting {
    public static void main(String[] args) {
        // Creating a HashMap
        HashMap<Integer, String> map = new HashMap<>();
        map.put(3, "Three");
        map.put(1, "One");
        map.put(4, "Four");
        map.put(2, "Two");

        // Sorting using TreeMap (keys will be sorted)
        TreeMap<Integer, String> sortedMap = new TreeMap<>(map);

        // Printing sorted map
        for (Map.Entry<Integer, String> entry : sortedMap.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}

```
**Alternative**: Using Stream API
```java
import java.util.*;
import java.util.stream.Collectors;

public class HashMapSorting {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(3, "Three");
        map.put(1, "One");
        map.put(4, "Four");
        map.put(2, "Two");

        // Sorting using Stream and LinkedHashMap to maintain order
        Map<Integer, String> sortedMap = map.entrySet().stream()
            .sorted(Map.Entry.comparingByKey())
            .collect(Collectors.toMap(
                Map.Entry::getKey, 
                Map.Entry::getValue, 
                (e1, e2) -> e1, LinkedHashMap::new));

        // Printing sorted map
        sortedMap.forEach((key, value) -> System.out.println(key + " -> " + value));
    }
}
```
**One more Alternative**: List and Collections.sort() method
```java
import java.util.*;

public class HashMapSorting {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("Three", 3);
        map.put("One", 1);
        map.put("Four", 4);
        map.put("Two", 2);

        // Step 1: Get the keys and store them in a List
        ArrayList<String> keys = new ArrayList<>(map.keySet());

        // Step 2: Sort the List
        Collections.sort(keys);

        // Step 3: Print the sorted keys with values
        for (String key : keys) {
            System.out.println(key + " -> " + map.get(key));
        }
    }
}

**Output:**
Four -> 4
One -> 1
Three -> 3
Two -> 2
```

## 48. How to Use Caching in Spring Boot
Spring Boot provides built-in support for caching using the **Spring Cache Abstraction**. This allows caching data in memory or using external cache providers like **Redis**, **EhCache**, and **Caffeine**.

---

### **1. Enable Caching in Spring Boot**
First, enable caching in your Spring Boot application by adding the `@EnableCaching` annotation in your main class or a configuration class.

```java
import org.springframework.cache.annotation.EnableCaching;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
@EnableCaching  // Enables caching in the application
public class CachingExampleApplication {
    public static void main(String[] args) {
        SpringApplication.run(CachingExampleApplication.class, args);
    }
}
```

### **2. Use @Cacheable Annotation**
You can use `@Cacheable` to cache method results so that subsequent calls with the same arguments return the cached result instead of executing the method again.

#### **Example: Caching a Method Result**
```java
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @Cacheable("users") // Caches the result under "users"
    public String getUserById(int userId) {
        System.out.println("Fetching from database...");
        return "User_" + userId;
    }
}
```
#### **How It Works:**
1. The first time `getUserById(1)` is called, it fetches data and stores it in the cache.
2. The next time `getUserById(1)` is called, it returns the cached result instead of executing the method.


### **3. Clear Cache with @CacheEvict**
If data changes and you need to remove it from the cache, use `@CacheEvict`.

```java
import org.springframework.cache.annotation.CacheEvict;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @CacheEvict(value = "users", allEntries = true) // Clears the "users" cache
    public void clearUsersCache() {
        System.out.println("Users cache cleared.");
    }
}
```
- `allEntries = true` clears all cached entries under "users".
- `@CacheEvict(value = "users", key = "#userId")` clears a specific entry.


### **4. Update Cache with @CachePut**
Use `@CachePut` to update the cache when a method is called.

```java
import org.springframework.cache.annotation.CachePut;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @CachePut(value = "users", key = "#userId") // Updates the cache
    public String updateUser(int userId) {
        System.out.println("Updating user in database...");
        return "Updated_User_" + userId;
    }
}
```


### **5. Configure Cache in application.properties**
Spring Boot uses **ConcurrentHashMap** as the default cache. You can configure other cache providers like **EhCache, Redis, or Caffeine**.

#### **For Simple In-Memory Cache:**
```properties
spring.cache.type=simple
```

#### **For Redis Cache:**
```properties
spring.cache.type=redis
spring.redis.host=localhost
spring.redis.port=6379
```


### **6. Example with Redis Cache**
If you want to use Redis as a cache, add the following dependency in `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

Then, define a RedisCacheConfiguration:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.cache.RedisCacheConfiguration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.cache.RedisCacheManager;

import java.time.Duration;

@Configuration
public class RedisConfig {

    @Bean
    public RedisCacheManager cacheManager(RedisConnectionFactory connectionFactory) {
        RedisCacheConfiguration config = RedisCacheConfiguration.defaultCacheConfig()
                .entryTtl(Duration.ofMinutes(10)); // Cache expiry time
        return RedisCacheManager.builder(connectionFactory).cacheDefaults(config).build();
    }
}
```


### **Conclusion**
Spring Boot provides simple caching mechanisms using annotations. The best caching approach depends on your use case:

- **For small applications** → Use default simple cache (`ConcurrentHashMap`).
- **For distributed caching** → Use **Redis**.
- **For advanced caching** → Use **EhCache, Caffeine, or Hazelcast**.

---

## 49. ConcurrentModificationException in Java
The `ConcurrentModificationException` occurs when a collection (like `ArrayList`, `HashMap`, etc.) is modified while iterating over it using an **iterator** or **enhanced for loop**.

### **Example Scenario:**
```java
import java.util.*;

public class ConcurrentModificationExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");

        // Iterating using enhanced for loop (causes ConcurrentModificationException)
        for (String s : list) {
            if (s.equals("B")) {
                list.remove(s); // Modifying the list while iterating
            }
        }

        System.out.println(list);
    }
}
```
### **Output:**
```
Exception in thread "main" java.util.ConcurrentModificationException
```

### **Ways to Avoid ConcurrentModificationException**
#### **1. Use Iterator’s remove() Method**
Instead of modifying the list directly, use `Iterator.remove()`.
```java
import java.util.*;

public class FixWithIterator {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");

        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            String s = iterator.next();
            if (s.equals("B")) {
                iterator.remove(); // Safe removal
            }
        }

        System.out.println(list); // Output: [A, C]
    }
}
```

#### **2. Use `CopyOnWriteArrayList` (Thread-Safe)**
`CopyOnWriteArrayList` creates a copy of the list whenever modified, avoiding modification issues.
```java
import java.util.concurrent.CopyOnWriteArrayList;

public class FixWithCopyOnWriteArrayList {
    public static void main(String[] args) {
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");

        for (String s : list) {
            if (s.equals("B")) {
                list.remove(s); // No ConcurrentModificationException
            }
        }

        System.out.println(list); // Output: [A, C]
    }
}
```

#### **3. Use `removeIf()` Method (Java 8+)**
Java 8 introduced `removeIf()`, which removes elements safely while iterating.
```java
import java.util.*;

public class FixWithRemoveIf {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");

        list.removeIf(s -> s.equals("B")); // No exception

        System.out.println(list); // Output: [A, C]
    }
}
```

#### **4. Use `Stream API` for Filtering (Java 8+)**
Instead of modifying a list during iteration, create a new list with filtered values.
```java
import java.util.*;
import java.util.stream.Collectors;

public class FixWithStreams {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");

        // Create a new list without "B"
        list = list.stream()
                   .filter(s -> !s.equals("B"))
                   .collect(Collectors.toList());

        System.out.println(list); // Output: [A, C]
    }
}
```

#### **Conclusion**
| Approach | Safe? | Best For |
|----------|------|---------|
| `Iterator.remove()` | ✅ Yes | Single-threaded list modification |
| `CopyOnWriteArrayList` | ✅ Yes | Multi-threaded environments |
| `removeIf()` | ✅ Yes | Simple removals (Java 8+) |
| `Stream API` | ✅ Yes | Functional-style filtering |

Would you like a deeper explanation of any approach? 🚀

## 50. Thread Communication in Java
Threads in Java communicate with each other mainly using **wait(), notify(), and notifyAll()**, which are part of the `Object` class. This is commonly used for **inter-thread synchronization**.


### **1. Using wait() and notify()**
- `wait()`: Causes the current thread to wait until another thread calls `notify()` or `notifyAll()`.
- `notify()`: Wakes up one thread that is waiting on the same object's monitor.
- `notifyAll()`: Wakes up all threads waiting on the object's monitor.

### **Example: Producer-Consumer Problem**
```java
class SharedResource {
    private int data;
    private boolean available = false;

    public synchronized void produce(int value) {
        while (available) { // Wait if data is already produced
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        data = value;
        System.out.println("Produced: " + data);
        available = true;
        notify(); // Notify the consumer
    }

    public synchronized void consume() {
        while (!available) { // Wait if no data is available
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("Consumed: " + data);
        available = false;
        notify(); // Notify the producer
    }
}

class Producer extends Thread {
    private SharedResource resource;

    public Producer(SharedResource resource) {
        this.resource = resource;
    }

    public void run() {
        for (int i = 1; i <= 5; i++) {
            resource.produce(i);
        }
    }
}

class Consumer extends Thread {
    private SharedResource resource;

    public Consumer(SharedResource resource) {
        this.resource = resource;
    }

    public void run() {
        for (int i = 1; i <= 5; i++) {
            resource.consume();
        }
    }
}

public class ThreadCommunicationExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();
        Producer producer = new Producer(resource);
        Consumer consumer = new Consumer(resource);

        producer.start();
        consumer.start();
    }
}
```
### **Output (Order may vary)**
```
Produced: 1
Consumed: 1
Produced: 2
Consumed: 2
Produced: 3
Consumed: 3
Produced: 4
Consumed: 4
Produced: 5
Consumed: 5
```
### **Explanation**
1. The **producer** produces data and calls `notify()` to wake up the consumer.
2. The **consumer** waits using `wait()` until the producer notifies it.
3. This continues until all elements are processed.



## **2. Using Locks and Condition (Better than wait/notify)**
Java `Lock` and `Condition` provide a more flexible way for thread communication.

### **Example: Using `ReentrantLock` and `Condition`**
```java
import java.util.concurrent.locks.*;

class SharedResource {
    private int data;
    private boolean available = false;
    private final Lock lock = new ReentrantLock();
    private final Condition condition = lock.newCondition();

    public void produce(int value) {
        lock.lock();
        try {
            while (available) {
                condition.await(); // Wait if data is already produced
            }
            data = value;
            System.out.println("Produced: " + data);
            available = true;
            condition.signal(); // Notify the consumer
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    public void consume() {
        lock.lock();
        try {
            while (!available) {
                condition.await(); // Wait if no data is available
            }
            System.out.println("Consumed: " + data);
            available = false;
            condition.signal(); // Notify the producer
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }
}

public class ThreadCommunicationWithLock {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();
        new Thread(() -> { for (int i = 1; i <= 5; i++) resource.produce(i); }).start();
        new Thread(resource::consume).start();
    }
}
```
### **Why Use Locks?**
- More control over synchronization.
- Avoids issues like **spurious wakeups**.


## **3. Using `BlockingQueue` (Simplest Approach)**
Instead of manually using `wait/notify`, Java provides `BlockingQueue`, which handles inter-thread communication automatically.

### **Example Using `LinkedBlockingQueue`**
```java
import java.util.concurrent.*;

class Producer implements Runnable {
    private BlockingQueue<Integer> queue;

    public Producer(BlockingQueue<Integer> queue) {
        this.queue = queue;
    }

    public void run() {
        try {
            for (int i = 1; i <= 5; i++) {
                queue.put(i); // Puts element, waits if full
                System.out.println("Produced: " + i);
                Thread.sleep(1000);
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

class Consumer implements Runnable {
    private BlockingQueue<Integer> queue;

    public Consumer(BlockingQueue<Integer> queue) {
        this.queue = queue;
    }

    public void run() {
        try {
            for (int i = 1; i <= 5; i++) {
                int value = queue.take(); // Takes element, waits if empty
                System.out.println("Consumed: " + value);
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class BlockingQueueExample {
    public static void main(String[] args) {
        BlockingQueue<Integer> queue = new LinkedBlockingQueue<>(2);
        new Thread(new Producer(queue)).start();
        new Thread(new Consumer(queue)).start();
    }
}
```
### **Why Use `BlockingQueue`?**
- Handles `wait/notify` internally.
- No need for explicit synchronization.

### **Comparison of Approaches**
| Method | Complexity | Best For |
|--------|------------|---------|
| `wait()/notify()` | Medium | Simple inter-thread communication |
| `Lock/Condition` | Medium | More control over synchronization |
| `BlockingQueue` | Easy | Producer-Consumer pattern |

For most cases, **`BlockingQueue` is recommended** because it simplifies inter-thread communication.

---

## 51. **Can We Create a Fixed (Immutable) List in Java?**
Yes! Java provides multiple ways to create **fixed-size** or **immutable** lists. Here are different approaches:


## **1. Using `Arrays.asList()` (Fixed-Size, But Mutable)**
- The list is **fixed-size**, meaning you **cannot add or remove elements**.
- However, you **can modify existing elements**.

```java
import java.util.Arrays;
import java.util.List;

public class FixedListExample {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("A", "B", "C");

        list.set(1, "X"); // ✅ Allowed
        System.out.println(list); // Output: [A, X, C]

        list.add("D"); // ❌ UnsupportedOperationException
        list.remove("A"); // ❌ UnsupportedOperationException
    }
}
```

### **Key Points**
✅ **Can modify elements (`set()`)**  
❌ **Cannot add/remove elements (`add()/remove()`)**

## **2. Using `List.of()` (Completely Immutable)**
Introduced in Java 9, `List.of()` creates **a truly immutable list**.

```java
import java.util.List;

public class ImmutableListExample {
    public static void main(String[] args) {
        List<String> list = List.of("A", "B", "C");

        list.set(1, "X"); // ❌ UnsupportedOperationException
        list.add("D"); // ❌ UnsupportedOperationException
        list.remove("A"); // ❌ UnsupportedOperationException
    }
}
```

### **Key Points**
✅ **Best for creating read-only lists**  
❌ **Cannot modify, add, or remove elements**


## **3. Using `Collections.unmodifiableList()`**
This method wraps a list and **makes it immutable**, but modifications to the original list will reflect in the unmodifiable list.

```java
import java.util.*;

public class UnmodifiableListExample {
    public static void main(String[] args) {
        List<String> original = new ArrayList<>(Arrays.asList("A", "B", "C"));
        List<String> fixedList = Collections.unmodifiableList(original);

        fixedList.set(1, "X"); // ❌ UnsupportedOperationException
        fixedList.add("D"); // ❌ UnsupportedOperationException

        original.set(1, "X"); // ✅ Changes reflect in fixedList
        System.out.println(fixedList); // Output: [A, X, C]
    }
}
```

### **Key Points**
✅ **Wraps an existing list**  
❌ **Changes in the original list will reflect in the unmodifiable list**

## **4. Using `Collections.singletonList()` (Single Element Fixed List)**
Creates an **immutable list with only one element**.

```java
import java.util.Collections;
import java.util.List;

public class SingletonListExample {
    public static void main(String[] args) {
        List<String> list = Collections.singletonList("A");

        list.set(0, "X"); // ✅ Allowed
        list.add("B"); // ❌ UnsupportedOperationException
        list.remove(0); // ❌ UnsupportedOperationException
    }
}
```

### **Key Points**
✅ **Single-element list (Can modify the element but not the size)**  
❌ **Cannot add or remove elements**

### **Comparison of Fixed List Methods**
| Method | Can Modify Elements? | Can Add/Remove? | Java Version |
|--------|----------------|---------------|--------------|
| `Arrays.asList()` | ✅ Yes | ❌ No | Java 1.2 |
| `List.of()` | ❌ No | ❌ No | Java 9 |
| `Collections.unmodifiableList()` | ❌ No | ❌ No | Java 1.2 |
| `Collections.singletonList()` | ✅ Yes (for single element) | ❌ No | Java 1.3 |


### **Which One to Use?**
- **Need a fixed-size but modifiable list?** → Use `Arrays.asList()`
- **Need a completely immutable list?** → Use `List.of()`
- **Need an immutable wrapper around an existing list?** → Use `Collections.unmodifiableList()`
- **Need a single-element immutable list?** → Use `Collections.singletonList()`

---

## 52. Reasons Why Java is Not Fully OOP
Java is **not considered a "pure" Object-Oriented Programming (OOP) language** because it does not strictly enforce all object-oriented principles. While Java follows OOP concepts like **encapsulation, inheritance, and polymorphism**, it includes some features that break the pure OOP model.  

### **1. Presence of Primitive Data Types (`int`, `char`, etc.)**
- Java has **primitive types** (`int`, `char`, `double`, `boolean`, etc.) that are **not objects**.
- In a fully OOP language, everything should be an object.
  
🔹 **Example:**
```java
int num = 10;  // num is not an object
```
👉 **In pure OOP languages like Smalltalk, even numbers are objects.**  

**Workaround:** Java provides wrapper classes (`Integer`, `Double`, etc.) to convert primitives into objects, but primitives still exist.  
```java
Integer num = Integer.valueOf(10);  // Now, num is an object
```


### **2. Static Methods and Variables**
- Java allows **static methods** and **static variables** that belong to a class rather than an object.
- In **pure OOP**, everything should be associated with objects.

🔹 **Example:**
```java
class Example {
    static int count = 0;  // Not associated with an object

    static void show() {   // Can be called without an object
        System.out.println("Static method");
    }
}

public class Main {
    public static void main(String[] args) {
        Example.show();  // ✅ No object required
    }
}
```
👉 **In pure OOP, you would need to create an instance to access any method.**


### **3. Use of `static` Keyword in Main Method**
- The `main()` method is **static**, meaning it can run without creating an object.
- In **true OOP**, execution should start with an object.

🔹 **Example:**
```java
public class Main {
    public static void main(String[] args) {  // static method
        System.out.println("Hello, Java!");
    }
}
```
👉 **In a fully OOP language, the entry point should require an object instance.**


### **4. Lack of Multiple Inheritance (Uses Interfaces Instead)**
- Java **does not support multiple inheritance** for classes due to the **diamond problem**.
- Instead, Java uses **interfaces** as a workaround.

🔹 **Example (Not Allowed in Java):**
```java
class A {
    void show() {
        System.out.println("A");
    }
}

class B {
    void show() {
        System.out.println("B");
    }
}

// ❌ Java does not allow multiple inheritance
class C extends A, B {}  // Compilation error
```

👉 **In fully OOP languages like C++, multiple inheritance is supported.**

**Java Workaround:**
```java
interface A {
    void show();
}

interface B {
    void display();
}

class C implements A, B {  // ✅ Using interfaces
    public void show() {
        System.out.println("A");
    }

    public void display() {
        System.out.println("B");
    }
}
```

### **5. Non-OOP Features Like Operators and Control Statements**
- Java still uses **procedural programming** constructs like:
  - `if`, `for`, `while` loops (not object-based)
  - Arithmetic operators (`+`, `-`, `*`, `/`) are not method calls.

🔹 **Example:**
```java
int a = 5, b = 10;
int sum = a + b;  // Using `+` instead of a method call
```
👉 **In pure OOP, even operations should be done through objects (e.g., `a.add(b)`).**


## **Is Java an Object-Oriented Language?**
✅ **Yes, Java is primarily OOP-based, but not 100% OOP.**  
❌ **It has features that break pure OOP principles (like primitives and static methods).**  

💡 **A Fully OOP Language Would Have:**
- No primitives (everything is an object)
- No static methods or variables
- No direct use of operators (`+`, `-`, etc.)
- Object-based execution (no `static main()`)


### **Conclusion**
| Feature | Java | Fully OOP (e.g., Smalltalk) |
|---------|------|----------------|
| Everything is an Object | ❌ No (primitives exist) | ✅ Yes |
| Multiple Inheritance | ❌ No (only via interfaces) | ✅ Yes |
| Static Methods | ✅ Yes | ❌ No |
| Operators as Methods | ❌ No | ✅ Yes |
| Execution Without Object | ✅ Yes (`static main()`) | ❌ No |

Java follows **OOP principles**, but its design **includes non-OOP features** for performance and simplicity. That’s why Java is called **"not a fully object-oriented language" but an "OOP-based language."** 🚀  ---

## 53. If you have two default methods in a functional interface and you are printing ram from one method and Shyam from other method then how to print Shyam using other class
A **functional interface** in Java is an interface that has only **one abstract method**. However, it can have **multiple default methods**.  

### Problem Breakdown:
- You have two `default` methods in a functional interface.
- One method prints `"Ram"`, and the other prints `"Shyam"`.
- You want to print `"Shyam"` using another class.

### Solution:
You can achieve this by **overriding** the `default` method in a class that implements the interface. Here’s how you can do it:

### Code Implementation:

#### **1. Define the Functional Interface**
```java
@FunctionalInterface
interface MyInterface {
    void abstractMethod(); // Functional interface must have one abstract method

    default void printRam() {
        System.out.println("Ram");
    }

    default void printShyam() {
        System.out.println("Shyam");
    }
}
```

#### **2. Implement the Interface in a Class**
```java
class MyClass implements MyInterface {
    @Override
    public void abstractMethod() {
        // Implementation of the abstract method
        System.out.println("Abstract Method Implementation");
    }

    @Override
    public void printShyam() {
        System.out.println("Shyam"); // Overriding the default method
    }
}
```

#### **3. Test the Implementation**
```java
public class Main {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        
        obj.printShyam();  // This will print "Shyam"
    }
}
```

### **Explanation:**
1. The `MyInterface` has **two default methods**: `printRam()` and `printShyam()`.
2. The `MyClass` implements `MyInterface` and **overrides** the `printShyam()` method.
3. When calling `obj.printShyam()`, the overridden method in `MyClass` executes and prints `"Shyam"`.

Here are a few interview questions based on **functional interfaces and default methods** that test a candidate’s understanding of Java 8 features:  

### **1. Default Methods in Functional Interfaces**  
> **Question:**  
If a functional interface has two default methods, and both print different values (e.g., `"Ram"` and `"Shyam"`), how can you ensure that `"Shyam"` is printed when calling the method from another class?  

> **Follow-up Question:**  
Can you override default methods in a class that implements the functional interface? If yes, how does method resolution work?  


### **2. Multiple Default Methods Conflict**  
> **Question:**  
If a class implements two interfaces, and both interfaces have a default method with the **same signature**, how can you resolve the conflict?  

> **Expected Answer:**  
The implementing class must **override** the conflicting method explicitly to resolve ambiguity.  

### **3. Functional Interface with Multiple Default Methods**  
> **Question:**  
Is it valid for a **functional interface** to have multiple **default methods**? If yes, how does it still satisfy the functional interface definition?  

> **Hint:**  
A functional interface must have exactly **one abstract method**, but it **can** have multiple `default` and `static` methods.  


### **4. Calling Superclass Default Method from Implementing Class**  
> **Question:**  
If an interface provides a default method, how can an implementing class explicitly call that interface’s default method from an overridden method?  

> **Example:**  
```java
interface MyInterface {
    default void show() {
        System.out.println("Interface default method");
    }
}

class MyClass implements MyInterface {
    @Override
    public void show() {
        MyInterface.super.show(); // Calling interface's default method
        System.out.println("Overridden method");
    }
}
```
> **What will be the output of the above code?**  
```java
Interface default method
Overridden method
```

### **5. Can a Functional Interface Extend Another Interface?**  
> **Question:**  
Can a functional interface extend another interface that has a default method? If yes, will the default method be available to the implementing class?  

> **Hint:**  
Yes, a functional interface **can** extend another interface. The implementing class will inherit the default method unless it overrides it.  

Here are some **scenario-based** and **real-world** interview questions on **functional interfaces and default methods** in Java:  

### **1. Real-World Scenario: Logging Mechanism**  
> **Question:**  
Imagine you are designing a logging framework where multiple classes need a default logging method. You want to provide a `log()` method in an interface, but also allow classes to override it if needed.  
>
> - How would you design the interface using default methods?  
> - How can a class use the interface’s default `log()` method without overriding it?  

> **Hint:**  
Use a default method in the interface for logging, and allow implementing classes to override it selectively.  


### **2. Diamond Problem with Default Methods**  
> **Question:**  
You have two interfaces, `InterfaceA` and `InterfaceB`, both containing a default method with the **same name and implementation**. If a class `MyClass` implements both interfaces, how will Java resolve this conflict?  

```java
interface InterfaceA {
    default void greet() {
        System.out.println("Hello from A");
    }
}

interface InterfaceB {
    default void greet() {
        System.out.println("Hello from B");
    }
}

class MyClass implements InterfaceA, InterfaceB {
    // What should you do here to resolve the conflict?
}
```
- What happens if you don’t override the `greet()` method in `MyClass`?  
- How can you explicitly call `greet()` from `InterfaceA` inside `MyClass`?  

> **Expected Answer:**  
Java will throw a **compilation error** due to ambiguity. You must override `greet()` in `MyClass` and use `InterfaceA.super.greet()` or `InterfaceB.super.greet()` to specify which one to call.  


### **3. Designing a Payment Gateway Using Functional Interface**  
> **Question:**  
You are designing a payment gateway where different payment processors (PayPal, Stripe, Razorpay) must implement a `processPayment()` method. You also want a **default method** to **validate payments** before processing.  

> - How would you design a functional interface for this use case?  
> - If a new payment provider wants to modify only the validation logic, how can it override the default method?  

> **Hint:**  
Use a **functional interface** with one abstract method (`processPayment()`) and a default method (`validatePayment()`). Allow implementing classes to override validation logic if necessary.  

### **4. Combining Functional Interfaces and Streams**  
> **Question:**  
Suppose you have a `List<String>` of employee names and you need to:  
1. Convert all names to uppercase  
2. Filter names that start with "A"  
3. Print them using a method from a functional interface  

- How can you achieve this using Java Streams and a custom functional interface?  
- Can a default method in the functional interface be used to provide a common transformation logic?  


### **5. Modifying Default Method Behavior Dynamically**  
> **Question:**  
You have a functional interface with a default method for sending notifications. Some users prefer **email**, while others prefer **SMS**.  

- How can you modify the default method dynamically based on user preference **without modifying the interface**?  
- Can this be achieved using **lambda expressions** or **method references**?  

> **Hint:**  
Pass a custom implementation using lambda expressions or override the default method in an anonymous class.  

### **6. Default Methods vs. Abstract Classes**  
> **Question:**  
Both **default methods in interfaces** and **methods in abstract classes** allow code reuse.  
- When should you **prefer default methods** over an **abstract class**?  
- Can an interface with default methods completely replace an abstract class?  

> **Expected Answer:**  
- Default methods allow multiple inheritance, while abstract classes don’t.  
- If shared behavior is needed but the class should still extend another class, **default methods** are better.  
- If state (fields) needs to be maintained, an **abstract class** is preferred.  

---

## 54. Questions on Hibernate: 

1️⃣ Hibernate Basics – What is Hibernate? How does it work? Why is it better than JDBC? 
### **What is Hibernate?**  
**Hibernate** is a **Java-based ORM (Object-Relational Mapping) framework** that simplifies database interactions by mapping Java objects to database tables. It eliminates the need for writing complex SQL queries and handles **database CRUD operations** efficiently.  

✅ **Key Features of Hibernate:**  
- **ORM-Based**: Maps Java classes to database tables.  
- **HQL (Hibernate Query Language)**: Supports database-independent queries.  
- **Automatic Table Creation**: Generates tables based on Java entity classes.  
- **Caching**: Improves performance by reducing database hits.  
- **Lazy & Eager Loading**: Optimizes data fetching.  
- **Transaction Management**: Works seamlessly with JPA and Spring Boot.  

### **How Does Hibernate Work?**
1. **Configuration**  
   - Uses `hibernate.cfg.xml` or `persistence.xml` (if using JPA).  
   - Defines database connection properties and entity mappings.  

2. **SessionFactory Creation**  
   - `SessionFactory` is created once (expensive operation).  
   - Manages `Session` instances for database operations.  

3. **Session & Transaction Management**  
   - `Session` is used to perform CRUD operations.  
   - `Transaction` ensures data consistency.  

4. **Query Execution**  
   - Uses **HQL (Hibernate Query Language)** or **Criteria API** instead of raw SQL.  

5. **Caching & Optimization**  
   - First-level cache (default) and second-level cache (optional).  
   - Lazy loading prevents unnecessary data retrieval.  

### **Why Hibernate is Better Than JDBC?**
| Feature | Hibernate | JDBC |
|---------|----------|------|
| **ORM (Object-Relational Mapping)** | Yes, converts Java objects to DB tables automatically | No, manual SQL writing needed |
| **Query Language** | HQL (Database Independent) | SQL (DB Specific) |
| **Automatic Table Creation** | Yes, via `@Entity` annotations | No, tables must be created manually |
| **Caching Support** | Yes, first and second-level caching | No caching, always queries DB |
| **Transaction Management** | Built-in support | Manual handling required |
| **Performance Optimization** | Lazy loading, caching, batching | No built-in optimization |
| **Scalability** | Works well with large applications | Becomes complex with large codebases |

✅ **Hibernate reduces boilerplate code, improves maintainability, and provides flexibility across different databases.**  


### **Example: Hibernate vs. JDBC**
#### **JDBC Approach (Manual SQL Queries)**
```java
Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/db", "user", "pass");
PreparedStatement ps = con.prepareStatement("INSERT INTO Employee VALUES (?,?)");
ps.setInt(1, 101);
ps.setString(2, "John");
ps.executeUpdate();
```
- 🚨 Requires **manual SQL handling**.  
- 🚨 **DB-specific queries** → Less flexible.  
- 🚨 **No built-in caching** → Slower performance.  

#### **Hibernate Approach (Entity-Based)**
```java
@Entity
@Table(name="Employee")
public class Employee {
    @Id @GeneratedValue
    private int id;
    private String name;
}
```
```java
Session session = sessionFactory.openSession();
Transaction tx = session.beginTransaction();
Employee e = new Employee();
e.setName("John");
session.save(e);
tx.commit();
session.close();
```
- ✅ **No manual SQL** → Uses objects instead.  
- ✅ **Auto table creation** via `@Entity`.  
- ✅ **Database independent** (Works with MySQL, PostgreSQL, etc.).  
- ✅ **Faster performance** via caching.  

### **When Should You Use Hibernate?**
✔ **Enterprise Applications** (Spring Boot, Microservices).  
✔ **Projects Needing DB Portability** (Supports MySQL, PostgreSQL, Oracle, etc.).  
✔ **Scalable & Maintainable Apps** (Less SQL, more object-oriented).  

⛔ **When Not to Use Hibernate?**  
- If **performance is extremely critical**, raw JDBC **may be faster** for simple queries.  
- If the project **does not involve relational databases** (NoSQL, Redis).  


### **Conclusion**
Hibernate simplifies database interactions **by removing the need for raw SQL** and handling **transactions, caching, and object mappings** efficiently. 🚀  

2️⃣ Configuration & Annotations – Setting up Hibernate with `hibernate.cfg.xml` and using JPA annotations like `@Entity`, `@Table`, `@Column`, etc. 

3️⃣ Session & SessionFactory – Understanding how Hibernate manages database operations using Session and SessionFactory. 

4️⃣ Hibernate CRUD Operations – Performing Create, Read, Update, Delete operations using Hibernate. 

5️⃣ HQL (Hibernate Query Language) – Writing database-independent queries using HQL instead of raw SQL. 

6️⃣ Criteria API – Fetching data dynamically using Hibernate's Criteria API. 

7️⃣ Lazy & Eager Loading – Controlling how Hibernate fetches related data (`@OneToMany`, `@ManyToOne`). 

8️⃣ Caching in Hibernate – First-level vs. Second-level caching, using EhCache or Redis for performance optimization. 

9️⃣ Transaction Management – Handling transactions with commit, rollback, and exception handling. 

🔟 Hibernate Relationships & Mappings – Implementing `@OneToOne`, `@OneToMany`, `@ManyToOne`, and `@ManyToMany` mappings. 

1️⃣1️⃣ Pagination in Hibernate – Efficiently fetching large datasets using pagination. 

1️⃣2️⃣ Native SQL Queries – Using createNativeQuery() to run raw SQL queries when needed. 

---

## 55. DTO vs Entity
Both **DTO (Data Transfer Object)** and **Entity** are commonly used in Java applications, but they serve different purposes. Let’s break down their differences:

### **1. What is an Entity?**
An **Entity** is a Java class that represents a **database table**. It is directly mapped to a table using **JPA annotations** (`@Entity`).  

✅ **Key Features of an Entity:**  
- Represents a **database table**.  
- Managed by **Hibernate/JPA**.  
- Contains **database-specific fields** (e.g., `@Id`, `@Column`).  
- **Tightly coupled** with the database.  

### **Example: Entity Class**
```java
import jakarta.persistence.*;

@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    private String email;
    
    // Getters and Setters
}
```
- **`@Entity`** → Marks it as a JPA entity.  
- **`@Table(name = "users")`** → Maps to the database table "users".  
- **`@Id`** → Primary key.  

🔹 **Used for:** Database operations (CRUD).  


### **2. What is a DTO (Data Transfer Object)?**
A **DTO** is a **plain Java class** used to **transfer data** between layers (Controller ↔ Service ↔ Client).  
DTOs are **not managed by JPA** and usually contain only required fields.  

✅ **Key Features of a DTO:**  
- **Not mapped to the database** (No `@Entity`).  
- Used to transfer data between layers.  
- Improves **performance & security** (only necessary fields exposed).  
- Helps **avoid exposing entity structure** to external clients (REST APIs).  

#### **Example: DTO Class**
```java
public class UserDTO {
    private String name;
    private String email;

    // Constructor
    public UserDTO(String name, String email) {
        this.name = name;
        this.email = email;
    }

    // Getters
}
```
- **No `@Entity` annotations**.  
- **Only essential fields** (No `id` here).  

🔹 **Used for:** API responses, reducing data exposure.  

### **3. Differences Between DTO and Entity**
| Feature        | Entity | DTO |
|---------------|--------|-----|
| **Purpose**   | Represents a database table | Transfers data between layers |
| **Annotation** | `@Entity`, `@Table` | Plain Java class (No annotations) |
| **Managed By** | Hibernate / JPA | Application logic (Controller, Service) |
| **Contains**  | All database fields | Only required fields |
| **Performance** | Can be slow (large data fetch) | Optimized, lightweight |
| **Security** | Exposes all fields (risk) | Can hide sensitive fields |


### **4. How to Convert Between DTO and Entity?**
Since DTOs and Entities serve different purposes, we need to **convert** between them using a **Mapper** function.

### **Example: Convert Entity → DTO in a Service Layer**
```java
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    // Convert Entity to DTO
    public UserDTO getUserById(Long id) {
        User user = userRepository.findById(id).orElseThrow();
        return new UserDTO(user.getName(), user.getEmail()); // Convert Entity to DTO
    }
}
```

### **Example: Convert DTO → Entity (For Saving to Database)**
```java
public User convertToEntity(UserDTO userDTO) {
    User user = new User();
    user.setName(userDTO.getName());
    user.setEmail(userDTO.getEmail());
    return user;
}
```
✅ **Using a DTO ensures the API does not expose database fields like `id`, `password`, etc.**  

### **5. When to Use DTO vs. Entity?**
| **Scenario** | **Use DTO?** | **Use Entity?** |
|-------------|-------------|-------------|
| **Fetching data for API response** | ✅ Yes (return only necessary fields) | ❌ No (avoid exposing entity directly) |
| **Saving/updating data in DB** | ✅ Yes (for validation) | ✅ Yes (JPA manages persistence) |
| **Internal database operations** | ❌ No | ✅ Yes |
| **Avoiding lazy loading issues** | ✅ Yes | ❌ No |

### **6. Why Use DTOs Instead of Entities in APIs?**
🚀 **Advantages of DTOs in REST APIs:**  
1. **Prevents over-exposure of database fields** (e.g., `password`, `createdAt`).  
2. **Reduces response size** (improves performance).  
3. **Decouples database structure from API responses** (flexibility).  
4. **Allows API versioning** without changing database schema.  

🔴 **Bad Practice (Returning Entity in API Response)**  
```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) { // ❌ Exposes Entity directly
    return userRepository.findById(id).orElseThrow();
}
```
✅ **Good Practice (Returning DTO in API Response)**  
```java
@GetMapping("/users/{id}")
public UserDTO getUser(@PathVariable Long id) { // ✅ Uses DTO
    return userService.getUserById(id);
}
```

### **7. Conclusion**
✅ **Use `Entity` for database operations (JPA/Hibernate).**  
✅ **Use `DTO` for API responses, improving security & performance.**  
✅ **Convert between `Entity` ↔ `DTO` using Mapper functions.**  


## 56. Why Choose Spring Boot over spring MVC?
Spring MVC and Spring Boot both help build Java web applications, but **Spring Boot simplifies development** significantly. Let’s compare them and see why **Spring Boot is the preferred choice.**

### **📌 Spring MVC** (Traditional Approach)  
- Requires **manual configuration** of dependencies, database, and web server.  
- Needs **boilerplate code** for XML or Java-based configurations.  
- Requires an **external** server (Tomcat, Jetty) to run.  
- Complex **integration of third-party libraries** (Jackson, Hibernate, etc.).  

### **🚀 Spring Boot** (Modern Approach)  
- **Auto-configures** dependencies, database, and embedded servers.  
- Provides **built-in Tomcat/Jetty** (No need for an external server).  
- **Production-ready features** (Actuator, Metrics, Logging).  
- Requires **less code**, reducing development time.  

### **2. Key Differences Between Spring Boot & Spring MVC**  

| Feature             | Spring MVC | Spring Boot |
|---------------------|-----------|-------------|
| **Setup Complexity** | High (Requires manual setup) | Low (Auto-configuration) |
| **Configuration** | XML/Java-based, complex | Almost zero configuration |
| **Embedded Server** | Needs an external Tomcat/Jetty | Built-in Tomcat/Jetty |
| **Boilerplate Code** | More (Beans, XML, AppConfig) | Less (Auto-configured) |
| **Dependency Management** | Manual (spring-web, spring-core, etc.) | Simplified with `spring-boot-starter-web` |
| **Microservices Support** | Requires additional setup | Designed for microservices |
| **Performance Optimization** | Manual tuning needed | Optimized out of the box |
| **Production-Ready Features** | Not included | Actuator, Logging, Monitoring |
| **REST API Support** | Needs manual configuration | Built-in REST support |
| **Security** | Needs extra setup | Auto-configured with Spring Security |

When to Use Spring Boot vs Spring MVC?**  

| **Scenario** | **Use Spring MVC** | **Use Spring Boot** |
|-------------|--------------------|---------------------|
| **Building a traditional web app** | ✅ Yes | ✅ Yes |
| **Building REST APIs** | ❌ Harder | ✅ Easier |
| **Microservices Architecture** | ❌ No | ✅ Yes |
| **Need auto-configuration** | ❌ No | ✅ Yes |
| **Want production-ready features** | ❌ No | ✅ Yes |
| **Need fast development** | ❌ No | ✅ Yes |

#### **6. Conclusion: Why Choose Spring Boot?**  

✅ **Easier Setup** → No XML, embedded Tomcat, auto-configured.  
✅ **Less Boilerplate Code** → Just write business logic.  
✅ **Better Performance** → Optimized defaults, Actuator.  
✅ **Great for REST & Microservices** → API development is easy.  
✅ **Production-Ready** → Monitoring, Logging, Security.  

💡 **Spring Boot is the future of Spring development!** 🚀 Would you like a real-world example, like **a REST API with authentication**? 😊

---

## 57. Java Singleton Design Pattern
The **Singleton pattern** ensures that a class has **only one instance** and provides a **global point of access** to that instance. This is useful for scenarios like **database connections, logging, configuration management, and thread pools**.

### 1. Implementing Singleton Pattern in Java**
#### A. Eager Initialization (Thread-Safe)**
In this approach, the instance is created **at the time of class loading**.  
```java
public class Singleton {
    private static final Singleton instance = new Singleton(); // Eager instance creation

    private Singleton() { }  // Private constructor prevents instantiation

    public static Singleton getInstance() {
        return instance;
    }
}
```
✅ **Pros:** Simple, thread-safe  
❌ **Cons:** Instance is created even if not used  


#### **B. Lazy Initialization (Not Thread-Safe)**
Instance is created **only when needed**, but this is **not thread-safe**.
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() { }

    public static Singleton getInstance() {
        if (instance == null) { // Instance created only when first called
            instance = new Singleton();
        }
        return instance;
    }
}
```
✅ **Pros:** Saves memory if the instance is never used  
❌ **Cons:** **Not thread-safe** in multi-threaded environments  

---

#### **C. Thread-Safe Singleton (Double-Checked Locking)**
A better approach to make the Singleton thread-safe **without performance issues**.
```java
public class Singleton {
    private static volatile Singleton instance;  // Volatile to prevent multiple instances

    private Singleton() { }

    public static Singleton getInstance() {
        if (instance == null) {  // First check (no locking)
            synchronized (Singleton.class) { // Locking block
                if (instance == null) {  // Second check (after locking)
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```
✅ **Pros:** Thread-safe, efficient performance  
❌ **Cons:** More complex  

---

#### **D. Bill Pugh Singleton (Best Approach)**
This approach uses an **inner static helper class**, which ensures **lazy initialization and thread safety**.
```java
public class Singleton {
    private Singleton() { }

    private static class SingletonHelper {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```
✅ **Pros:** Lazy-loaded, thread-safe, best performance  
❌ **Cons:** None  

---

#### **E. Enum Singleton (Recommended for Thread-Safety)**
Using an `enum` prevents multiple instances **even during serialization and reflection**.
```java
public enum Singleton {
    INSTANCE;

    public void showMessage() {
        System.out.println("Singleton using Enum");
    }
}
```
✅ **Pros:** Simplest, thread-safe, prevents reflection attacks  
❌ **Cons:** Cannot support lazy initialization  

---

#### **2. When to Use Singleton Pattern?**
- **Database connections** (JDBC, Hibernate)
- **Logging framework** (Log4j, SLF4J)
- **Configuration management** (properties, environment variables)
- **Caching mechanisms** (storing frequently used objects)
- **Thread pools** (managing reusable worker threads)

---

#### **3. Avoiding Issues with Singleton**
#### 🔴 **Common Problems**
1. **Multi-threading issues** (use **Double-Checked Locking** or **Bill Pugh method**)
2. **Serialization creates multiple instances** (implement `readResolve()` method)
3. **Reflection can break Singleton** (use `Enum Singleton`)
4. **Cloning can break Singleton** (override `clone()` and throw exception)

#### ✅ **Best Practices**
- Prefer **Enum Singleton** for the safest implementation.
- Use **Bill Pugh Singleton** for **lazy initialization with thread safety**.
- Avoid unnecessary **synchronization**, as it affects performance.

---

## 58. Find the output:
    class Parent {
	public void print() throws FileNotFoundException {
		System.out.println("Parent");
    	}
    }
    
    public class Child extends Parent{
    	
    	@Override
    	public void print() throws  IOException{
    		System.out.println("Child ");
    	}
    
    	public static void main(String[] args) throws IOException {
    		Parent p = new Child();
    		p.print();
    	}
    
    }
 
Output:
    Child

---

## 59. Count repeating numbers and from an array.
  ```java
  import java.util.*;

  public class Main {
    public static void main(String[] args) {
    int[] arr = {1,2,3,4,2,2,3};
    int count=0;
    
    Map<Integer, Integer> h = new HashMap<>();
    
    for (Integer n: arr) {
      if (h.get(n)==null) {
        h.put(n, 1);
      } else {
        int x = h.get(n);
        h.put(n, x+1);
      }
    }
    
      System.out.println(h);
  }
  ```

---

## 60. Find palindrome or not for an Integer (12345 & 1234321) and a String ("ravi" & "kammak").


---

## 61. Java 8 Features Introduced
### Major Features

#### 1. Lambda Expressions  
Concise functional code using `->`.

#### 2. Functional Interfaces  
Single-method interfaces.

#### 3. Introduced and Improved APIs  
- **Stream API**: Efficient data manipulation.  
- **Date/Time API**: Robust date and time handling.  
- **Collection API Improvements**: Enhanced methods for collections (e.g., `removeIf`, `replaceAll`).  
- **Concurrency API Improvements**: New classes for parallel processing (e.g., `CompletableFuture`).  

#### 4. Optional Class  
Handle `null` values safely.

#### 5. `forEach()` Method in Iterable Interface  
Executes an action for each element in a collection.

#### 6. Default Methods  
Evolve interfaces without breaking compatibility.

#### 7. Static Methods in Interfaces  
Allows adding methods with default implementations to interfaces.

#### 8. Method References  
Refer to methods easily.

---

## 62. Valid parenthesis
	Example 1:
	Input: s = "()"
	Output: true
	Example 2:
	Input: s = "()[]{}"
	Output: true
	Example 3:
	Input: s = "(]"
	Output: false
	Example 4:
	Input: s = "([])"
	Output: true
 ```java
 class Solution {
    public boolean isValid(String s) {
        Deque<Character> stk = new ArrayDeque<>();
        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stk.push(c);
            } else if (stk.isEmpty() || !match(stk.pop(), c)) {
                return false;
            }
        }
        return stk.isEmpty();
    }

    private boolean match(char l, char r) {
        return (l == '(' && r == ')') || (l == '{' && r == '}') || (l == '[' && r == ']');
    }
 }
 ```

---

## 61. Strings are immutable or not.
Strings are immutable. Once a string is created, its value cannot be changed. Any operation that appears to modify a string actually creates a new string object. This immutability offers several benefits, including thread safety, security, and efficient memory management. 

 ```java
  public class StringImmutability {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = str1.toUpperCase(); // Creates a new string "HELLO"
        
        System.out.println(str1); // Output: Hello
        System.out.println(str2); // Output: HELLO
    }
  }
  ```

---

## 63. @Component vs @Service vs @Controller
In the Spring framework, @Component, @Service, and @Controller are annotations used for dependency injection and component scanning, each with a specific semantic meaning.
@Component:
This is the most generic annotation and marks a class as a Spring-managed component. It indicates that Spring should detect and register the class as a bean in the application context. It is used for general-purpose components that don't fit neatly into the roles of @Service or @Controller.
@Service:
This annotation specializes @Component and designates a class as belonging to the service layer. It's used for classes containing business logic and operations. While it doesn't add specific functionality beyond @Component, it provides better code organization and clarity, indicating the purpose of the class within the application architecture.
@Controller:
This annotation, also a specialization of @Component, is used for classes that handle incoming web requests in Spring MVC applications. It marks a class as a controller, enabling it to define request handling methods and interact with the view layer. It is mainly used in the presentation layer.
In essence, @Service and @Controller are specialized forms of @Component. They don't inherently add new technical capabilities but provide semantic meaning, making the code more readable and maintainable by clearly defining the role of each component within the application's architecture.

---

## 64. ArrayList vs LinkedList
|     |                                                                                   ArrayList                                                                                   |                                                                                                 LinkedList                                                                                                |
|:---:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|  1. |            This class uses a dynamic array to store the elements in it. With the introduction of generics, this class supports the storage of all types of objects.           |                         This class uses a doubly linked list to store the elements in it. Similar to the ArrayList, this class also supports the storage of all types of objects.                         |
|  2. | Manipulating ArrayList takes more time due to the internal implementation. Whenever we remove an element, internally, the array is traversed and the memory bits are shifted. | Manipulating LinkedList takes less time compared to ArrayList because, in a doubly-linked list, there is no concept of shifting the memory bits. The list is traversed and the reference link is changed. |
|  3. |                                                                        Inefficient memory utilization.                                                                        |                                                                                          Good memory utilization.                                                                                         |
|  4. |                                                                    It can be one, two or multi-dimensional.                                                                   |                                                                          It can either be single, double or circular LinkedList.                                                                          |
|  5. |                                                                          Insertion operation is slow.                                                                         |                                                                                        Insertion operation is fast.                                                                                       |
|  6. |                                                    This class implements a List interface. Therefore, this acts as a list.                                                    |                                            This class implements both the List interface and the Deque interface. Therefore, it can act as a list and a deque.                                            |
|  7. |                                            This class works better when the application demands storing the data and accessing it.                                            |                                                           This class works better when the application demands manipulation of the stored data.                                                           |
|  8. |                                         Data access and storage is very efficient as it stores the elements according to the indexes.                                         |                                                                               Data access and storage is slow in LinkedList.                                                                              |
|  9. |                                                                   Deletion operation is not very efficient.                                                                   |                                                                                   Deletion operation is very efficient.                                                                                   |
| 10. |                                                                It is used to store only similar types of data.                                                                |                                                                                   It is used to store any types of data.                                                                                  |
| 11. |                                                                              Less memory is used.                                                                             |                                                                                            More memory is used.                                                                                           |
| 12. |                                                                   This is known as static memory allocation.                                                                  |                                                                                This is known as dynamic memory allocation.                                                                                |

---

## 65. Duplicate records from a table.
SELECT * 
FROM your_table 
WHERE your_column IN (
    SELECT your_column 
    FROM your_table 
    GROUP BY your_column 
    HAVING COUNT(*) > 1
);

---

## 66. @SpringBootApplication
The @SpringBootApplication annotation in Spring Boot is a composite annotation that combines three other annotations: @Configuration, @EnableAutoConfiguration, and @ComponentScan. It is used to mark the main class of a Spring Boot application and enables several key features.
@Configuration:
Indicates that the class can be used by the Spring IoC container as a source of bean definitions. It essentially marks the class as a configuration class, allowing it to define beans using @Bean annotated methods.
@EnableAutoConfiguration:
Enables Spring Boot's auto-configuration mechanism, which automatically configures the application based on the dependencies added in the classpath. It attempts to infer and configure beans that are likely needed based on the project's dependencies. 
@ComponentScan:
Enables component scanning, allowing Spring to automatically discover and register beans in the application context within the package of the annotated class and its sub-packages.
By combining these three annotations, @SpringBootApplication simplifies the setup and configuration of Spring Boot applications. It serves as a convenient and concise way to bootstrap a Spring Boot application, reducing the need for manual configuration and boilerplate code.

---

## 67. How to configure multiple database in Spring Boot.
Add in your application.properties file:

#first db
spring.datasource.url = [url]
spring.datasource.username = [username]
spring.datasource.password = [password]
spring.datasource.driverClassName = oracle.jdbc.OracleDriver

#second db ...
spring.secondDatasource.url = [url]
spring.secondDatasource.username = [username]
spring.secondDatasource.password = [password]
spring.secondDatasource.driverClassName = oracle.jdbc.OracleDriver
Add in any class annotated with @Configuration the following methods:

@Bean
@Primary
@ConfigurationProperties(prefix="spring.datasource")
public DataSource primaryDataSource() {
    return DataSourceBuilder.create().build();
}

@Bean
@ConfigurationProperties(prefix="spring.secondDatasource")
public DataSource secondaryDataSource() {
    return DataSourceBuilder.create().build();
}

---

## 68. 

---

## 69. 

---

## 70. 

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


#Core Java & OOP Concept
✅ What is the difference between a class and an object? 
✅ Explain OOP principles (Encapsulation, Inheritance, Polymorphism, Abstraction) with examples. 
✅ What is method overloading vs. method overriding? 
✅ How does Java handle memory management (Heap vs. Stack, Garbage Collection)? 
✅ Explain shallow copy vs. deep copy in Java. 
✅ What are static methods and variables, and when should you use them? 

hashtag#Comparator vs. Comparable 
✅ What is the difference between Comparator and Comparable? 
✅ How do you sort a list using Comparator? 
✅ Can a class implement both Comparator and Comparable? 
✅ How do you handle multiple sorting criteria in Java? 

hashtag#Functional Programming & Streams 
✅ What are functional interfaces, and how are they used? 
✅ Explain filter, map, reduce operations in Java Streams. 
✅ How do you handle parallel streams, and when should you use them? 
✅ What is the difference between findFirst() and findAny()? 
✅ Can you modify a collection while iterating using streams? 

hashtag#Spring Boot & Advanced Java 
✅ What are key annotations in Spring Boot? 
✅ Difference between @Controller vs. @RestController? 
✅ What is the Bean Lifecycle in Spring? 
✅ How does Spring Boot handle dependency injection? 
✅ What are proxies in Spring, and why are they needed? 
✅ How does @Transactional work in Spring Boot? 
