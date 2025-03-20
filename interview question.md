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

## 42. Div vs span
div is a block element
span is an inline element.

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

## **1. Enable Caching in Spring Boot**
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

## **2. Use @Cacheable Annotation**
You can use `@Cacheable` to cache method results so that subsequent calls with the same arguments return the cached result instead of executing the method again.

### **Example: Caching a Method Result**
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
### **How It Works:**
1. The first time `getUserById(1)` is called, it fetches data and stores it in the cache.
2. The next time `getUserById(1)` is called, it returns the cached result instead of executing the method.


## **3. Clear Cache with @CacheEvict**
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


## **4. Update Cache with @CachePut**
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


## **5. Configure Cache in application.properties**
Spring Boot uses **ConcurrentHashMap** as the default cache. You can configure other cache providers like **EhCache, Redis, or Caffeine**.

### **For Simple In-Memory Cache:**
```properties
spring.cache.type=simple
```

### **For Redis Cache:**
```properties
spring.cache.type=redis
spring.redis.host=localhost
spring.redis.port=6379
```


## **6. Example with Redis Cache**
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


## **Conclusion**
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

## **Ways to Avoid ConcurrentModificationException**
### **1. Use Iterator’s remove() Method**
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

### **2. Use `CopyOnWriteArrayList` (Thread-Safe)**
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

### **3. Use `removeIf()` Method (Java 8+)**
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

### **4. Use `Stream API` for Filtering (Java 8+)**
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

### **Conclusion**
| Approach | Safe? | Best For |
|----------|------|---------|
| `Iterator.remove()` | ✅ Yes | Single-threaded list modification |
| `CopyOnWriteArrayList` | ✅ Yes | Multi-threaded environments |
| `removeIf()` | ✅ Yes | Simple removals (Java 8+) |
| `Stream API` | ✅ Yes | Functional-style filtering |

Would you like a deeper explanation of any approach? 🚀

## 50. Thread Communication in Java
Threads in Java communicate with each other mainly using **wait(), notify(), and notifyAll()**, which are part of the `Object` class. This is commonly used for **inter-thread synchronization**.


## **1. Using wait() and notify()**
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

Java follows **OOP principles**, but its design **includes non-OOP features** for performance and simplicity. That’s why Java is called **"not a fully object-oriented language" but an "OOP-based language."** 🚀  

---

## 53.

---

## 54.

---

## 55.

---

## 56.

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
