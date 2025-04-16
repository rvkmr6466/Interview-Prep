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
In Java, an **immutable class** is one whose **instances cannot be modified after creation, ensuring their state remains constant**. To create an immutable class, you need to:  
- Make the class `final`  
- Declare fields as `private` and `final`  
- Provide a constructor to initialize fields  
- Use **defensive copying** for mutable objects  
### **Steps to Create an Immutable Class in Java**  
1. **Make the class `final`**  
   - Prevents inheritance, which could allow modification through subclassing.  
2. **Make all fields `private` and `final`**  
   - Prevents direct access and modification of fields after object creation.  
3. **Provide a constructor to initialize all fields**  
   - Use a constructor to set initial values.  
   - Perform deep copies for mutable objects to avoid unintended modifications.  
4. **Do not provide setter methods**  
   - Since the object's state is immutable, there should be no methods to modify its fields.  
5. **Use getter methods carefully**  
   - If fields are mutable, return a **copy** of the object instead of exposing the original reference.  
6. **Use defensive copying for mutable objects**  
   - If the class contains references to mutable objects, create and return a copy in getter methods to **prevent external modification** of the internal state.  
### **Example: Immutable Class in Java**
```java
 public final class Person {
    private final String name;
    private final int age;
    private final String[] hobbies; // Example of a mutable object

    public Person(String name, int age, String[] hobbies) {
        this.name = name;
        this.age = age;
        // Defensive copy for mutable object
        this.hobbies = hobbies.clone();
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    // Defensive copy for mutable object in getter method
    public String[] getHobbies() {
        return hobbies.clone();
    }
 }
```
### **Benefits of Immutable Classes**  
✔ **Thread Safety:** Immutable objects are inherently thread-safe as their state cannot change, eliminating the need for synchronization.  
✔ **Caching:** Since values remain constant, immutable objects can be safely cached and reused.  
✔ **Data Integrity:** Immutability ensures the object’s data remains consistent throughout its lifecycle.  
✔ **Functional Programming:** Immutability is a core principle of functional programming, making code easier to understand and debug.  
✔ **Security:** Prevents accidental or malicious modification of sensitive data.  
✔ **Example – `String` Class:**  
   - The `String` class in Java is immutable. Once a `String` object is created, its value cannot be changed.
In Java, the term "immutable" means that once a String object is created, its content cannot be changed. This implies that any operation that appears to modify a String actually creates a new String object with the modified content, leaving the original String unchanged. 
**Elaboration:**
- No In-Place Modification: Unlike mutable objects (like StringBuffer or StringBuilder), you cannot directly alter the internal character array of a String object once it's been initialized. [2, 4]  
- New Object Creation: When you try to modify a String (e.g., by concatenating or using methods like substring), the Java runtime creates a new String object containing the desired changes. The original String object remains unchanged. [1, 4]  
- Memory Efficiency and Thread Safety: Immutability is crucial for memory management and thread safety. Because String objects are immutable, they can be shared across threads without synchronization concerns, as their value will never change unexpectedly. [1, 5]  
- String Pool: Immutability also allows for the implementation of the String pool, where the JVM caches String objects with the same content. This can save memory by reusing the same object when multiple String variables refer to the same value. [3, 5]  
**Example: **
    ```
    String str1 = "Hello";
    String str2 = str1 + " World";
    System.out.println(str1); // Output: Hello (str1 remains unchanged)
    System.out.println(str2); // Output: Hello World (str2 is a new string)
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
## 5. Stream API  
Stream API in Java is used for processing collections efficiently.
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
## 6. What are functional interfaces, and how are they used?  
A functional interface in Java is an interface with exactly one abstract method, allowing it to be used with lambda expressions and method references. These interfaces are a cornerstone of functional programming in Java, enabling concise and expressive code.  
Here's a breakdown of functional interfaces: 
- **Single Abstract Method (SAM)**: A functional interface must have only one abstract method, also known as the "functional method". 
- **Lambda Expressions & Method References:** The presence of a single abstract method makes the interface a target type for lambda expressions and method references, allowing for concise and functional code. 
- **Optional @FunctionalInterface Annotation:** While not mandatory, the @FunctionalInterface annotation can be used to explicitly declare an interface as a functional interface, helping the compiler catch errors if the interface definition violates the SAM rule. 
- **Default and Static Methods:** Functional interfaces can also contain default and static methods, in addition to the single abstract method. 
- **Examples**: Runnable, ActionListener, Consumer<T>, Supplier<T>, Function<T, R>, and Predicate<T> are common examples of functional interfaces provided by Java.
How to Use Functional Interfaces:
1. **Create a Functional Interface:** Define an interface with only one abstract method.
2. **Implement with Lambda Expressions:** Use lambda expressions to provide implementations for the functional method.  
3. **Use with Method References:** Use method references to provide implementations for the functional method. 
4. **Pass as Arguments:** Pass functional interface instances (lambda expressions or method references) as arguments to methods that expect them.  
5. **Return as Values:** Return functional interface instances (lambda expressions or method references) from methods. 
**Example**: 
```java
 @FunctionalInterface
 interface MyInterface {
    void doSomething(String input);
 }

 public class Main {
    public static void main(String[] args) {
        // Using a lambda expression
        MyInterface lambdaImpl = (String input) -> System.out.println("Lambda: " + input);
        lambdaImpl.doSomething("Hello");

        // Using a method reference
        MyInterface methodRefImpl = System.out::println;
        methodRefImpl.doSomething("Method Reference");
    }
 }
