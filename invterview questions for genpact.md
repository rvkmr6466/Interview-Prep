### 🔹 **Section 1: Basic Level (30 Questions)**

**Java & Spring Boot**
### 1. What are the key features of Java 8?
Java 8 introduced several powerful features that significantly enhanced Java programming:
- **Lambda Expressions**: Enables functional programming by allowing you to write inline implementations of functional interfaces.
- **Stream API**: Supports functional-style operations on collections, such as filtering, mapping, and reducing.
- **Optional Class**: Helps avoid null pointer exceptions by wrapping potentially null values.
- **Functional Interfaces**: Interfaces with a single abstract method like `Runnable`, `Callable`, `Predicate`.
- **Default and Static Methods in Interfaces**: Allows method implementations inside interfaces.
- **Date and Time API (java.time)**: A new, more robust and consistent date-time library.

*Example (Lambda + Stream API):*
```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
names.stream().filter(name -> name.startsWith("J"))
             .forEach(System.out::println);
```

---

### 2. What is Spring Boot and how is it different from Spring?
Spring Boot is an extension of the Spring framework that simplifies the setup and development of new Spring applications.

**Differences:**
- **Spring** requires extensive configuration; Spring Boot offers convention over configuration with auto-setup.
- **Spring Boot** provides embedded servers (Tomcat/Jetty) so you don't need external deployments.
- It also includes production-ready tools like **Actuator**, and has default settings to help start projects faster.

*Example:* You can run a Spring Boot application with a `main()` method:
```java
@SpringBootApplication
public class MyApp {
  public static void main(String[] args) {
    SpringApplication.run(MyApp.class, args);
  }
}
```

---

### 3. What are RESTful web services?
RESTful services follow **REST (Representational State Transfer)** architecture. They use HTTP methods (GET, POST, PUT, DELETE) to perform CRUD operations.

- **GET**: Retrieve data
- **POST**: Create new data
- **PUT**: Update existing data
- **DELETE**: Remove data

*Example:*
```java
@RestController
@RequestMapping("/api/users")
public class UserController {
    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return userService.findById(id);
    }
}
```

---

### 4. Explain dependency injection in Spring.
Dependency Injection (DI) is a design pattern where dependencies (objects) are provided by a container rather than being created manually. Spring handles DI using **constructor**, **setter**, or **field** injection.

*Example:* Using `@Autowired`:
```java
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;
}
```
This allows loose coupling and makes testing and maintenance easier.

- _Constructor Based_
```
public class SimpleMovieLister {

	// the SimpleMovieLister has a dependency on a MovieFinder
	private final MovieFinder movieFinder;

	// a constructor so that the Spring container can inject a MovieFinder
	public SimpleMovieLister(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}

	// business logic that actually uses the injected MovieFinder is omitted...
}
```

- _Setter Based_
```
public class SimpleMovieLister {

	// the SimpleMovieLister has a dependency on the MovieFinder
	private MovieFinder movieFinder;

	// a setter method so that the Spring container can inject a MovieFinder
	public void setMovieFinder(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}

	// business logic that actually uses the injected MovieFinder is omitted...
}
```

- 
---

### 5. How do you handle exceptions in Spring Boot?
Spring Boot provides exception handling using `@ControllerAdvice` and `@ExceptionHandler`.

*Example:*
```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<?> handleResourceNotFound(ResourceNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}
```
This ensures that your APIs return consistent error messages.

---

### 6. What are annotations like @RestController, @Service, @Autowired used for?
- `@RestController`: Marks a class as a RESTful controller.
- `@Service`: Indicates that a class is a service component in the service layer.
- `@Autowired`: Automatically injects dependencies.

---

### 7. What is the difference between JPA and Hibernate?
- **JPA** is a specification; **Hibernate** is an implementation.
- JPA defines how to map Java objects to database tables, Hibernate provides the actual implementation.

---

### 8. How do you implement logging in a Spring Boot app?
Use **SLF4J** with **Logback** or **Log4j2**.

*Example:*
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

