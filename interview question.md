# Java and Spring Boot Interview Preparation

## 1. Difference Between Parallelism and Concurrency

| S.No | Concurrency | Parallelism |
|------|------------|-------------|
| 1 | Concurrency is the task of running and managing multiple computations at the same time. | Parallelism is the task of running multiple computations simultaneously. |
| 2 | Achieved through interleaving operation of processes on the CPU (context switching). | Achieved using multiple central processing units (CPUs). |
| 3 | Can be done using a single processing unit. | Requires multiple processing units. |
| 4 | Increases the amount of work finished at a time. | Improves system throughput and computational speed. |
| 5 | Deals with multiple tasks at once. | Executes multiple tasks at the same time. |
| 6 | Follows a non-deterministic control flow approach. | Uses a deterministic control flow approach. |
| 7 | Debugging is very difficult. | Debugging is also hard but simpler than concurrency. |

---

## 2. List vs Set

## 3. Creating an Immutable Class in Java

An **immutable class** in Java means that once an object is created, its content cannot be changed.  
All wrapper classes (`Integer`, `Boolean`, `Byte`, `Short`) and the `String` class in Java are immutable.

### Requirements:
- The class must be declared as `final` (to prevent subclassing).
- Data members must be `private` (to restrict direct access).
- Data members must be declared `final` (to prevent modification).
- A parameterized constructor should initialize all fields using **deep copy**.
- No setters should be provided.

---

## 4. Validation in Spring Boot

## 5. Java 8 Stream API Questions

- Create `List<Integer>`, add values, filter even numbers, and return a list using streams.
- Convert `List<Integer>` to `List<String>` using streams.
- Convert `List<Employee>` to `Map<Integer, String>` (key: employee ID, value: employee name).
- Convert `List<Employee>` to `Map<Double, List<Employee>>` (key: salary, value: employee list).
- Convert `List<Employee>` to `Map<Double, String>` (key: salary, value: comma-separated employee names).

---

## 6. Functional Interfaces

## 7. SOLID Principles

## 8. Difference Between Hibernate and JDBC

## 9. Common Java Annotations

## 10. Find Length of Longest Substring Without Repeating Characters

```java
Input: s = "abcabcbb"
Output: 3
Explanation: "abc" (length = 3)

Input: s = "bbbbb"
Output: 1
Explanation: "b" (length = 1)

Input: s = "pwwkew"
Output: 3
Explanation: "wke" (length = 3)
```

---

## 11. Technical Architecture

## 12. SQL vs NoSQL

## 13. Factory Design Pattern

## 14. Algorithm Behind `Collection.sort()`

## 15. Challenges Faced as an Engineer & How to Solve Them

## 16. How JVM Works?

## 17. Spring Boot Actuator

## 18. Difference Between Abstract Class and Interface

## 19. Understanding Browser Caching

## 20. Strong Knowledge of UX Design Principles

## 21. Event-Driven Implementation Using Kafka

## 22. HTML5/CSS

## 23. Angular 17 Features

## 24. Lazy Loading in Hibernate

## 25. Reverse a String in Java

```java
public class ReverseString {
    public static void main(String[] args) {
        String str = "Java";
        String reversed = new StringBuilder(str).reverse().toString();
        System.out.println("Reversed: " + reversed);
    }
}
```

---

## 26. Exception Handling in Angular

### Strategies:
1. **Try-Catch Blocks**
2. **Global ErrorHandler**
3. **RxJS `catchError` Operator**
4. **HTTP Interceptors**
5. **Displaying User-Friendly Error Messages**
6. **Logging Errors**

```typescript
import { Injectable, ErrorHandler } from '@angular/core';

@Injectable()
export class GlobalErrorHandler implements ErrorHandler {
  handleError(error: any) {
    console.error('Global error:', error);
  }
}
```

---

## 27. Signals in Angular

## 28. Zone.js

## 29. Find Second Highest Salary in SQL

```sql
SELECT salary 
FROM employees 
ORDER BY salary DESC 
LIMIT 1 OFFSET 1;
```

---

## 30. Shift an Array by 3 Positions to the Right in Java

```java
import java.util.Arrays;

public class ArrayShift {
    public static void main(String[] args) {
        int[] array = {1, 2, 3, 4, 5, 6, 7};
        int shiftBy = 3;

        shiftArrayRight(array, shiftBy);
        System.out.println("Shifted Array: " + Arrays.toString(array));
    }

    public static void shiftArrayRight(int[] array, int positions) {
        int length = array.length;
        positions = positions % length;
        reverseArray(array, 0, length - 1);
        reverseArray(array, 0, positions - 1);
        reverseArray(array, positions, length - 1);
    }

    private static void reverseArray(int[] array, int start, int end) {
        while (start < end) {
            int temp = array[start];
            array[start] = array[end];
            array[end] = temp;
            start++;
            end--;
        }
    }
}
```

---

## 31. Java 8 Stream API Operations

### Intermediate Operations:
- `flatMap(List::stream)`
- `filter(s -> s.startsWith("S"))`
- `map(String::toUpperCase)`
- `distinct()`
- `sorted()`
- `peek(...)`
- `collect(Collectors.toList())`

### Terminal Operations:
- `forEach`
- `collect`
- `reduce`
- `count`
- `findFirst`
- `allMatch`
- `anyMatch`

---

## 32. Find First Repeating Character in a String

```java
import java.util.HashSet;
import java.util.Optional;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        String myString = "iamaveryverylongstring";
        Optional<Character> firstRepeated = findFirstRepeatedCharacter(myString);

        firstRepeated.ifPresent(c -> System.out.println("First repeated character: " + c));
    }

    public static Optional<Character> findFirstRepeatedCharacter(String input) {
        Set<Character> seenCharacters = new HashSet<>();
        return input.chars()
                .mapToObj(c -> (char) c)
                .filter(c -> !seenCharacters.add(c))
                .findFirst();
    }
}
```

---

## 33. Find Employees Who Are Managers in SQL

```sql
SELECT e1.name 
FROM emp e1 
JOIN emp e2 
ON e1.emp_mgr_id = e2.emp_id;
```

---

## 34. Common HTTP Status Codes

- **200**: OK  
- **201**: Created  
- **403**: Forbidden  
- **500**: Internal Server Error  
- **502**: Bad Gateway  

---

## 35. Best Websites to Practice JavaScript Output-Based Questions

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