```

We don’t need to define the method with an abstract keyword because by default functional interface will allow only one abstract method, if we try to define more than one abstract method in the functional interface we will get a _compile time error_.
![image](https://github.com/user-attachments/assets/202f7155-752c-4bb3-b562-73961290eda9)

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
The JVM acts as an intermediary between Java bytecode and the underlying hardware, providing a platform-independent environment for executing Java applications. It compiles Java code into bytecode, then interprets or compiles it into machine code at runtime using a Just-in-Time (JIT) compiler. This compiled code is stored in memory for later reuse. [1, 2, 3, 4]  
Here's a more detailed breakdown:
1. Java Code Compilation:
- Java source code is first compiled by the javac compiler into bytecode, which is a set of instructions independent of a specific operating system or hardware architecture.
- This bytecode is then loaded into the JVM. 

2. JVM Architecture: 
- Class Loader: Loads class files (bytecode) into memory, manages the class hierarchy, and ensures that classes are loaded only once.
- Execution Engine: Interprets or compiles bytecode into native machine code using the JIT compiler.  
- Runtime Data Areas: These are memory regions used during program execution, including:  
	• Heap: Stores objects.
	• Method Area: Stores class metadata, method code, and constant pool.
	• Stack: Manages local variables, method calls, and return addresses. 
	• Native Stack: Used for native method calls.
	• Program Counters: Keep track of the current instruction.
- Java Native Interface (JNI): Enables Java code to interact with native (non-Java) code and libraries. 
- Garbage Collector: Automatically manages memory allocation and deallocation, reclaiming unused memory.
3. Bytecode Interpretation/Compilation: 
- The JVM interprets or compiles bytecode into machine code.
- The JIT compiler optimizes frequently used bytecode, improving performance.
- This optimized code is stored in cached memory for reuse. 
4. Memory Management: 
- The JVM automatically manages memory through allocation and garbage collection.
- Objects are allocated in the heap, and when no longer referenced, the garbage collector reclaims their memory. 
5. Platform Independence:  
- The JVM provides a platform-independent environment, meaning Java applications can run on different operating systems and hardware architectures without modification.
- This is achieved by the JVM handling the translation of bytecode into machine code specific to the underlying platform. 

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
## 20. What happened when we add value in a certain size of a HashMap?
When a value is added to a HashMap when it reaches a certain size (defined by the load factor), the HashMap automatically re-sizes itself. This involves creating a new, larger internal array and then re-hashing all the existing key-value pairs into the new array. This process is called "rehashing" or "resizing".  
Elaboration:
- _Load Factor:_ HashMap uses a "load factor" (default is 0.75) to determine when to resize. This factor specifies the threshold at which the HashMap will resize.
- _Threshold_: The threshold is calculated by multiplying the current capacity of the HashMap by the load factor. For example, if the initial capacity is 16 and the load factor is 0.75, the threshold would be 12. 
- _Resizing_: When the number of key-value pairs in the HashMap exceeds the threshold, it triggers resizing.
- _Rehashing_: During resizing, the HashMap creates a new array with a larger capacity (typically twice the size of the previous one). Then, it iterates through all the existing key-value pairs and calculates their new hash codes based on the new capacity. These key-value pairs are then placed in the new array based on their new hash codes.
- _Performance_: Rehashing can be computationally expensive, but it helps to maintain the efficiency of the HashMap by preventing excessive collisions and ensuring good average-case performance.

---
## 21. Event-Driven Implementation Using Kafka  
- **Producer** sends message to **Kafka Topic**  
- **Consumer** reads message from topic  

---

## 22. JpaRepository vs CrudRepository in SpringBoot
`JpaRepository` extends `PagingAndSortingRepository` which in turn extends `CrudRepository`.
Their main functions are:
- CrudRepository mainly provides CRUD functions.
- PagingAndSortingRepository provides methods to do pagination and sorting records.
- JpaRepository provides some JPA-related methods such as flushing the persistence context and deleting records in a batch.
Because of the inheritance mentioned above, `JpaRepository` will have all the functions of `CrudRepository` and `PagingAndSortingRepository`. So if you don't need the repository to have the functions provided by `JpaRepository` and `PagingAndSortingRepository`, use `CrudRepository`.

---
## 23. Circuit Breaker Pattern in Microservices
In microservices, the **Circuit Breaker pattern** helps prevent cascading failures by detecting and reacting to service failures. It switches to a fallback mechanism to maintain system stability and prevent overload.
**Purpose**
- **Prevent Cascading Failures:** When one microservice fails, it can trigger a chain reaction of failures in dependent services. The Circuit Breaker pattern interrupts this chain by preventing further calls to the failing service.
- **Improve Resilience:** Handles failures gracefully, making the system more resilient to disruptions and outages.
- **Minimize Impact on Users:** When a service is unavailable, the Circuit Breaker can provide a fallback response or error message, preventing a complete system outage.
**How It Works**
**States of the Circuit Breaker:**
- **Closed:**  
  The service is healthy, and calls are allowed to pass through normally.
- **Open:**  
  The service is failing; further calls are rejected, and a fallback mechanism is used instead.
- **Half-Open:**  
  After a timeout period, a limited number of test calls are allowed to check if the service has recovered.
**Monitoring Mechanism:**
- **Threshold:**  
  If the number of failures exceeds a predefined threshold within a certain time period, the Circuit Breaker "opens".
- **Fallback:**  
  While in the "Open" state, subsequent calls are automatically redirected to a fallback mechanism (e.g., cached response, default value).
- **Recovery:**  
  After a timeout, the Circuit Breaker enters the "Half-Open" state. If test calls succeed, it transitions back to "Closed". If not, it remains "Open".
**Benefits**
- **Reduced Downtime:**  
  Prevents cascading failures, reducing prolonged outages.
- **Improved User Experience:**  
  Fallback mechanisms ensure continued usability even during partial outages.
- **Simplified Debugging:**  
  Easier to identify and isolate failing services.
- **Enhanced Resiliency:**  
  Increases the robustness of the overall microservices architecture.
**Example**
Imagine a **Shopping Cart** microservice that depends on a **Product Catalog** microservice to fetch product details. If the Product Catalog service goes down, the Shopping Cart service could be overwhelmed with requests and may fail too.
By implementing a **Circuit Breaker**, the Shopping Cart service can:
- Monitor the Product Catalog service.
- Open the circuit if failures exceed a threshold.
- Stop calling the failing service temporarily.
- Display a user-friendly message like _"Product details are temporarily unavailable."_  
- Retry after a timeout to check if the Product Catalog service has recovered.
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

## 26. Orchestration vs Choreography in microservices
In microservices architecture, orchestration uses a central controller to manage interactions between services, while choreography relies on decentralized, event-driven communication where services interact independently.  
**Orchestration:**  
- _Centralized Control:_ A central orchestrator or conductor manages the flow of interactions between microservices.
- _Command-Driven:_ The orchestrator sends commands or instructions to other services, dictating the sequence of operations.
- _Simpler to Implement:_ Orchestration can be easier to implement and maintain, as the control logic is centralized.
- _Potential Single Point of Failure:_ The orchestrator itself can become a single point of failure if it fails.
**Example:** Think of a conductor leading an orchestra, where the conductor dictates the timing and actions of each musician.
**Choreography:**
- _Decentralized Communication:_ Microservices communicate directly with each other through events or messages, without a central controller.
- _Event-Driven:_ Services react to events published by other services, triggering their own actions. [2, 4]
- _Loosely Coupled:_ Microservices are loosely coupled, meaning they can operate independently and asynchronously. [2, 4]
- _More Complex to Debug:_ Debugging and understanding the flow of interactions can be more challenging in a choreography-based system. [2, 5]
**Example:** Imagine a dance where each dancer knows their steps and when to interact with other dancers, but there's no central leader directing the dance. [2, 3]  
**Key Differences Summarized:** 
| Feature | Orchestration | Choreography  |
| --- | --- | --- |
| Control | Centralized (by an orchestrator) | Decentralized (services interact directly)  |
| Communication | Command-driven (orchestrator sends commands) | Event-driven (services react to events)  |
| Coupling | Tightly coupled (services depend on orchestrator) | Loosely coupled (services are independent)  |
| Complexity | Simpler to implement and maintain | More complex to debug and understand  |
| Resilience | Orchestrator is a potential single point of failure | Services are more resilient, but debugging is harder  |

---

## 27. Default method vs static method
In interfaces, default methods provide default implementations, allowing classes implementing the interface to optionally override them, while static methods provide utility functions directly on the interface itself and cannot be overridden. [1, 2, 3]  
Default Methods: [4, 5]  

• Provide a concrete implementation for a method within the interface. [4, 5]  
• Can be overridden by implementing classes, allowing them to provide their own specialized implementations. [1, 6]  
• Enable interface evolution without breaking backward compatibility; new default methods can be added without requiring implementing classes to change their code. [1, 2, 3]  
• Used to provide default implementations for common functionality, which can be inherited by implementing classes. [7, 8]  

Static Methods: [4, 5]  

• Are declared with the static keyword and belong to the interface itself. [4, 5]  
• Cannot be overridden by implementing classes. [8, 9]  
• Typically used for utility functions or helper methods related to the interface, without requiring an instance of the implementing class. [8, 10]  
• Can be accessed directly through the interface name, e.g., InterfaceName.staticMethod(). [4, 9]  
• Provide security by preventing implementation classes from overriding them. [8]  

---
## 28. 

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

## 31. 

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
Common HTTP status codes include 200 OK, 301 Moved Permanently, 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 500 Internal Server Error, and 503 Service Unavailable. These codes indicate the outcome of a request made to a web server. 
Here's a breakdown of some common codes: 
• 200 OK: The request was successful, and the server has delivered the requested resource. 
• 301 Moved Permanently: The requested resource has been moved to a new location, and the browser should update its address. 
• 400 Bad Request: The server cannot process the request due to an error in the request itself, such as incorrect syntax. 
• 401 Unauthorized: The client needs to authenticate with the server before being able to access the resource. 
• 403 Forbidden: The server understands the request but refuses to authorize it. 
• 404 Not Found: The server cannot find the requested resource. 
• 500 Internal Server Error: The server encountered an unexpected condition that prevented it from fulfilling the request. 
• 503 Service Unavailable: The server is temporarily unable to handle the request due to overload or maintenance.
These codes are categorized into groups based on their meaning, such as 1xx (informational), 2xx (success), 3xx (redirection), 4xx (client errors), and 5xx (server errors).

---

## 35. 

---

## 36. 

---

## 37. 

---

## 38. 

---

## 39. 

---

## 40. 

---

## 41. 

---

## 42. 

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

---
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

---
## 45. Second highest element in an Array using stream
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
    ```
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
    ```

---

## 46. Stream vs Parallelstream
In Java, both `stream()` and `parallelStream()` are methods used to create streams from collections, but they have different execution models.
- `stream()`: Creates a sequential stream that processes elements one at a time in a single thread.
- `parallelStream()`: Creates a parallel stream that can process elements concurrently using multiple threads, potentially improving performance for large datasets.
Here is an example demonstrating the difference:
    ```
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
    ```
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

---
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

---
## 48. How to Use Caching in Spring Boot
Spring Boot provides built-in support for caching using the **Spring Cache Abstraction**. This allows caching data in memory or using external cache providers like **Redis**, **EhCache**, and **Caffeine**.
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

---
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
### **1. Using `Arrays.asList()` (Fixed-Size, But Mutable)**
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
### **3. Using `Collections.unmodifiableList()`**
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

---
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
#### **2. When to Use Singleton Pattern?**
- **Database connections** (JDBC, Hibernate)
- **Logging framework** (Log4j, SLF4J)
- **Configuration management** (properties, environment variables)
- **Caching mechanisms** (storing frequently used objects)
- **Thread pools** (managing reusable worker threads)
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

## 59. Count repeating numbers from an array in java.
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

## 60. Write a program to find a string or a number is palindrome or not?.
```
class Main {
  public static void main(String[] args) {

    String str = "Radar", reverseStr = "";
    
    int strLength = str.length();

    for (int i = (strLength - 1); i >=0; --i) {
      reverseStr = reverseStr + str.charAt(i);
    }

    if (str.toLowerCase().equals(reverseStr.toLowerCase())) {
      System.out.println(str + " is a Palindrome String.");
    }
    else {
      System.out.println(str + " is not a Palindrome String.");
    }
  }
}
```
```
class Main {
  public static void main(String[] args) {
    
    int num = 3553, reversedNum = 0, remainder;
    
    // store the number to originalNum
    int originalNum = num;
    
    // get the reverse of originalNum
    // store it in variable
    while (num != 0) {
      remainder = num % 10;
      reversedNum = reversedNum * 10 + remainder;
      num /= 10;
    }
    
    // check if reversedNum and originalNum are equal
    if (originalNum == reversedNum) {
      System.out.println(originalNum + " is Palindrome.");
    }
    else {
      System.out.println(originalNum + " is not Palindrome.");
    }
  }
}
```

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
**Example 1:**
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
**Example 2:**
```
public class StringImmutabilityExample {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = str1.concat(", World!");