private static final Logger logger = LoggerFactory.getLogger(MyService.class);
logger.info("Service started");
```

---

### 9. What is a POJO?
POJO stands for Plain Old Java Object. It is a simple class with no special restrictions. Example:
```java
public class User {
    private String name;
    private int age;
    // getters and setters
}
```

---

### 10. How do you expose and consume a REST API?
- **Exposing** using Spring Boot:
```java
@GetMapping("/api/products")
public List<Product> getProducts() { return productService.getAll(); }
```
- **Consuming** using `RestTemplate`:
```java
RestTemplate restTemplate = new RestTemplate();
Product product = restTemplate.getForObject("http://localhost:8080/api/products/1", Product.class);
```
---

**11. What are components in Angular?**

Components are the basic building blocks of an Angular application. A component includes the following parts:
- **Template**: Defines the HTML view.
- **Class**: Contains the logic (written in TypeScript).
- **Metadata**: Decorated using the `@Component` decorator to link template and class.

Example:
```typescript
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html'
})
export class UserComponent {
  name = 'John';
}
```

---

**12. What is the difference between ngIf and ngFor?**

- `*ngIf`: Conditionally renders a block based on boolean expression.
- `*ngFor`: Iterates over a list to create multiple elements.

Example:
```html
<p *ngIf="isLoggedIn">Welcome!</p>
<div *ngFor="let item of items">{{ item }}</div>
```

---

**13. Explain the concept of two-way data binding.**

Two-way data binding synchronizes data between the component class and the view using `[(ngModel)]`. When the user updates the value in the view, it automatically updates in the class and vice versa.

Example:
```html
<input [(ngModel)]="username" />
<p>{{ username }}</p>
```

---

**14. What are services in Angular and how do you use them?**

Services provide business logic and data access in Angular. They are created using the `@Injectable()` decorator and are typically injected into components via the constructor.

Example:
```typescript
@Injectable({ providedIn: 'root' })
export class UserService {
  getUsers() { return ['John', 'Jane']; }
}
```

```typescript
constructor(private userService: UserService) {}
```

---

**15. What is a module in Angular?**

A module is a container for components, services, directives, and pipes. It helps organize an application into cohesive blocks.

Example:
```typescript
@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

---

**16. Difference between Oracle and PostgreSQL.**

| Feature        | Oracle                 | PostgreSQL              |
|----------------|-------------------------|--------------------------|
| License        | Commercial              | Open-source              |
| Performance    | High (for enterprise)   | Excellent for analytics  |
| Features       | Advanced (e.g., RAC)    | Extensible (e.g., JSONB) |
| Cost           | Expensive               | Free                     |

Oracle is ideal for large enterprise systems, while PostgreSQL is suitable for cost-effective, open-source systems.

---

**17. How do you connect a Spring Boot app to a database?**

