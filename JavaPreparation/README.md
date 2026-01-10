# 🚀 Java to Spring Boot - Complete Learning Path

> A structured roadmap from **Core Java** to **Production-Ready Spring Boot Applications**

---

## 📋 Overview

| Phase | Topic | Duration | Priority |
|-------|-------|----------|----------|
| 1 | Java Fundamentals | 1-2 weeks | 🔴 Critical |
| 2 | Object-Oriented Programming | 1-2 weeks | 🔴 Critical |
| 3 | Exception Handling | 3-4 days | 🔴 Critical |
| 4 | Core Java APIs | 1-2 weeks | 🔴 Critical |
| 5 | Java 8+ Features | 1 week | 🔴 Critical |
| 6 | Multithreading Basics | 3-4 days | 🟡 Important |
| 7 | I/O Basics | 2-3 days | 🟡 Important |
| 8 | JDBC | 3-4 days | 🟡 Important |
| 9 | Build Tools (Maven) | 2-3 days | 🔴 Critical |
| 10 | Spring Core | 1 week | 🔴 Critical |
| 11 | Spring Boot | 2-3 weeks | 🔴 Critical |
| 12 | Testing | 3-4 days | 🟡 Important |

**Total Estimated Time:** 10-14 weeks (with practice)

---

## **Phase 1: Java Fundamentals** 🏗️

> 👉 *Master these before moving ahead*

### 1.1 Java Introduction
- What is Java & Why it's popular
- Java Features (Platform Independent, OOP, Secure, Robust)
- JDK vs JRE vs JVM
- How Java code executes (Compilation → Bytecode → JVM)