        System.out.println("str1: " + str1); // Output: str1: Hello
        System.out.println("str2: " + str2); // Output: str2: Hello, World!
    }
}
```
In this example, `str1` is initialized with the value "Hello". When the `concat()` method is called on `str1` to append ", World!", a new String object is created with the value "Hello, World!", and `str2` is assigned to this new object. The original `str1` remains unchanged. This behavior demonstrates that String objects are immutable; their values cannot be modified after they are created. Any operation that appears to modify a String actually results in the creation of a new String object.

---

## 63. @Component vs @Service vs @Controller
In the Spring framework, @Component, @Service, and @Controller are annotations used for dependency injection and component scanning, each with a specific semantic meaning.
_@Component:_
This is the most generic annotation and marks a class as a Spring-managed component. It indicates that Spring should detect and register the class as a bean in the application context. It is used for general-purpose components that don't fit neatly into the roles of @Service or @Controller.
_@Service:_
This annotation specializes @Component and designates a class as belonging to the service layer. It's used for classes containing business logic and operations. While it doesn't add specific functionality beyond @Component, it provides better code organization and clarity, indicating the purpose of the class within the application architecture.
_@Controller:_
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
## 66. @SpringBootApplication Annotation in Spring Boot
The `@SpringBootApplication` annotation is a **composite annotation** in Spring Boot that combines three other annotations:  

1. **`@Configuration`**  
   - Marks the class as a configuration class.  
   - Allows defining beans using `@Bean` annotated methods.  

2. **`@EnableAutoConfiguration`**  
   - Enables **Spring Boot’s auto-configuration mechanism**.  
   - Automatically configures beans based on the classpath dependencies.  

3. **`@ComponentScan`**  
   - Enables **component scanning**.  
   - Automatically discovers and registers Spring beans within the package and its sub-packages.  

### **Purpose of `@SpringBootApplication`**  
- Marks the **main class** of a Spring Boot application.  
- Simplifies the setup by reducing the need for manual configuration.  
- Provides a **concise way** to bootstrap a Spring Boot application.  

### **Example Usage:**  
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MySpringBootApplication {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}
```

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
## 68. Object class methods in java:
In Java, the `Object` class serves as the root of the class hierarchy, meaning every class implicitly or explicitly inherits from it. This class provides several essential methods available to all Java objects. 