You connect a Spring Boot app to a database using JDBC or JPA. Configuration is done in `application.properties`:
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
spring.datasource.username=admin
spring.datasource.password=admin
spring.jpa.hibernate.ddl-auto=update
```

And use JPA entities:
```java
@Entity
public class User {
  @Id
  @GeneratedValue
  private Long id;
  private String name;
}
```

---

**18. What are joins in SQL?**

Joins combine rows from two or more tables based on a related column.
- **INNER JOIN**: Matches rows with common values.
- **LEFT JOIN**: Includes all rows from the left table.
- **RIGHT JOIN**: Includes all rows from the right table.
- **FULL JOIN**: Includes all rows from both tables.

Example:
```sql
SELECT users.name, orders.amount
FROM users
INNER JOIN orders ON users.id = orders.user_id;
```

---

**19. What is GCP?**

Google Cloud Platform (GCP) is a suite of cloud computing services provided by Google. It offers services for compute (e.g., GCE), storage (e.g., Cloud Storage), databases (e.g., Cloud SQL), and machine learning (e.g., Vertex AI).

You can deploy web apps, set up CI/CD, use BigQuery for analytics, and more.

---

**20. What is Jenkins used for?**

Jenkins is an open-source automation server used for continuous integration and continuous delivery (CI/CD). It helps automate tasks like building, testing, and deploying software.

You define pipelines using Jenkinsfiles, and integrate with tools like Git, Docker, and Kubernetes.

Example:
```groovy
pipeline {
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
  }
}
```

Great! Let’s continue with **questions 21–30**, each answered with **200+ words and examples** as requested.

---

### **21. What is TDD and why is it important?**

**TDD (Test-Driven Development)** is a software development approach in which test cases are written before writing the actual code. The TDD process follows a short and repetitive development cycle:
1. **Write a failing test** based on requirements.
2. **Write the minimum code** to make the test pass.
3. **Refactor** the code while keeping the test green.

This practice ensures code quality, fewer bugs, and more modular, testable code. It promotes better design decisions and helps catch issues early.

**Example:**
You are building a calculator class. You start by writing a test like:

```java
@Test
public void testAddition() {
    Calculator calc = new Calculator();
    assertEquals(5, calc.add(2, 3));
}
```

Then, you implement the `add()` method. Once it passes the test, you proceed to the next method.

TDD is vital because it fosters confidence in code changes, simplifies debugging, and acts as documentation for the system.

---

### **22. What is unit testing and which tools have you used?**

**Unit testing** involves testing individual units or components of a system in isolation. A "unit" is the smallest testable part of an application, such as a method.

**Tools** commonly used:
- **JUnit** (Java)
- **Mockito** (for mocking dependencies)
- **Jest** (JavaScript/Angular)
- **Karma** (Angular)
- **Spring Boot Test** annotations like `@WebMvcTest`, `@DataJpaTest`

**Example:**
Testing a service layer method in Spring Boot:
```java
@Test
public void getUserTest() {
    when(userRepository.findById(1L)).thenReturn(Optional.of(new User("John")));
    User user = userService.getUser(1L);
    assertEquals("John", user.getName());
}
```

Unit testing ensures code correctness and facilitates refactoring with confidence. It is a cornerstone of TDD and Agile development.

---

### **23. What is Scrum?**

**Scrum** is an Agile framework used to manage and control complex software and product development. It is iterative and incremental, enabling teams to deliver working software frequently.

**Key roles in Scrum:**
- **Product Owner:** Manages the product backlog.
- **Scrum Master:** Facilitates the process and removes impediments.
- **Development Team:** Builds the product.

**Scrum Ceremonies:**
- Sprint Planning
- Daily Standups
- Sprint Reviews
- Sprint Retrospectives

**Example:**
In a 2-week sprint, the team picks items from the backlog in Sprint Planning, meets daily in standups, and delivers a demoable product at Sprint Review. They reflect and improve in the Retrospective.

Scrum promotes transparency, collaboration, and continuous improvement.

---

### **24. What is pair programming?**

**Pair programming** is an Agile technique where two developers work together at one workstation. One writes code (the "driver"), while the other reviews each line (the "observer" or "navigator"). They switch roles frequently.

**Benefits:**
- Fewer bugs and higher code quality
- Continuous code review
- Faster onboarding of new team members
- Better knowledge sharing

**Example:**
Two developers working on an Angular component might discuss UI logic, write the template and TypeScript together, and instantly catch logic errors.

Pair programming is often used in Extreme Programming (XP) and improves team collaboration and code quality.

---

### **25. What are environment variables?**

**Environment variables** are key-value pairs used to configure applications without hardcoding values into the source code. They vary across environments (dev, test, prod) and are typically used for:
- Database credentials
- API keys
- Application secrets

**Example:**
In Spring Boot, you might use:
```properties
spring.datasource.url=${DB_URL}
```
In a terminal:
```bash
export DB_URL=jdbc:mysql://localhost:3306/mydb
```

In Angular, environment files like `environment.ts` are used for different builds.

Using environment variables enhances security and makes your app easier to configure and deploy.

---

### **26. How do you manage code quality?**

Managing code quality involves tools, practices, and processes to ensure the software is maintainable, readable, and defect-free.

**Practices:**
- Code Reviews
- Static Code Analysis (SonarQube, PMD)
- Linting (ESLint, Checkstyle)
- Writing unit/integration tests
- Following coding standards (Google Java Style Guide)

**Example:**
In a CI pipeline:
- Lint checks are run on every pull request.
- SonarQube checks for code smells and vulnerabilities.
- Code must have 80%+ test coverage to be merged.

High code quality reduces technical debt and improves maintainability.

---

### **27. What tools do you use for collaboration and tracking (JIRA, Pivotal Tracker)?**

Teams use various tools to collaborate and manage work efficiently:
- **JIRA:** For user stories, sprint planning, bug tracking
- **Pivotal Tracker:** Agile project management tool
- **Confluence:** Documentation
- **Slack, MS Teams:** Communication
- **GitHub/GitLab/Bitbucket:** Source control and code review

**Example:**
A developer uses JIRA to pick a story, tracks time, and updates the status. Code changes are committed in GitHub, where team members review it. Progress is discussed during standups and retrospectives.

These tools enable transparency, accountability, and smoother team collaboration.

---

### **28. What are microservices?**

**Microservices** are an architectural style where an application is divided into small, loosely coupled services, each responsible for a single business function.

**Key Characteristics:**
- Independent deployability
- Decentralized data management
- Own technology stack
- Inter-service communication (REST, gRPC, messaging)

**Example:**
An e-commerce app could have microservices like:
- Auth Service
- Product Service
- Cart Service
- Payment Service

Each service is developed, deployed, and scaled independently.

**Benefits:**
- Improved scalability
- Fault isolation
- Faster development

**Challenges:**
- Complex deployments
- Inter-service communication
- Monitoring and debugging

Spring Boot, Docker, and Kubernetes are commonly used in microservices.

---

### **29. How do you test REST APIs?**

**REST APIs** are tested using:
- **Postman** – Manual testing and automation via collections
- **JUnit + MockMvc** (Spring Boot)
- **RestAssured** – For integration tests
- **Swagger/OpenAPI** – Documentation and test interface

**Example (MockMvc in Spring Boot):**
```java
mockMvc.perform(get("/api/users/1"))
    .andExpect(status().isOk())
    .andExpect(jsonPath("$.name").value("John"));