### 1.2 Environment Setup
- Install JDK (Java 17+ recommended)
- IDE Setup (IntelliJ IDEA / VS Code)
- First "Hello World" program
- \`javac\` and \`java\` commands

### 1.3 Data Types & Variables
- **Primitive Types:** \`byte\`, \`short\`, \`int\`, \`long\`, \`float\`, \`double\`, \`char\`, \`boolean\`
- **Reference Types:** Objects, Arrays, Strings
- **Variable Types:**
  - Local variables (inside methods)
  - Instance variables (object-level)
  - Static/Class variables (class-level)
- Type casting (implicit & explicit)

### 1.4 Operators
- Arithmetic: \`+\`, \`-\`, \`*\`, \`/\`, \`%\`
- Relational: \`==\`, \`!=\`, \`>\`, \`<\`, \`>=\`, \`<=\`
- Logical: \`&&\`, \`||\`, \`!\`
- Assignment: \`=\`, \`+=\`, \`-=\`, etc.
- Ternary: \`condition ? value1 : value2\`

### 1.5 Control Flow
- **Conditionals:** \`if\`, \`if-else\`, \`else-if ladder\`, \`switch\`
- **Loops:** \`for\`, \`while\`, \`do-while\`, enhanced \`for-each\`
- **Jump Statements:** \`break\`, \`continue\`, \`return\`

### 1.6 Arrays
- Single-dimensional arrays
- Multi-dimensional arrays (2D arrays)
- Array declaration, initialization, iteration
- Common operations (length, sorting, searching)

### 1.7 Methods
- Method declaration & invocation
- Parameters & return types
- Method overloading
- Variable arguments (var-args): \`method(int... nums)\`
- Command-line arguments (\`String[] args\`)

**🎯 Practice:** Write programs for patterns, factorial, prime numbers, array operations

---

## **Phase 2: Object-Oriented Programming (OOP)** 🎭

> 👉 *Foundation for Spring Framework - Master this!*

### 2.1 Classes & Objects
- Class as a blueprint
- Object creation with \`new\`
- Instance variables & methods
- Memory allocation (Heap vs Stack)

### 2.2 Constructors
- Default constructor
- Parameterized constructor
- Constructor overloading
- Constructor chaining (\`this()\`)
- Copy constructor

### 2.3 Encapsulation
- Private fields + Public getters/setters
- Data hiding benefits
- JavaBeans convention

### 2.4 Inheritance (IS-A)
- \`extends\` keyword
- Single & multilevel inheritance
- \`super\` keyword (accessing parent)
- Constructor chaining with \`super()\`
- Method overriding (\`@Override\`)
- \`final\` keyword (class, method, variable)

### 2.5 Polymorphism
- **Compile-time:** Method overloading
- **Runtime:** Method overriding + Dynamic dispatch
- Upcasting & Downcasting
- \`instanceof\` operator

### 2.6 Abstraction
- **Abstract Classes:**
  - \`abstract\` keyword
  - Abstract vs concrete methods
  - When to use
- **Interfaces:**
  - \`interface\` keyword
  - Multiple inheritance with interfaces
  - \`default\` and \`static\` methods (Java 8+)
  - Functional interfaces

### 2.7 Composition (HAS-A)
- Object as instance variable
- Composition vs Inheritance
- Loose coupling benefits

### 2.8 Access Modifiers
| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| \`public\` | ✅ | ✅ | ✅ | ✅ |
| \`protected\` | ✅ | ✅ | ✅ | ❌ |
| \`default\` | ✅ | ✅ | ❌ | ❌ |
| \`private\` | ✅ | ❌ | ❌ | ❌ |

### 2.9 Static Members
- Static variables (shared across objects)
- Static methods (called without object)
- Static blocks (initialization)
- Static nested classes

### 2.10 Packages
- Package declaration & import
- Built-in packages (\`java.lang\`, \`java.util\`, etc.)
- Creating custom packages
- Access control with packages

**🎯 Practice:** Build a mini Bank Account system, Employee Management with inheritance

---

## **Phase 3: Exception Handling** ⚠️

> 👉 *Essential for robust backend applications*

### 3.1 Exception Basics
- What are exceptions
- Exception vs Error
- Exception hierarchy (\`Throwable\` → \`Exception\` / \`Error\`)

### 3.2 Exception Types
- **Checked Exceptions:** \`IOException\`, \`SQLException\` (compile-time)
- **Unchecked Exceptions:** \`NullPointerException\`, \`ArrayIndexOutOfBoundsException\` (runtime)

### 3.3 Handling Exceptions
\`\`\`java
try {
    // risky code
} catch (SpecificException e) {
    // handle specific
} catch (Exception e) {
    // handle general
} finally {
    // always executes (cleanup)
}
\`\`\`

### 3.4 Keywords
- \`throw\` - Manually throw an exception
- \`throws\` - Declare exceptions in method signature
- Difference between \`throw\` vs \`throws\`

### 3.5 Custom Exceptions
\`\`\`java
public class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}
\`\`\`

### 3.6 Try-with-Resources (Java 7+)
\`\`\`java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    // auto-closes resource
}
\`\`\`

### 3.7 Best Practices
- Catch specific exceptions first
- Don't catch \`Exception\` or \`Throwable\` generically
- Use meaningful messages
- Log exceptions properly
- Don't swallow exceptions silently

**🎯 Practice:** Create custom exceptions for a validation system

---

## **Phase 4: Core Java APIs** 📚

### 4.1 java.lang Package

#### Object Class Methods
- \`toString()\` - String representation
- \`equals()\` & \`hashCode()\` - Object comparison (contract!)
- \`getClass()\` - Runtime class info
- \`clone()\` - Object copying

#### String Handling
- String immutability & String Pool
- String methods: \`length()\`, \`charAt()\`, \`substring()\`, \`split()\`, \`trim()\`, \`replace()\`
- \`StringBuilder\` (mutable, not thread-safe) - **Use this!**
- \`StringBuffer\` (mutable, thread-safe)
- String formatting & concatenation

#### Wrapper Classes
- \`Integer\`, \`Double\`, \`Boolean\`, \`Character\`, etc.
- Autoboxing: \`int\` → \`Integer\`
- Unboxing: \`Integer\` → \`int\`
- Parsing: \`Integer.parseInt()\`, \`Double.parseDouble()\`

### 4.2 Collections Framework 🔥

> 👉 *Heavily used in Spring Boot - Master this!*

#### Collection Hierarchy
\`\`\`
Collection (interface)
├── List (ordered, duplicates allowed)
│   ├── ArrayList (fast read, slow insert/delete)
│   ├── LinkedList (fast insert/delete)
│   └── Vector (legacy, thread-safe)
├── Set (no duplicates)
│   ├── HashSet (unordered, O(1) operations)
│   ├── LinkedHashSet (insertion order)
│   └── TreeSet (sorted)
└── Queue
    ├── PriorityQueue
    └── LinkedList

Map (interface) - Key-Value pairs
├── HashMap (unordered, allows null)
├── LinkedHashMap (insertion order)
├── TreeMap (sorted by keys)
└── Hashtable (legacy, thread-safe)
\`\`\`

#### Essential Operations
\`\`\`java
// List
List<String> list = new ArrayList<>();
list.add("item");
list.get(0);
list.remove("item");
list.size();

// Set
Set<String> set = new HashSet<>();
set.add("item");
set.contains("item");

// Map
Map<String, Integer> map = new HashMap<>();
map.put("key", 1);
map.get("key");
map.containsKey("key");
map.keySet();
map.values();
map.entrySet();
\`\`\`

#### Iteration
\`\`\`java
// For-each
for (String item : list) { }

// Iterator
Iterator<String> it = list.iterator();
while (it.hasNext()) { it.next(); }

// Stream (Java 8+)
list.forEach(item -> System.out.println(item));
\`\`\`

#### Comparable vs Comparator
- \`Comparable<T>\` - Natural ordering (\`compareTo()\`)
- \`Comparator<T>\` - Custom ordering (\`compare()\`)

#### Utility Methods
\`\`\`java
Collections.sort(list);
Collections.reverse(list);
Collections.shuffle(list);
Collections.binarySearch(list, key);
\`\`\`

**🎯 Practice:** Implement a phone book using HashMap, sort employees by salary

---

## **Phase 5: Java 8+ Features** ⚡

> 👉 *Mandatory for modern Spring Boot development*

### 5.1 Lambda Expressions
\`\`\`java
// Before Java 8
Runnable r = new Runnable() {
    public void run() { System.out.println("Hello"); }
};

// With Lambda
Runnable r = () -> System.out.println("Hello");

// With parameters
Comparator<String> comp = (a, b) -> a.compareTo(b);
\`\`\`

### 5.2 Functional Interfaces
\`\`\`java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

Calculator add = (a, b) -> a + b;
\`\`\`

#### Built-in Functional Interfaces
| Interface | Method | Use Case |
|-----------|--------|----------|
| \`Predicate<T>\` | \`test(T)\` → boolean | Filtering |
| \`Function<T,R>\` | \`apply(T)\` → R | Transformation |
| \`Consumer<T>\` | \`accept(T)\` → void | Processing |
| \`Supplier<T>\` | \`get()\` → T | Providing values |

### 5.3 Stream API 🔥
\`\`\`java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

// Filter even numbers, square them, sum
int result = numbers.stream()
    .filter(n -> n % 2 == 0)      // 2, 4, 6
    .map(n -> n * n)               // 4, 16, 36
    .reduce(0, Integer::sum);      // 56

// Collect to list
List<Integer> evens = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
\`\`\`

#### Common Stream Operations
- **Intermediate:** \`filter()\`, \`map()\`, \`flatMap()\`, \`sorted()\`, \`distinct()\`, \`limit()\`, \`skip()\`
- **Terminal:** \`collect()\`, \`forEach()\`, \`reduce()\`, \`count()\`, \`findFirst()\`, \`anyMatch()\`, \`allMatch()\`

### 5.4 Method References
\`\`\`java
// Instance method
list.forEach(System.out::println);

// Static method
list.stream().map(String::toUpperCase);

// Constructor
Supplier<List<String>> supplier = ArrayList::new;
\`\`\`

### 5.5 Optional Class
\`\`\`java
Optional<String> opt = Optional.ofNullable(getValue());

// Safe access
String value = opt.orElse("default");
String value = opt.orElseThrow(() -> new RuntimeException("Not found"));

// Conditional processing
opt.ifPresent(v -> System.out.println(v));
\`\`\`

**🎯 Practice:** Process a list of employees using streams - filter, sort, group by department

---

## **Phase 6: Multithreading Basics** 🧵

> 👉 *Conceptual understanding for Spring's async features*

### 6.1 Thread Basics
- Process vs Thread
- Thread lifecycle: New → Runnable → Running → Blocked → Terminated

### 6.2 Creating Threads
\`\`\`java
// Extending Thread
class MyThread extends Thread {
    public void run() { /* task */ }
}

// Implementing Runnable (Preferred)
class MyTask implements Runnable {
    public void run() { /* task */ }
}
Thread t = new Thread(new MyTask());

// Lambda
Thread t = new Thread(() -> System.out.println("Running"));
\`\`\`

### 6.3 Thread Methods
- \`start()\`, \`run()\`, \`sleep()\`, \`join()\`, \`yield()\`
- \`interrupt()\`, \`isAlive()\`

### 6.4 Synchronization
\`\`\`java
synchronized void method() { /* thread-safe */ }

synchronized(lockObject) {
    // critical section
}
\`\`\`

### 6.5 Executor Framework (Important for Spring)
\`\`\`java
ExecutorService executor = Executors.newFixedThreadPool(5);
executor.submit(() -> doTask());
executor.shutdown();
\`\`\`

---

## **Phase 7: Java I/O Basics** 📁

### 7.1 File Operations
\`\`\`java
// Reading
BufferedReader reader = new BufferedReader(new FileReader("file.txt"));
String line;
while ((line = reader.readLine()) != null) {
    System.out.println(line);
}

// Writing
BufferedWriter writer = new BufferedWriter(new FileWriter("file.txt"));
writer.write("Hello");
\`\`\`

### 7.2 NIO.2 (Java 7+)
\`\`\`java
Path path = Paths.get("file.txt");
List<String> lines = Files.readAllLines(path);
Files.write(path, lines);
\`\`\`

### 7.3 Serialization (Concept)
- Converting object to byte stream
- \`Serializable\` interface
- \`transient\` keyword

---

## **Phase 8: JDBC** 🗄️

> 👉 *Understand before Spring Data JPA*

### 8.1 JDBC Steps
\`\`\`java
// 1. Load driver (optional in modern JDBC)
// 2. Get connection
Connection conn = DriverManager.getConnection(url, user, password);

// 3. Create statement
PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE id = ?");
ps.setInt(1, userId);

// 4. Execute query
ResultSet rs = ps.executeQuery();

// 5. Process results
while (rs.next()) {
    String name = rs.getString("name");
}

// 6. Close resources
rs.close(); ps.close(); conn.close();
\`\`\`

### 8.2 Key Concepts
- \`Statement\` vs \`PreparedStatement\` (use PreparedStatement!)
- SQL injection prevention
- Transaction management (\`commit()\`, \`rollback()\`)
- Connection pooling (concept)

---

## **Phase 9: Build Tools - Maven** 🔧

> 👉 *Required for all Spring Boot projects*

### 9.1 Maven Basics
- What is Maven (Build + Dependency Management)
- Project structure:
  \`\`\`
  project/
  ├── src/main/java/       # Source code
  ├── src/main/resources/  # Config files
  ├── src/test/java/       # Test code
  └── pom.xml              # Project config
  \`\`\`

### 9.2 pom.xml Structure
\`\`\`xml
<project>
    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>3.2.0</version>
        </dependency>
    </dependencies>
</project>
\`\`\`

### 9.3 Maven Commands
\`\`\`bash
mvn clean           # Clean target folder
mvn compile         # Compile source
mvn test            # Run tests
mvn package         # Create JAR/WAR
mvn install         # Install to local repo
mvn spring-boot:run # Run Spring Boot app
\`\`\`

### 9.4 Maven Lifecycle
\`validate\` → \`compile\` → \`test\` → \`package\` → \`verify\` → \`install\` → \`deploy\`

---

## **Phase 10: Spring Framework Core** 🌱

> 👉 *Foundation - Understand before Spring Boot*

### 10.1 What is Spring
- Lightweight framework for enterprise Java
- Core features: IoC, DI, AOP

### 10.2 Inversion of Control (IoC)
- Container manages object lifecycle
- Objects don't create dependencies themselves
- Spring IoC Container: \`ApplicationContext\`

### 10.3 Dependency Injection (DI)
\`\`\`java
// Without DI (tight coupling)
class UserService {
    private UserRepository repo = new UserRepository(); // Bad!
}

// With DI (loose coupling)
class UserService {
    private UserRepository repo;
    
    @Autowired  // Spring injects dependency
    public UserService(UserRepository repo) {
        this.repo = repo;
    }
}
\`\`\`

#### DI Types
- **Constructor Injection** (Recommended)
- **Setter Injection**
- **Field Injection** (Not recommended)

### 10.4 Spring Annotations

| Annotation | Purpose |
|------------|---------|
| \`@Component\` | Generic Spring-managed bean |
| \`@Service\` | Business logic layer |
| \`@Repository\` | Data access layer |
| \`@Controller\` | Web controller (MVC) |
| \`@RestController\` | REST API controller |
| \`@Configuration\` | Java-based config class |
| \`@Bean\` | Declare bean in config class |
| \`@Autowired\` | Inject dependency |
| \`@Qualifier\` | Specify which bean to inject |
| \`@Value\` | Inject property values |

### 10.5 Bean Scopes
- \`singleton\` (default) - One instance per container
- \`prototype\` - New instance each time
- \`request\` - One per HTTP request
- \`session\` - One per HTTP session

### 10.6 Bean Lifecycle
1. Instantiation
2. Populate properties
3. \`@PostConstruct\` method
4. Bean ready
5. \`@PreDestroy\` method
6. Destruction

---

## **Phase 11: Spring Boot** 🚀

> 👉 *Main Goal - This is what companies use!*

### 11.1 What is Spring Boot
- Opinionated Spring setup
- Auto-configuration
- Embedded server (Tomcat)
- Production-ready features

### 11.2 Creating a Project
- Use [Spring Initializr](https://start.spring.io)
- Select dependencies: Web, JPA, MySQL/H2, Validation, DevTools

### 11.3 Project Structure
\`\`\`
src/
├── main/
│   ├── java/com/example/demo/
│   │   ├── DemoApplication.java      # Main class
│   │   ├── controller/               # REST controllers
│   │   ├── service/                  # Business logic
│   │   ├── repository/               # Data access
│   │   ├── model/                    # Entity classes
│   │   ├── dto/                      # Data Transfer Objects
│   │   └── exception/                # Custom exceptions
│   └── resources/
│       ├── application.properties    # Configuration
│       └── application.yml           # Alternative config
└── test/                             # Test classes
\`\`\`

### 11.4 Main Application
\`\`\`java
@SpringBootApplication  // = @Configuration + @EnableAutoConfiguration + @ComponentScan
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
\`\`\`

### 11.5 Configuration
\`\`\`yaml
# application.yml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: secret
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
\`\`\`

---

### 11.6 REST API Development 🌐

#### Controller
\`\`\`java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping
    public List<User> getAllUsers() {
        return userService.findAll();
    }

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        return userService.findById(id);
    }

    @PostMapping
    public ResponseEntity<User> createUser(@Valid @RequestBody UserDTO userDTO) {
        User created = userService.save(userDTO);
        return ResponseEntity.status(HttpStatus.CREATED).body(created);
    }

    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @Valid @RequestBody UserDTO userDTO) {
        return userService.update(id, userDTO);
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        userService.delete(id);
        return ResponseEntity.noContent().build();
    }
}
\`\`\`

#### HTTP Methods & Status Codes
| Method | Purpose | Success Code |
|--------|---------|--------------|
| GET | Retrieve | 200 OK |
| POST | Create | 201 Created |
| PUT | Update (full) | 200 OK |
| PATCH | Update (partial) | 200 OK |
| DELETE | Remove | 204 No Content |

#### Request Annotations
- \`@RequestParam\` - Query parameters (\`?name=John\`)
- \`@PathVariable\` - URL path variables (\`/users/{id}\`)
- \`@RequestBody\` - JSON body to object
- \`@RequestHeader\` - HTTP headers

---

### 11.7 Spring Data JPA 🗃️

#### Entity
\`\`\`java
@Entity
@Table(name = "users")
public class User {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, length = 100)
    private String name;
    
    @Column(unique = true)
    private String email;
    
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Order> orders;
    
    // Getters, Setters, Constructors
}
\`\`\`

#### Repository
\`\`\`java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    
    // Derived queries
    List<User> findByName(String name);
    Optional<User> findByEmail(String email);
    List<User> findByNameContaining(String keyword);
    
    // Custom query
    @Query("SELECT u FROM User u WHERE u.email LIKE %:domain")
    List<User> findByEmailDomain(@Param("domain") String domain);
    
    // Native query
    @Query(value = "SELECT * FROM users WHERE status = ?1", nativeQuery = true)
    List<User> findByStatus(String status);
}
\`\`\`

#### Service
\`\`\`java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public List<User> findAll() {
        return userRepository.findAll();
    }

    public User findById(Long id) {
        return userRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("User not found"));
    }

    @Transactional
    public User save(UserDTO dto) {
        User user = new User();
        user.setName(dto.getName());
        user.setEmail(dto.getEmail());
        return userRepository.save(user);
    }
}
\`\`\`

---

### 11.8 Validation ✅

\`\`\`java
public class UserDTO {
    
    @NotBlank(message = "Name is required")
    @Size(min = 2, max = 100)
    private String name;
    
    @NotBlank
    @Email(message = "Invalid email format")
    private String email;
    
    @Min(18)
    @Max(120)
    private Integer age;
    
    @Pattern(regexp = "^\\d{10}$", message = "Phone must be 10 digits")
    private String phone;
}
\`\`\`

---

### 11.9 Exception Handling 🚨

#### Custom Exception
\`\`\`java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
\`\`\`

#### Global Exception Handler
\`\`\`java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
        ErrorResponse error = new ErrorResponse(
            HttpStatus.NOT_FOUND.value(),
            ex.getMessage(),
            LocalDateTime.now()
        );
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, String>> handleValidation(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors()
            .forEach(e -> errors.put(e.getField(), e.getDefaultMessage()));
        return ResponseEntity.badRequest().body(errors);
    }
}
\`\`\`

---

## **Phase 12: Testing** 🧪

### 12.1 JUnit 5 Basics
\`\`\`java
@SpringBootTest
class UserServiceTest {

    @Autowired
    private UserService userService;

    @Test
    void shouldFindUserById() {
        User user = userService.findById(1L);
        assertNotNull(user);
        assertEquals("John", user.getName());
    }
}
\`\`\`

### 12.2 MockMvc for Controllers
\`\`\`java
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void shouldReturnAllUsers() throws Exception {
        when(userService.findAll()).thenReturn(List.of(new User("John")));

        mockMvc.perform(get("/api/users"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$[0].name").value("John"));
    }
}
\`\`\`

---

## ✅ Final Outcome

After completing this roadmap, you will be able to:

| Skill | Level |
|-------|-------|
| Build REST APIs | ✅ Production-ready |
| Database operations with JPA | ✅ CRUD + Custom queries |
| Input validation | ✅ Complete |
| Exception handling | ✅ Global handlers |
| Unit testing | ✅ Basic coverage |
| Project structure | ✅ Industry standard |

### 🎯 Capstone Project Ideas
1. **User Management System** - CRUD + Authentication
2. **E-Commerce Backend** - Products, Orders, Cart
3. **Blog REST API** - Posts, Comments, Categories
4. **Task Manager** - Tasks, Users, Assignments

---

## 📚 Recommended Resources

- **Documentation:** [Spring Boot Docs](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- **Practice:** Build mini-projects after each phase
- **Video:** Java Brains, Amigoscode, Telusko

---

> 💡 **Tip:** Don't rush. Spend time practicing each phase before moving ahead. Build small projects to reinforce learning.