Below is an overview of the commonly used methods in the `Object` class:  

#### 1. `clone()`  
- Creates and returns a copy of the object.  
- It is a `protected` method and must be overridden and made `public` in subclasses to be used.  
- The class must implement the `Cloneable` interface; otherwise, it throws a `CloneNotSupportedException`.  

#### 2. `equals(Object obj)`  
- Compares two objects for equality.  
- The default implementation checks if the two objects are the same instance in memory.  
- Often overridden to provide a meaningful comparison based on object attributes.  

#### 3. `finalize()`  
- Called by the garbage collector before an object is reclaimed.  
- Allows cleanup actions before destruction.  
- Its use is discouraged due to unpredictability and performance issues.  

#### 4. `getClass()`  
- Returns the runtime class of the object.  
- It is a `final` method, meaning it cannot be overridden.  

#### 5. `hashCode()`  
- Returns a hash code value for the object.  
- Used by hash-based collections like `HashMap` and `HashSet`.  
- If `equals()` is overridden, `hashCode()` must also be overridden to maintain consistency.  

#### 6. `toString()`  
- Returns a string representation of the object.  
- The default implementation provides the class name and object's hash code.  
- Commonly overridden to provide a more meaningful representation of an object’s state.  

#### 7. `notify()`  
- Wakes up a single thread waiting on this object's monitor.  
- Used for thread synchronization.  