```

**Test types:**
- Unit tests (controller/service)
- Integration tests (end-to-end)
- Contract tests (validate API structure)

API testing ensures correctness, stability, and reliability of services.

---

### **30. What is a software release cycle?**

A **software release cycle** refers to the stages through which software progresses, from development to production.

**Phases:**
1. **Development** – Coding and initial unit testing
2. **Testing/QA** – Functional, regression, UAT
3. **Staging/Pre-Prod** – Replica of production
4. **Production** – Live release
5. **Maintenance** – Bug fixes, updates

**Release Types:**
- Major: New features and breaking changes
- Minor: Enhancements, backward-compatible
- Patch: Bug fixes

**Tools involved:** Jenkins, GitHub Actions, Helm, Docker, Kubernetes

Following a structured release cycle ensures smooth deployment, minimal downtime, and easier rollback in case of failure.

---

Certainly! Let's proceed with the next set of 30 intermediate-level full-stack interview questions, each answered in detail with examples:

---

### **31. What is the difference between Continuous Integration, Continuous Delivery, and Continuous Deployment?**

- **Continuous Integration (CI):** Developers frequently merge code changes into a shared repository, triggering automated builds and tests to detect issues early.
  
- **Continuous Delivery (CD):** Extends CI by ensuring that code changes are automatically prepared for a release to production, but the deployment is manual.
  
- **Continuous Deployment:** Further extends CD by automatically deploying every change that passes all stages of the production pipeline to customers without manual intervention.

**Example:**
In a CI/CD pipeline:
- CI ensures that code merges trigger automated tests.
- CD packages the application and prepares it for deployment.
- Continuous Deployment automatically releases the package to production if all tests pass.

---

### **32. What are the benefits of CI/CD?**

- **Faster Time to Market:** Automates the software release process, enabling frequent and reliable releases.
- **Improved Quality:** Automated testing catches bugs early in the development cycle.
- **Reduced Manual Errors:** Automation reduces the risk of human error during deployment.
- **Enhanced Collaboration:** Encourages developers to share code and tests, improving team collaboration.
- **Quick Feedback:** Immediate feedback on code changes helps developers address issues promptly.

**Example:**
A team using CI/CD can deploy new features to production multiple times a day, with confidence that automated tests ensure stability.

---

### **33. What are the most important characteristics in a CI/CD platform?**

- **Scalability:** Ability to handle increasing workloads efficiently.
- **Reliability:** Consistent performance with minimal downtime.
- **Security:** Secure handling of code, credentials, and deployment processes.
- **Integration:** Compatibility with various tools and services (e.g., version control, testing frameworks).
- **Monitoring and Logging:** Provides insights into build and deployment processes.

**Example:**
A robust CI/CD platform integrates with Git for version control, uses Jenkins for automation, and provides dashboards for monitoring build statuses.

---

### **34. What is the build stage in a CI/CD pipeline?**

The build stage involves compiling the source code into executable artifacts. It includes:
- **Code Compilation:** Transforming source code into binary code.
- **Dependency Resolution:** Fetching and integrating external libraries.
- **Static Code Analysis:** Checking code for potential errors or code smells.

**Example:**
In a Java project, the build stage compiles `.java` files into `.class` files and packages them into a `.jar` or `.war` file.

---

### **35. What’s the difference between a hosted and a cloud-based CI/CD platform?**

- **Hosted CI/CD Platform:** Managed by a third-party service provider, requiring minimal setup from the user.
- **Cloud-Based CI/CD Platform:** Deployed on cloud infrastructure, offering scalability and flexibility.

**Example:**
- **Hosted:** GitHub Actions provides a managed CI/CD environment.
- **Cloud-Based:** Jenkins installed on AWS EC2 instances, managed by the development team.

---

### **36. How long should a build take?**

Ideally, builds should be:
- **Fast:** To provide quick feedback, builds should complete within 10 minutes.
- **Efficient:** Avoid unnecessary steps to reduce build time.
- **Scalable:** Capable of handling multiple builds concurrently.

**Example:**
A well-optimized build process compiles code, runs tests, and packages the application in under 5 minutes.

---

### **37. Is security important in CI/CD? What mechanisms are there to secure it?**

Yes, security is crucial in CI/CD pipelines. Mechanisms include:
- **Credential Management:** Secure storage of secrets and credentials.
- **Access Controls:** Restricting access to CI/CD tools and resources.
- **Audit Logging:** Tracking changes and access to the pipeline.
- **Code Signing:** Ensuring the integrity of artifacts.

**Example:**
Using tools like HashiCorp Vault to manage secrets and implementing role-based access controls in Jenkins.

---

### **38. Can you name some deployment strategies?**

- **Blue-Green Deployment:** Maintains two environments (blue and green); traffic is switched to the new version after deployment.
- **Canary Deployment:** Gradually rolls out the new version to a subset of users before full deployment.
- **Rolling Deployment:** Incrementally replaces instances of the previous version with the new one.

**Example:**
In a blue-green deployment, version 1 runs in the blue environment. After deploying version 2 to the green environment and testing, traffic is switched to green.

---

### **39. How does testing fit into CI?**

Testing is integral to CI:
- **Unit Tests:** Validate individual components.
- **Integration Tests:** Ensure components work together.
- **End-to-End Tests:** Simulate user scenarios.

Automated tests run during the CI process to catch issues early.

**Example:**
Upon code commit, Jenkins triggers a pipeline that runs unit and integration tests before merging the code.

---

### **40. Should testing always be automated?**

While automation is essential for consistency and speed, some testing types benefit from manual execution:
- **Exploratory Testing:** Human testers explore the application to find unexpected issues.
- **Usability Testing:** Assessing user experience and interface design.

However, repetitive tests like unit and regression tests should be automated.

**Example:**
Automated tests validate functionality, while manual testing assesses the application's look and feel.

---

### 🔹 **Section 2: Intermediate Level (30 Questions)**

Sure! Here's a detailed explanation for each of the questions:

---

### **1. How do you secure a Spring Boot application?**

Securing a Spring Boot application typically involves using **Spring Security**, a powerful and customizable framework that handles authentication and authorization.

**Key Steps:**
- **Authentication:** Verify user identity using username/password, tokens (JWT), OAuth2, etc.
- **Authorization:** Restrict access to specific endpoints or functionalities based on user roles.

**Example:**
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable()
            .authorizeRequests()
            .antMatchers("/api/public/**").permitAll()
            .antMatchers("/api/admin/**").hasRole("ADMIN")
            .anyRequest().authenticated()
            .and().httpBasic();
    }
}
```

