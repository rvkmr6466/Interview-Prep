1. What is the difference between parallism vs concurrency?
2. List vs Set
3. Create an immutable class
  Immutable class in java means that once an object is created, we cannot change its content. In Java, all the wrapper classes (like Integer, Boolean, Byte,     
  Short) and String class is immutable. We can create our own immutable class as well. Prior to going ahead do go through characteristics of immutability in order 
  to have a good understanding while implementing the same. Following are the requirements: 
  - The class must be declared as final so that child classes can’t be created.
  - Data members in the class must be declared private so that direct access is not allowed.
  - Data members in the class must be declared as final so that we can’t change the value of it after object creation.
  - A parameterized constructor should initialize all the fields performing a deep copy so that data members can’t be modified with an object reference.
  - Deep Copy of objects should be performed in the getter methods to return a copy rather than returning the actual object reference)
  
  Note: There should be no setters or in simpler terms, there should be no option to change the value of the instance variable.

4. Validation in Spring Boot
5. Questions on Stream API
  5.1 Create List<Integer> add some values in it and filter all even numbers and return to list again using java 8 stream.
  5.2 Convert List<Integer> to List<String> using  java 8 streams.
  5.3 Convert List<Employee> to Map<Integer,String> where key will be employee id and value will be employee name using java 8 stream.'
  5.4 Convert List<Employee> to Map<Double,List<Employee>> where key will be employee salary and value will be employee list accordingly using java 8 stream.
  5.5 Convert List<Employee> to Map<Double,String> where key will be employee salary and value will be employee names comma seperated	 accordingly using java 8 stream.
   
7. Functional interface
*7. SOLID principles
8. Difference between hibernate and JDBC
*9. Annotations used in java.
10. Given a string s, find the length of the longest substring without duplicate characters.
  Example 1:
    Input: s = "abcabcbb"
    Output: 3
    Explanation: The answer is "abc", with the length of 3.
    Example 2:
    Input: s = "bbbbb"
    Output: 1
    Explanation: The answer is "b", with the length of 1.
    Example 3:
    Input: s = "pwwkew"
    Output: 3
    Explanation: The answer is "wke", with the length of 3.
    Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
11. Technical architecture
12. SQL vs NoSQL
13. Factory Design pattern
14. Alogithm behind Collection.sort().
15. Challenges you faces as an engineer and how did you resolved it?
16. How jvm works?
17. Spring actuator
18. Diff between Abstract class vs interface
19. Understanding of browser caching.
20. Strong knowledge of UX design and principles.
21. Event-driven implementation using Kafka.
22. Html 5/css
23. Angular 17 features
24. Lazy loading in hibernate
25. Reverse you name in Java 
26. Handle exception in Angular
  A: Error handling in Angular applications is crucial for providing a smooth user experience and debugging issues. Here's an overview of common strategies:
    1. Try-Catch Blocks
      Used for handling synchronous errors within specific code blocks.
      
      try {
        // Code that might throw an error
        const result = someFunction();
      } catch (error) {
        // Handle the error
        console.error('An error occurred:', error);
      }

  2. Angular ErrorHandler
    A global error handling mechanism for catching unhandled exceptions.
    
    import { Injectable, ErrorHandler } from '@angular/core';
    @Injectable()
    export class GlobalErrorHandler implements ErrorHandler {
      handleError(error: any) {
        // Log the error, display a user-friendly message, etc.
        console.error('Global error handler:', error);
      }
    }
    To use it, provide it in your module or component:
    TypeScript
    
    import { NgModule } from '@angular/core';
    import { GlobalErrorHandler } from './global-error-handler';
    import { ErrorHandler } from '@angular/core';
    
    @NgModule({
      providers: [{ provide: ErrorHandler, useClass: GlobalErrorHandler }],
    })
    export class AppModule {}

  3. RxJS catchError Operator
    Handles errors in Observables, commonly used with HTTP requests.
    
    import { catchError } from 'rxjs/operators';
    import { of } from 'rxjs';
    
    this.http.get('/api/data').pipe(
      catchError(error => {
        console.error('HTTP error:', error);
        // Return a new observable or throw the error again
        return of([]); // Return an empty array as a fallback
      })
    ).subscribe(data => {
      // Process the data
    });

  4. HTTP Interceptors
    Centralized handling of HTTP errors for all requests.
    
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
              console.error('HTTP error:', error);
              // Handle the error (e.g., display a message, retry the request)
              return throwError(() => error);
            })
          );
      }
    }
    Provide the interceptor in your module:
    
    import { NgModule } from '@angular/core';
    import { HTTP_INTERCEPTORS } from '@angular/common/http';
    import { HttpErrorInterceptor } from './http-error-interceptor';
    
    @NgModule({
      providers: [{ provide: HTTP_INTERCEPTORS, useClass: HttpErrorInterceptor, multi: true }],
    })
    export class AppModule {}

  5. Displaying Error Messages
    Provide user-friendly feedback when errors occur.
    Use descriptive error messages that guide users.
    Avoid exposing sensitive information.
    Display errors in a consistent manner (e.g., using a dialog or notification).
  
  6. Logging Errors
    Log errors for debugging and monitoring purposes.
    Use console.error for development.
    Consider using a logging service for production.
    Include relevant information in logs (e.g., timestamp, error message, stack trace). 

27. Signal in Angular
28. Zone.js
29. Second highest salary from a table
  SELECT salary
  FROM employees
  ORDER BY salary DESC
  LIMIT 1 OFFSET 1;

30. Write a coode to Shift an array by 3 to the right ([1,2,3,4,5] -> [4,5,1,2,3])
31. Stream API in Java
  Stream API is used to process collections of objects. A stream in Java is a sequence of objects that supports various methods that can be pipelined to produce the desired result.
    Intermediate operations:
      flatMap(List::stream): Flattens the nested lists into a single stream of strings.
      filter(s -> s.startsWith("S")): Filters the strings to only include those that start with “S”.
      map(String::toUpperCase): Converts each string in the stream to uppercase.
      distinct(): Removes any duplicate strings.
      sorted(): Sorts the resulting strings alphabetically.
      peek(...): Adds each processed element to the intermediateResults set for intermediate inspection.
      collect(Collectors.toList()): Collects the final processed strings into a list called result.

  Terminal operations:
    forEach: Prints each name in the list.
    collect: Filters names starting with ‘S’ and collects them into a new list.
    reduce: Concatenates all names into a single string.
    count: Counts the total number of names.
    findFirst: Finds and prints the first name in the list.
    allMatch: Checks if all names start with ‘S’.
    anyMatch: Checks if any name starts with ‘S’.

  For more: https://www.geeksforgeeks.org/stream-in-java/

React project 
Core Java prepare
Spring boot