#### 8. `notifyAll()`  
- Wakes up all threads waiting on this object's monitor.  
- Also used for thread synchronization.  

#### 9. `wait()`  
- Causes the current thread to wait until another thread invokes `notify()` or `notifyAll()`.  
- Can also wait until a specified timeout elapses.  
- Used for thread synchronization.  

### Conclusion  
These methods provide fundamental functionalities for all Java objects, including object creation, comparison, string representation, and thread synchronization. Understanding them is crucial for effective Java programming.  

---
## 69.  HashMap vs Hashtable in Java 

Both `HashMap` and `Hashtable` are used to store key-value pairs in Java, but they have some key differences in terms of performance, synchronization, and usage.  

| Feature         | HashMap | Hashtable |
|---------------|---------|----------|
| **Synchronization** | Not synchronized (not thread-safe). | Synchronized (thread-safe). |
| **Performance** | Faster because it is not synchronized. | Slower due to synchronization overhead. |
| **Null Keys/Values** | Allows **one null key** and multiple null values. | Does **not** allow null keys or null values. |
| **Iteration (Fail-Fast vs Fail-Safe)** | Uses **fail-fast** iterator (throws `ConcurrentModificationException` if modified during iteration). | Uses **fail-safe** enumerator (does not throw an exception when modified). |
| **Thread Safety** | Not thread-safe (use `Collections.synchronizedMap()` or `ConcurrentHashMap` for thread safety). | Thread-safe (synchronized by default). |
| **Performance in Multi-threading** | Better performance in single-threaded environments. | Can cause performance bottlenecks due to synchronization. |
| **Inheritance** | Inherits from `AbstractMap`. | Inherits from `Dictionary` (legacy class). |
| **Usage Recommendation** | Preferred in non-threaded applications for better performance. | Used in multi-threaded environments where synchronization is needed. |