Spring Security can also integrate with OAuth2 providers (like Google, Facebook) or JWT-based systems for stateless sessions.

**Best Practices:**
- Store passwords using **bcrypt**.
- Use HTTPS to encrypt traffic.
- Implement **CORS** and **CSRF** protections.
- Validate and sanitize input data.
- Use JWT for stateless authentication.

---

### **2. What is the use of @Transactional?**

`@Transactional` in Spring ensures **ACID** properties for database operations.

**Key Points:**
- Wraps methods in a **transactional context**.
- Automatically **rolls back** in case of a **RuntimeException**.
- Can be applied at **method or class level**.

**Example:**
```java
@Transactional
public void transferAmount(Account from, Account to, BigDecimal amount) {
    from.debit(amount);
    to.credit(amount);
    accountRepository.save(from);
    accountRepository.save(to);
}
```

If an exception occurs after debiting but before crediting, changes are rolled back.

**Types of Propagation:**
- `REQUIRED`, `REQUIRES_NEW`, `NESTED`, etc., define how nested transactions behave.

---

### **3. Explain the Bean Lifecycle in Spring.**

Spring Beans go through multiple stages:

1. **Instantiation**
2. **Populate Properties**
3. **BeanNameAware / BeanFactoryAware / ApplicationContextAware**
4. **PostConstruct (@PostConstruct)**
5. **afterPropertiesSet() from InitializingBean**
6. **Custom init-method**
7. **Business Logic**
8. **PreDestroy (@PreDestroy)**
9. **destroy() from DisposableBean**
10. **Custom destroy-method**

**Example:**
```java
@Component
public class MyBean {
    @PostConstruct
    public void init() {
        System.out.println("Bean initialized");
    }

    @PreDestroy
    public void destroy() {
        System.out.println("Bean destroyed");
    }
}
```

The lifecycle can be customized using annotations or interfaces like `InitializingBean`, `DisposableBean`.

---

### **4. Difference between @Component, @Service, @Repository?**

All three are Spring-managed beans annotated for component scanning.

| Annotation     | Purpose                         |
|----------------|----------------------------------|
| `@Component`   | Generic stereotype               |
| `@Service`     | Business logic layer             |
| `@Repository`  | DAO layer with exception translation |

**Example:**
```java
@Component
public class GenericBean {}

@Service
public class UserService {}

@Repository
public class UserRepository {}
```

`@Repository` also triggers exception translation to `DataAccessException`.

---

### **5. How do you paginate and sort data in Spring Data JPA?**

Spring Data JPA provides built-in support for **pagination and sorting** via `Pageable` and `Sort`.

**Example:**
```java
Page<User> findByRole(String role, Pageable pageable);
```

Usage:
```java
Pageable pageable = PageRequest.of(0, 10, Sort.by("name").ascending());
Page<User> users = userRepository.findByRole("ADMIN", pageable);
```

Returns:
- Page metadata (totalPages, totalElements)
- Current page content

You can also use `Slice<T>` when total count is not needed (for performance).

---

### **6. What are DTOs and how are they used?**

**DTO (Data Transfer Object)** is used to transfer only the required data between client and server, or between layers.

**Benefits:**
- Improves security (hide sensitive info)
- Better control over serialization
- Reduces payload size

**Example:**
```java
public class UserDTO {
    private String name;
    private String email;
}
```

Mapping:
```java
UserDTO dto = new UserDTO();
dto.setName(user.getName());
dto.setEmail(user.getEmail());
```

Can be mapped manually or using tools like **MapStruct** or **ModelMapper**.

---

### **7. What is the role of a ControllerAdvice?**

`@ControllerAdvice` is a specialization of `@Component` used for **global exception handling**, data binding, and model attribute configuration.