### **When to Use What?**  
- Use **`HashMap`** when **performance is a priority** and **synchronization is not required**.  
- Use **`Hashtable`** only if **you need thread-safety**, but **`ConcurrentHashMap`** is usually a better alternative.  

#### **Example Usage**  

**HashMap Example:**  
```java
import java.util.*;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(1, "Apple");
        map.put(2, "Banana");
        map.put(null, "Orange"); // Allows null key

        System.out.println(map); // Output: {1=Apple, 2=Banana, null=Orange}
    }
}
```

**Hashtable Example:**  
```java
import java.util.*;

public class HashtableExample {
    public static void main(String[] args) {
        Hashtable<Integer, String> table = new Hashtable<>();
        table.put(1, "Apple");
        table.put(2, "Banana");
        // table.put(null, "Orange"); // Throws NullPointerException

        System.out.println(table); // Output: {1=Apple, 2=Banana}
    }
}
```

---

## 70.

---

## 71. MySQL vs PostgreSQL: A Detailed Comparison  

| Feature            | **MySQL**  | **PostgreSQL**  |
|--------------------|-----------|----------------|
| **Architecture**  | Relational Database (RDBMS) | Object-Relational Database (ORDBMS) |
| **ACID Compliance** | Fully ACID-compliant (with InnoDB) | Fully ACID-compliant |
| **Performance**  | Faster for **read-heavy** workloads | Better for **write-heavy** and complex queries |
| **SQL Compliance** | Partially SQL-compliant | More SQL-compliant (supports advanced SQL features) |
| **Indexing** | Supports B-Tree, Full-text, and Hash Indexing | Supports B-Tree, Hash, GiST, GIN, BRIN Indexing |
| **JSON Support** | Basic JSON functions | Advanced JSON and JSONB support |
| **Concurrency Control** | Uses **row-level locking** (InnoDB) | Uses **MVCC (Multi-Version Concurrency Control)** |
| **Replication** | Supports Master-Slave & Group Replication | Supports Master-Slave, Logical & Streaming Replication |
| **Partitioning** | Limited support (Range & List) | Advanced Partitioning (Range, List, Hash) |
| **Stored Procedures** | Supports **PL/SQL-like** syntax | Supports **PL/pgSQL**, Python, Java, etc. |
| **Extensions & Customization** | Limited extensibility | Highly extensible (e.g., TimescaleDB, PostGIS) |
| **Security** | Basic authentication & SSL | Advanced security with role-based access, RLS |
| **Use Cases** | Web applications, CMS (e.g., WordPress, Joomla) | Data analytics, OLAP, GIS, complex queries |

### **Which One to Choose?**
- **Choose MySQL if:** You need a simple, fast, and lightweight database for web apps.  
- **Choose PostgreSQL if:** You need complex queries, high scalability, and advanced features like JSON, GIS, and full ACID compliance.

---

## 72. Find the output:
	1. String s = "A";
           s = "B";
	   System.out.println(list);
	output: "B"
 
        2. final int x = 10;
           x=20;
	   System.out.println(x);
	output: The Java code will result in a compile-time error because you cannot reassign a value to a final variable after its initialization.
 
        3. final List<Integer> list = new ArrayList<>();
           list.add(2);
           list.add(3);
           list.add(4);
           list.remove(2);
           System.out.println(list);

       output: [2,3]

---

## 73. What happened when a duplicate is added to a HashMap? 
When a duplicate key is added to a HashMap, the old value associated with that key is replaced by the new value, and the HashMap continues to store only one value for that key.

Here's a more detailed explanation: 
- HashMap and Unique Keys: HashMaps, by design, are intended to store unique keys, meaning each key can map to only one value.
- Duplicate Key Handling: If you attempt to insert a key that already exists, the HashMap will not insert a new entry. Instead, it will update the value associated with that existing key with the new value you've provided.
- No Exception Thrown: Adding a duplicate key does not cause a runtime exception or error; it simply overwrites the existing value.  

Example: 
```java
    HashMap<String, String> map = new HashMap<>();
    map.put("key1", "value1"); // map now contains {"key1": "value1"}
    map.put("key1", "value2"); // map now contains {"key1": "value2"} (value1 is replaced)
```
---

## 74. How hashmap works internally?
A HashMap in Java uses a hash table to store key-value pairs. The hash table is made up of an array of buckets, and each bucket can contain multiple key-value pairs.

**How it works**
1. When a key-value pair is added, the key's hashCode() method is called to calculate an integer hash value.
2. The hash value is used to determine the bucket where the entry will be placed.
3. If the bucket is empty, the entry is placed there.
4. If the bucket is not empty, the entry is added to the linked list at that bucket.
5. When a value is retrieved, the hash function is used to calculate the index of the key.
6. If there is a linked list at that index, the linked list is traversed until the key is found.