**Example:**
```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleNotFound(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

This avoids repetitive exception handling logic in every controller.

---

### **8. How does routing work in Angular?**

Angular uses **client-side routing** via the Angular Router.

**Key Elements:**
- `RouterModule.forRoot(routes)`
- `<router-outlet></router-outlet>` for rendering
- `routerLink="/path"` for navigation

**Example:**
```ts
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'profile', component: ProfileComponent }
];
```

Usage in HTML:
```html
<a routerLink="/profile">Profile</a>
```

The router handles navigation without reloading the page, supporting **SPA** behavior.

---

### **9. Explain lazy loading in Angular.**

Lazy loading loads modules **on demand**, not during initial app load. This reduces **bundle size** and improves performance.

**Steps:**
- Use Angular CLI to generate module with routing:
  ```
  ng generate module admin --route admin --module app
  ```

**Routing Example:**
```ts
{ path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule) }
```

Angular loads the `AdminModule` only when `/admin` route is accessed.

---

### **10. What is RxJS? What is the difference between switchMap, mergeMap, concatMap?**

**RxJS** is a reactive programming library for handling asynchronous data streams in Angular.

**Common Operators:**
- `map()`, `filter()`, `mergeMap()`, `switchMap()`, `concatMap()`

**Differences:**
| Operator    | Behavior                                                      |
|-------------|---------------------------------------------------------------|
| `switchMap` | Cancels previous inner observable                             |
| `mergeMap`  | Subscribes to all inner observables in parallel               |
| `concatMap` | Queues inner observables and executes sequentially            |

**Example:**
```ts
this.search$
  .pipe(
    debounceTime(300),
    switchMap(term => this.api.search(term))
  )
  .subscribe(results => this.results = results);
```

Here, `switchMap` ensures only the latest search result is processed, canceling prior ones.

---

### **11. How do you handle form validation in Angular?**

Angular supports **Template-driven** and **Reactive** forms.

**Reactive Forms Example:**
```ts
form = this.fb.group({
  username: ['', [Validators.required]],
  email: ['', [Validators.required, Validators.email]]
});
```

HTML:
```html
<input formControlName="username">
<div *ngIf="form.get('username').invalid">Username required</div>
```

Use `Validators` to apply custom and built-in rules.

**Benefits:**
- Precise control
- Easier to test
- Scalable for dynamic forms

---

### **12. What is the purpose of interceptors?**

**HTTP Interceptors** are used to intercept requests/responses for:

- Adding headers (e.g., JWT tokens)
- Handling errors globally
- Logging or modifying requests

**Example:**
```ts
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const token = localStorage.getItem('token');
    const cloned = req.clone({ headers: req.headers.set('Authorization', `Bearer ${token}`) });
    return next.handle(cloned);
  }
}
```

Register in providers:
```ts
{ provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true }
```

Interceptors help manage cross-cutting concerns cleanly.

---

Here are detailed answers (200+ words with examples) for the next set of questions across **Database**, **Cloud & CI/CD**, **TDD & Agile**, and **Mentorship & Communication**:

---

### **Database**

**13. What are stored procedures? When do you use them?**  
Stored procedures are precompiled sets of SQL statements stored in the database. They are useful for encapsulating repetitive logic like complex queries, insert/update logic, or business rules directly within the database, enhancing performance by reducing the amount of data sent over the network.

**Example:**  
In a payroll system, you might use a stored procedure like `calculateMonthlySalary(employee_id)` that handles complex business rules and deductions within the database. This ensures consistency and allows reusability across multiple application modules.

Stored procedures are also useful for batch operations, auditing, and enforcing data validation at the database level.

---

**14. What is normalization?**  
Normalization is a process of organizing data in a database to reduce redundancy and improve data integrity. It involves breaking down large tables into smaller, related tables and defining relationships between them using foreign keys.

There are several normal forms (1NF to 5NF), with 3NF being the most common in practice. For example, in a library system, instead of storing book and author info in the same table, you separate them into `Books` and `Authors` tables and link them using an `author_id`.

Benefits include reduced data anomalies, better scalability, and easier maintenance. However, over-normalization can impact performance in read-heavy systems, which might benefit from some degree of denormalization.

---

**15. How do you optimize queries in Postgres?**  
Query optimization in PostgreSQL involves several strategies:

- **Indexes**: Creating B-tree, GIN, or full-text indexes to speed up queries on large datasets.
- **EXPLAIN ANALYZE**: Used to inspect query plans and understand bottlenecks.
- **Avoid SELECT ***: Always fetch only required columns.
- **Use JOINs carefully**: Minimize unnecessary joins; prefer `INNER JOIN` over `LEFT JOIN` when possible.
- **Partitioning**: For huge tables, partitioning helps in scanning only relevant sections.
- **Vacuuming**: Regular vacuuming ensures table stats are up-to-date.

**Example:**  
If you notice a slow query like:
```sql
SELECT * FROM orders WHERE customer_id = 123;
```
Adding an index on `customer_id` can drastically reduce execution time.

---

### **Cloud & CI/CD**

**16. What is Kubernetes? How does it manage deployments?**  
Kubernetes is an open-source container orchestration platform that automates deployment, scaling, and management of containerized applications. It uses abstractions like Pods (container groups), Deployments (versioning), and Services (exposing apps).

**Deployment process example:**
You define a deployment YAML file that describes your app, version, and replica count. Kubernetes ensures the desired state is maintained — if a pod crashes, it auto-restarts it, rolls back if an update fails, and scales pods up/down based on traffic.

---

**17. What is the difference between Docker and Kubernetes?**  
- **Docker** is a containerization tool that packages an application with all its dependencies into a single unit.
- **Kubernetes** is an orchestration system that manages Docker containers across clusters of machines.

Think of Docker as packaging and Kubernetes as the shipping and delivery system.

---

**18. What’s your experience deploying on GCP or other cloud platforms?**  
Experience with GCP includes deploying Spring Boot microservices using Cloud Run, App Engine, and Kubernetes Engine (GKE). Also used GCP Pub/Sub for async communication, Firestore/PostgreSQL for persistence, and Stackdriver for monitoring.

CI/CD pipelines using Cloud Build and GitHub Actions have helped automate testing and deployments.

---

**19. How do you set up CI/CD pipelines in Jenkins?**  
CI/CD in Jenkins involves:
- Creating a Jenkinsfile to define stages (build, test, deploy)
- Integrating with GitHub for automated builds on pull requests
- Using plugins for SonarQube (code quality), JUnit (test reports), Docker (image builds), etc.
- Setting up environment variables and credentials securely
- Integrating with deployment tools (e.g., Helm for Kubernetes)

**Example:** A pipeline might build a Spring Boot app, run tests, create a Docker image, push it to GCR, and then deploy to GKE.

---

### **TDD & Agile**

**20. What is mock testing?**  
Mock testing involves simulating the behavior of dependencies (like services, repositories) to isolate and test a particular unit. This is done using tools like Mockito or JMock.

**Example:**
```java
@Mock
UserRepository userRepository;