- **Collisions** 
When two keys hash to the same index, this is called a collision. To handle collisions, HashMap uses separate chaining (linked list or tree).  
- **Performance**
A good hash function distributes objects evenly. A good implementation of hashCode and equals method is required to avoid unwanted behavior.

---
## 75. How does garbage collection work in java?
Garbage collection in Java is the process of automatically managing memory by reclaiming space occupied by objects that are no longer in use. The Java Virtual Machine (JVM) handles garbage collection, relieving developers from manual memory management. Garbage collection operates primarily on the heap, the area of memory where objects are stored. It identifies and removes unreachable objects, which are objects no longer referenced by the program. 

The most common garbage collection algorithm is the mark-and-sweep algorithm, which involves the following steps:
- Marking: The garbage collector identifies and marks all reachable objects starting from root objects (e.g., global variables, local variables, and method parameters). 
- Sweeping: The garbage collector scans the heap and removes unmarked objects, freeing up the memory they occupied. 
- Compacting: After sweeping, the garbage collector may compact the remaining objects to reduce memory fragmentation. 

Garbage collection is triggered automatically by the JVM when it detects low memory or when an object cannot be allocated due to insufficient space. Developers can also manually request garbage collection using System.gc(), although this is generally discouraged as it can impact performance. 
Java uses generational garbage collection, dividing the heap into generations (young, old/tenured). Newly created objects are placed in the young generation, and objects that survive multiple garbage collection cycles are promoted to older generations. This approach optimizes garbage collection by focusing on the young generation, where most objects are short-lived. 

---

## 76. Can we override main method in java?
The main method in Java cannot be overridden in the traditional sense due to it being a static method. Overriding applies to instance methods in the context of inheritance. However, the main method can be overloaded. 
Overloading the main method means creating multiple methods with the same name but different signatures (different parameter lists). When the Java Virtual Machine (JVM) starts a program, it specifically looks for the main method with the signature public static void main(String[] args). Other overloaded main methods will not be executed automatically by the JVM; they must be called explicitly from within the public static void main(String[] args) method or other parts of the code. 
```java
class MainMethodExample {

    public static void main(String[] args) {
        System.out.println("Main method with String[] args");
        main("Hello"); // Calling overloaded main method
        main(10);      // Calling overloaded main method
    }

    public static void main(String arg1) {
        System.out.println("Overloaded main method with String argument: " + arg1);
    }

    public static void main(int arg1) {
         System.out.println("Overloaded main method with int argument: " + arg1);
    }
}
```

---
## 77. What are the methods of Optional in java
Here are the commonly used **methods of `Optional`** in Java 8, categorized by purpose for better clarity:
#### **Creation Methods**
- `Optional.of(value)`  
  → Creates an Optional with a non-null value (throws `NullPointerException` if value is null).

- `Optional.ofNullable(value)`  
  → Creates an Optional that may hold a null value.

- `Optional.empty()`  
  → Returns an empty Optional.

```
Optional<String> opt1 = Optional.of("Hello");           // Non-null value
Optional<String> opt2 = Optional.ofNullable(null);      // Can be null
Optional<String> opt3 = Optional.empty();               // Empty optional
```

#### 🔍 **Value Access & Checks**
- `get()`  
  → Returns the value if present; otherwise throws `NoSuchElementException`.

- `isPresent()`  
  → Returns `true` if the value is present, else `false`.

- `isEmpty()` *(Java 11+)*  
  → Returns `true` if the value is not present.

```
Optional<String> name = Optional.of("Alice");

System.out.println(name.get());           // Alice
System.out.println(name.isPresent());     // true
System.out.println(name.isEmpty());       // false (Java 11+)
```

#### 🛡️ **Fallbacks & Defaults**
- `orElse(defaultValue)`  
  → Returns the value if present, else returns `defaultValue`.

- `orElseGet(Supplier)`  
  → Returns the value if present, else computes value using `Supplier`.

- `orElseThrow()`  
  → Returns the value if present, else throws `NoSuchElementException`.

- `orElseThrow(Supplier)`  
  → Returns the value if present, else throws an exception provided by the `Supplier`.

```
Optional<String> emptyOpt = Optional.empty();

String val1 = emptyOpt.orElse("Default");               // "Default"
String val2 = emptyOpt.orElseGet(() -> "From Supplier");// "From Supplier"
String val3 = emptyOpt.orElseThrow(() -> new RuntimeException("No value")); // throws RuntimeException
```

#### 🔧 **Transformation Methods**
- `map(Function)`  
  → Applies the function if value is present and wraps the result in an Optional.

- `flatMap(Function)`  
  → Like `map`, but avoids nested Optionals if the function already returns an Optional.

```
Optional<String> opt = Optional.of("java");

Optional<String> upper = opt.map(String::toUpperCase);  
System.out.println(upper.get()); // "JAVA"

Optional<Integer> length = opt.map(String::length);
System.out.println(length.get()); // 4
```

#### 🧪 **Filtering**
- `filter(Predicate)`  
  → Returns the same Optional if the value matches the predicate; otherwise returns empty.

```
Optional<String> name = Optional.of("Alice");

Optional<String> filtered = name.filter(n -> n.startsWith("A"));
System.out.println(filtered.isPresent()); // true

Optional<String> filtered2 = name.filter(n -> n.startsWith("B"));
System.out.println(filtered2.isPresent()); // false
```

---

## 78. What is Transaction Propagation?
Transaction propagation defines how transactional methods should behave when called by other transactional methods. It determines whether a method should run within an existing transaction or start a new one. Understanding the different types of propagation is essential for building reliable and maintainable applications.

Types of Transaction Propagation. Spring Boot supports several types of transaction propagation:
- REQUIRED
- REQUIRES_NEW
- MANDATORY
- NESTED
- NOT_SUPPORTED
- NEVER
- SUPPORTS

Let’s dive into each of these types with detailed explanations and examples.
**1. REQUIRED**
It is the default propagation type in Spring. It means that the method must run within a transaction. If a transaction already exists, the method will run within that transaction. If there is no existing transaction, a new one will be started.
Example:
```
@Service
public class TransactionService {

    @Transactional(propagation = Propagation.REQUIRED)
    public void performTransaction() {
        // business logic
    }
}
```
Use Case:
Use REQUIRED when you want your method to participate in an existing transaction if one exists, or to create a new one if not. This is useful for methods that need to ensure that all database operations are part of a single transaction.

**2. REQUIRES_NEW**
It always starts a new transaction. If an existing transaction is present, it will be suspended until the new transaction completes.
Example:
```
@Service
public class TransactionService {

    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void performNewTransaction() {
        // business logic
    }
}
```

**3. MANDATORY**
It requires an existing transaction. If there is no active transaction, an exception will be thrown.
Example:
```
@Service
public class TransactionService {

    @Transactional(propagation = Propagation.MANDATORY)
    public void performMandatoryTransaction() {
        // business logic
    }
}
```
**Use Case:**
Use MANDATORY when a method must be called within an existing transaction context, such as methods that depend on the integrity of the outer transaction.

**4. NESTED**
It creates a nested transaction if an existing transaction is present. Otherwise, it behaves like REQUIRED and starts a new transaction.
Example:
```
@Service
public class TransactionService {

    @Transactional(propagation = Propagation.NESTED)
    public void performNestedTransaction() {
        // business logic
    }
}
```
**Use Case:**
Use NESTED for scenarios where you need savepoints and rollback capabilities within a larger transaction. This is useful for complex operations that require partial rollbacks.

**5. NOT_SUPPORTED**
It executes the method without a transaction. If a transaction is present, it will be suspended during the method execution.
Example:

```
@Service
public class TransactionService {

    @Transactional(propagation = Propagation.NOT_SUPPORTED)
    public void performNonTransactionalOperation() {
        // business logic
    }
}
```
**Use Case:**
Use NOT_SUPPORTED when you want to ensure that a method does not run within a transaction context, such as for non-transactional operations like reading configuration data.

**6. NEVER**
It ensures that the method is never executed within a transaction. If an existing transaction is present, an exception will be thrown.
Example:
```
@Service
public class TransactionService {

    @Transactional(propagation = Propagation.NEVER)
    public void performNonTransactionalOperation() {
        // business logic
    }
}
```
**Use Case:**
Use NEVER when you need to guarantee that a method runs outside of any transaction context, typically for operations that should fail if invoked within a transaction.

**7. SUPPORTS**
It runs the method within a transaction if one exists, but does not start a new transaction if none exists.
Example:
```
@Service
public class TransactionService {

    @Transactional(propagation = Propagation.SUPPORTS)
    public void performSupportedTransaction() {
        // business logic
    }
}
```
**Use Case:**
Use SUPPORTS for methods that can optionally run within a transaction, such as read-only operations that don't necessarily require transaction management.

**Best Practices**
Choose the Right Propagation Type: Select the appropriate propagation type based on your method’s transactional requirements and the overall transaction management strategy.
Avoid Overusing REQUIRES_NEW: Starting new transactions frequently can lead to performance issues and increased complexity. Use REQUIRES_NEW sparingly.
Use MANDATORY and NEVER Wisely: These propagation types enforce strict transactional requirements and should be used with a clear understanding of their implications.

**Summary**
Understanding and correctly using transaction propagation in Spring Boot is essential for building robust and reliable applications. By choosing the right propagation type, you can ensure that your transactional methods behave as expected, maintaining data consistency and integrity.

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