@Test
void testGetUser() {
    when(userRepository.findById(1)).thenReturn(Optional.of(new User("John")));
    assertEquals("John", userService.getUser(1).getName());
}
```
This ensures your test is not dependent on the database and runs faster.

---

**21. How do you write unit tests for REST endpoints?**  
Use Spring Boot’s `@WebMvcTest` or `@SpringBootTest`. Mock the service layer using `@MockBean`.

**Example:**
```java
@WebMvcTest(UserController.class)
public class UserControllerTest {
    @Autowired MockMvc mockMvc;
    @MockBean UserService userService;

    @Test
    public void shouldReturnUser() throws Exception {
        when(userService.getUser(1)).thenReturn(new User("Alex"));
        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("Alex"));
    }
}
```

---

**22. What’s your experience with integration testing?**  
Integration testing involves checking how multiple components (e.g., controller, service, repository, database) work together. Tools: `@SpringBootTest`, Testcontainers, H2 DB.

**Example:** Testing user registration API end-to-end, including validation, DB persistence, and token generation.

---

**23. How does Agile methodology benefit the team?**  
Agile promotes iterative development, collaboration, and responsiveness to change. It ensures early feedback, faster releases, and better product-market fit.

**Benefits:**
- Quick adaptation to requirement changes
- Close collaboration via daily standups, retrospectives
- Continuous delivery of value

---

**24. What is a retrospective in Scrum?**  
Retrospective is a Scrum ceremony at the end of a sprint to reflect on what went well, what didn’t, and how to improve. It promotes team transparency and continuous improvement.

**Example Output:**
- Keep: Daily standups
- Improve: Reduce scope creep
- Action: Clarify stories better in planning

---

### **Mentorship & Communication**

**25. How do you mentor junior developers?**  
- Pair programming
- Code reviews with constructive feedback
- Explaining architectural decisions and best practices
- Setting up learning goals and sharing resources
- Encouraging participation in discussions

---

**26. How do you handle code reviews?**  
Code reviews should be respectful, focused on maintainability, security, readability, and performance. I look for code duplication, naming, logic clarity, and test coverage.

---

**27. What if a teammate is struggling with a task?**  
- Offer help without judgment
- Pair up and walk through the problem
- Break the problem into smaller chunks
- Involve the team if more eyes are needed

---

**28. How do you approach feature estimation?**  
- Break feature into tasks
- Estimate each based on complexity, not time
- Use story points (Fibonacci scale)
- Account for unknowns and dependencies

---

**29. What’s your communication strategy in a distributed team?**  
- Clear documentation (Confluence, Jira)
- Async updates (Slack, Email)
- Daily syncs/standups
- Scheduled 1-on-1s and retrospectives

---

**30. How do you deal with changing requirements?**  
- Keep code loosely coupled and modular
- Embrace change using Agile practices
- Communicate impact early to stakeholders
- Reprioritize backlog with the Product Owner

---

Let me know if you want these answers in PDF or Markdown format!
---

### 🔹 **Section 3: Advanced Level (30 Questions)**

**Java & Spring Boot**
1. How does Spring handle AOP (Aspect Oriented Programming)?
2. How do you design and implement microservices in Spring Boot?
3. Explain the Circuit Breaker pattern. Have you implemented it?
4. What’s your experience with API Gateways (e.g., Zuul, Spring Cloud Gateway)?
5. How do you version REST APIs?

**Angular**
6. What are Angular lifecycle hooks and their purpose?
7. How do you optimize Angular performance for large applications?
8. How do you write custom pipes and directives?
9. Explain Change Detection in Angular.
10. What is zone.js?

**Cloud & DevOps**
11. How do you monitor applications in GCP?
12. What is Helm and how do you use it with Kubernetes?
13. What is Blue-Green deployment?
14. Explain autoscaling in Kubernetes.
15. How do you handle secrets management in cloud environments?

**Architecture & Patterns**
16. Explain the repository pattern.
17. What’s your approach to service-to-service communication?
18. What are design considerations for a scalable architecture?
19. How do you handle transactional boundaries in microservices?
20. How do you ensure fault tolerance and resilience?

**Testing & Quality**
21. How do you write tests for Angular services?
22. Explain code coverage and tools used.
23. How do you mock external dependencies?
24. What is contract testing in microservices?
25. What are your best practices for testing in CI/CD?

**Leadership & Ownership**
26. How do you lead a feature track?
27. How do you handle production incidents?
28. What metrics do you use to measure feature success?
29. How do you plan for technical debt?
30. How do you advocate for clean code and architecture in a team?

---

### **Section 1: Angular & Frontend (Basic to Advanced)**

1. **What is Angular and why is it used?**  
   Angular is a TypeScript-based frontend framework used for building dynamic single-page applications (SPAs). It offers tools for two-way binding, dependency injection, routing, and more.

2. **What are components in Angular?**  
   Components are the building blocks of Angular apps. Each component has a TypeScript file, HTML template, CSS for styling, and metadata defined in a decorator.

3. **Difference between Template-driven and Reactive forms?**  
   - *Template-driven*: Easy to use, suitable for simple forms. Uses directives in HTML.
   - *Reactive*: More scalable, uses explicit form model in TypeScript.

4. **What is data binding in Angular?**  
   Connecting the template and the component. Types include:
   - Interpolation (`{{ }}`)
   - Property binding (`[property]`)
   - Event binding (`(event)`)
   - Two-way binding (`[(ngModel)]`)

5. **What are services and dependency injection in Angular?**  
   Services hold business logic and can be injected into components using Angular’s dependency injection system.

6. **What is a directive in Angular?**
   - *Structural*: Changes DOM layout (e.g. `*ngIf`, `*ngFor`)
   - *Attribute*: Changes appearance or behavior (e.g. `ngClass`, `ngStyle`)

7. **What is Angular CLI and its advantages?**  
   Angular CLI automates project scaffolding, building, serving, testing, and more.

8. **How does routing work in Angular?**  
   The `RouterModule` maps URLs to components using `Routes`.

9. **How does change detection work in Angular?**  
   Angular’s change detection checks for component data changes and updates the DOM accordingly.

10. **What is Lazy Loading in Angular?**  
    It loads modules only when required, improving performance.

11. **What is an observable in Angular?**  
    Part of RxJS, observables represent streams of data used for asynchronous programming.

12. **What is the role of `ngOnInit()`?**  
    Lifecycle hook that runs once after component initialization.

13. **What is the difference between BehaviorSubject and Subject?**  
    - `Subject`: No initial value, emits to current subscribers.
    - `BehaviorSubject`: Requires initial value and emits last emitted value to new subscribers.

14. **What is ViewChild and ContentChild in Angular?**  
    Used to get references to components/elements within the template (`ViewChild`) or projected content (`ContentChild`).

15. **What is a pipe? How to create custom pipes?**  
    Pipes transform data in templates. Custom pipes implement `PipeTransform`.

16. **How do you test Angular components and services (TDD)?**  
    Use Jasmine/Karma for unit testing, with mocks for services and Angular TestBed.

17. **What is AoT and JiT compilation?**  
    - AoT: Ahead-of-Time (compile during build)
    - JiT: Just-in-Time (compile during runtime)

18. **What is the difference between promises and observables?**  
    - Promise resolves once.  
    - Observable supports multiple values over time and operators like `map`, `filter`.

19. **Explain `switchMap` in RxJS.**  
    Cancels previous observable and switches to new one. Useful in search/autocomplete.

20. **How do you manage state in Angular apps?**  
    Use services or libraries like NgRx, Akita for centralized state management.

21. **What is HttpClient in Angular?**  
    Built-in service to make HTTP calls. Supports interceptors for auth/logging.

22. **What are Angular lifecycle hooks?**  
    Hooks like `ngOnInit`, `ngOnDestroy`, `ngAfterViewInit` let you tap into component life stages.

23. **How do you handle forms validation?**  
    Use `Validators` (required, minLength, pattern etc.) in template-driven or reactive forms.

24. **What are guards in Angular?**  
    Control navigation using `CanActivate`, `CanDeactivate`, `Resolve` etc.

25. **How do you optimize Angular app performance?**  
    Lazy loading, `OnPush` change detection, trackBy in `*ngFor`, reduce DOM operations.

26. **What is SSR in Angular?**  
    Server-Side Rendering improves SEO and initial load performance (via Angular Universal).

27. **How do you manage modules and shared components?**  
    Break into feature modules and use `SharedModule` for reusable components/pipes.

28. **How do you handle authentication in Angular?**  
    JWT tokens stored in cookies/localStorage, guarded routes, interceptors for attaching tokens.

29. **What is the use of `Renderer2`?**  
    Provides abstraction for DOM manipulation in a safe, platform-independent way.

30. **What’s your experience with Angular 8+ specific features?**  
    Includes Ivy compiler, differential loading, lazy loading with dynamic imports, etc.

---
