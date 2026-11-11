# Extra knowledge (web, DB, OS)

<details><summary>

## [Easy] Difference between API and REST API?
</summary>

An API (Application Programming Interface) is a set of rules that define how applications or devices can connect to and communicate with each other. A REST API is a specific type of API that adheres to the constraints of the REST architectural style. REST stands for Representational State Transfer. REST is a style of web architecture that governs the behavior of clients and servers. REST APIs use HTTP requests to interact with data. Traditional APIs can use a variety of protocols.
REST APIs are also known as RESTful APIs. When a client requests a resource using a REST API, the server transfers back the current state of the resource in a standardized representation.

**Example:**

```java
// REST API in Spring Boot: resources + HTTP verbs + status codes, usually JSON
@RestController
@RequestMapping("/api/users")
class UserController {
    @GetMapping("/{id}") User get(@PathVariable Long id) { ... }          // read
    @PostMapping @ResponseStatus(HttpStatus.CREATED)
    User create(@RequestBody User u) { ... }                               // create
    @DeleteMapping("/{id}") void delete(@PathVariable Long id) { ... }    // delete
}
```

</details>

<details><summary>

## [Easy] What is domain vs. endpoint in API?
</summary>

- **Domain (host):** the address of the server that hosts the API, e.g. `api.example.com`. Together with the scheme and an optional base path it forms the **base URL**: `https://api.example.com/v1`.
- **Endpoint:** a specific URL path plus HTTP method that performs one operation on a resource, e.g. `GET https://api.example.com/v1/users/42` or `POST /v1/orders`.

So one domain hosts many endpoints. In API design, endpoints are usually resource nouns (`/users`, `/orders/{id}/items`), with the action expressed by the HTTP method.

</details>

<details><summary>

## [Easy] Difference between Http and Https?
</summary>

**HTTPS** is HTTP sent over an encrypted **TLS** connection (the successor of SSL). The HTTP protocol itself is the same; HTTPS wraps it in a secure channel.

| | HTTP | HTTPS |
|---|---|---|
| Encryption | None; data travels as plain text | Encrypted with TLS |
| Default port | 80 | 443 |
| Server identity | Not verified | Verified with an X.509 **TLS certificate** signed by a trusted Certificate Authority |
| Integrity | Data can be altered in transit | Tampering is detected |
| Layer | Application layer | Still the application layer (HTTP), running on top of TLS, on top of TCP |
| Performance | No handshake cost | Small TLS handshake cost; with TLS 1.3 and HTTP/2 the difference is negligible |

Modern browsers, APIs and app stores expect HTTPS everywhere. HTTPS protects passwords, tokens and payment data from interception.

</details>

<details><summary>

## [Easy] What is the difference between authentication and authorization in api?
</summary>

Authentication and authorization are two different security functions. Authentication verifies a user's identity, while authorization determines what resources a user can access.

Authentication is the process of verifying a user's identity before granting access to an API. Authorization is the process of determining what resources a user can access.

For example, when you go through security at an airport, you show your ID to authenticate your identity. Authorization is like an airline determining which people can come on board.

Authentication and authorization are often used interchangeably, but they are two separate functions.

**Example:**

```java
// Authentication: who are you? -> 401 if missing/invalid
// Authorization:  are you allowed? -> 403 if not permitted
@GetMapping("/admin/reports")
@PreAuthorize("hasRole('ADMIN')")      // authenticated users without ADMIN get 403
public List<Report> reports() { ... }
```

</details>

<details><summary>

## [Easy] Difference between Abstract class vs. interface?
</summary>

- An **abstract class** can have state (instance fields), constructors, and both abstract and concrete methods with any access modifier. A class can extend only one.
- An **interface** defines a contract. It can have abstract, `default`, `static` (Java 8) and `private` (Java 9) methods, but only `public static final` constants and no constructors. A class can implement many interfaces, and an interface can extend many interfaces.
- Abstract classes can have initialization blocks; interfaces can't.

Use an abstract class to share code and state among closely related classes; use an interface for a capability that unrelated classes can provide. (See the full comparison table in `02-oops/oops-basics.md`.)

</details>

<details><summary>

## [Easy] Difference between heap and stack memory?
</summary>

| | Stack | Heap |
|---|---|---|
| What it stores | Method frames: local primitives, references, return addresses | All objects and arrays |
| Ownership | **One stack per thread** | **Shared** by all threads |
| Lifetime | Frame is popped when the method returns (LIFO) | Objects live until they're unreachable and the GC reclaims them |
| Size | Small (typically 512 KB–1 MB per thread, `-Xss`) | Large (`-Xms` / `-Xmx`) |
| Speed | Very fast allocation | Slower, managed by GC |
| Error when full | `StackOverflowError` (e.g. deep recursion) | `OutOfMemoryError: Java heap space` |
| Thread safety | Naturally thread-safe (private to the thread) | Needs synchronization for shared mutable objects |

```java
void handle() {
	int retries = 3;                 // stack
	Order order = new Order(42);     // reference on the stack, Order object on the heap
}
```

The JIT can sometimes avoid heap allocation for objects that never escape a method (escape analysis), but conceptually objects live on the heap.

**Example:**

```java
void handle() {
    int retries = 3;                    // stack (primitive local)
    Order order = new Order(42);        // 'order' reference on stack, Order object on heap
    process(order);                     // new stack frame; same heap object shared
}                                       // frame popped; Order collectable once unreachable
// StackOverflowError: too-deep recursion. OutOfMemoryError: Java heap space: too many live objects.
```

</details>

<details><summary>

## [Easy] What is JSON? How is it utilized?
</summary>

JSON (JavaScript Object Notation) is a text-based format for storing and transporting data. It is often used when data is sent from a server to a web page or browser. JSON is a lightweight format that is easy to read and write. It is also easy for software to parse and generate.

JSON is used as an alternative to Extensible Markup Language (XML). It was introduced in the early 2000s as part of JavaScript. Today, 
JSON is the universal standard of data exchange.

JSON is used for:
- Exchanging data between web clients and web servers
- Transmitting data in web applications
- Serializing structured data and exchanging it over a network

JSON is a language-independent data format that supports almost every kind of language, framework, and library.

**Example:**

```java
record User(Long id, String name) {}

ObjectMapper mapper = new ObjectMapper();
String json = mapper.writeValueAsString(new User(1L, "Asha"));  // {"id":1,"name":"Asha"}
User u = mapper.readValue("{\"id\":2,\"name\":\"Ravi\"}", User.class);
// Spring Boot does this automatically for @RequestBody / @RestController return values.
```

</details>

<details><summary>

## [Easy] What is the usage of the PATH variable in an operating system? How is it utilized, when would you like to update it?
</summary>

The PATH variable is an environment variable that contains a list of directories the operating system checks before running a command. The PATH variable makes it easy to run commonly used programs located in their own folders. Updating the PATH variable allows you to run any executables found in the directories mentioned in PATH from any directory without typing the absolute file path.

The system-wide default is set in files such as `/etc/profile` or `/etc/environment`. Order matters: the first matching executable in PATH wins, so never put writable or untrusted directories (like `.`) at the front. Each user normally sets PATH in `~/.profile`, `~/.bashrc` or `~/.zshrc`. Update it when you install a tool (for example a new JDK) and want to run its commands from any directory, e.g. `export PATH="$JAVA_HOME/bin:$PATH"`.

If used unwisely, the value of the PATH variable can slow down the operating system by searching too many locations, or invalid locations.
</details>

<details><summary>

## [Easy] What is the difference between a database view and a table in a database?
</summary>

A database view is a virtual table that is extracted from a database. A table is an actual table that exists in physical locations. A view is a subset of a database and is based on a query that runs on one or more database tables. A view is used to query certain data present in different tables. A table is an independent data object that stores the data of a database.

Here are some differences between a view and a table:
- A view depends on the table.
- A view is a virtual table, it does not occupy storage space.
- A table is structured with columns and rows.
- A table is an independent data object.
- A table holds the basic user data and instances of defined objects.
- A view is used to query certain data present in different tables.

**Example:**

```sql
CREATE VIEW active_customers AS
SELECT id, name, email FROM customers WHERE status = 'ACTIVE';

SELECT * FROM active_customers WHERE name LIKE 'A%';   -- queried like a table
```

The view stores only the query; the data stays in `customers`. A **materialized view** stores the result and must be refreshed.

</details>

<details><summary>

## [Easy] What all commands in Unix are you aware of? Please explain their usage.
</summary>

Here are some Unix commands and their usage:
- cat: Creates and displays short files
- chmod: Changes permissions
- cd: Changes directory
- cp: Copies files
- date: Displays the system date and time
- ls: Lists the contents of a directory
- man: Gets documentation for any command
- ssh / scp: Log in to a remote machine securely / copy files to it
- tail -f, less: Follow or page through log files
- ps, top, kill: Inspect and stop processes
- df -h, du -sh: Check disk usage
- curl: Call HTTP endpoints from the terminal
- grep: Searches a file

Other Unix commands include:

mv, rm, mkdir, rmdir, ps, kill.

When writing Unix commands, you can follow these general rules:
- Enter commands in lowercase
- Options are often single letters prefixed with a dash (-)
- Options are set off by any number of spaces or tabs

**Example:**

```bash
ls -lah                      # list files with sizes
grep -rn "ERROR" logs/       # search text recursively
tail -f app.log              # follow a log file
ps aux | grep java           # find running Java processes
top -H -p <pid>              # CPU per thread of a process
df -h ; du -sh *             # disk usage
netstat -tulpn / ss -tulpn   # listening ports
curl -i http://localhost:8080/actuator/health
chmod +x run.sh ; kill -15 <pid>
```

</details>

<details><summary>

## [Easy] What is shell scripting? What purpose is it used for?
</summary>

Shell scripting is a computer program that is used to automate repetitive tasks. It is often used by system administrators to save time and increase accuracy. Shell scripts can be used for tasks such as:
- Backing up files
- Monitoring system resources
- Managing user accounts
- Creating command tools
- Manipulating files
- Running programs
- Linking programs together
- Completing batches

Shell scripts are written as a sequence of commands in a file. The file is made up of ASCII text, also called plain text. You can use a text editor to create shell scripts. Some good command line text editors include vim, emacs, and nano.

Shell scripts are easier to write and debug than other programming languages like C or C++. You can transfer the shell script to other UNIX and similar operating systems and execute it.

**Example:**

```bash
#!/usr/bin/env bash
set -euo pipefail                      # stop on errors and undefined vars

LOG_DIR=/var/log/app
find "$LOG_DIR" -name "*.log" -mtime +7 -delete   # delete logs older than 7 days
echo "Cleanup done at $(date)"
```

</details>

<details><summary>

## [Easy] Explain how you can read fields sent in a request from the browser using a servlet.
</summary>

Servlets are classes in a Java web application that handle requests and responses from client browsers. When a form is submitted, the servlet's doPost() method is invoked. The field values are submitted to the servlet as parameters in the HTTP request. You can use the following methods on the request object to get the parameter values: getParameter(, getParameterValues(, getParameterNames(.

The getParameter() method returns the value of a request parameter as a string. If there is no parameter, it returns null. You can use this method when the parameter has a single value.

The getParameterValues() method is used if the parameter appears more than once and returns multiple values. For example, a checkbox.

The getParameterNames() method is used if you want a complete list of all parameters in the current request.
</details>

<details><summary>

## [Easy] Difference between hashmap and hashtable?
</summary>

| | `HashMap` | `Hashtable` |
|---|---|---|
| Thread-safe | No | Yes – every method is `synchronized` (one lock for the whole table) |
| Nulls | One `null` key, any number of `null` values | No `null` keys or values (`NullPointerException`) |
| Iteration | Fail-fast `Iterator` | `Iterator` (fail-fast) and legacy `Enumeration` (not fail-fast) |
| Performance | Faster | Slower due to locking |
| Collision handling (Java 8+) | Buckets turn into balanced trees when large | Linked lists only |
| Status | Modern (Java 1.2, part of the Collections Framework) | Legacy (Java 1.0) |

`Hashtable` is effectively obsolete. Use `HashMap` for single-threaded code and **`ConcurrentHashMap`** when multiple threads share a map; it is thread-safe with much better concurrency than `Hashtable`.

**Example:**

```java
Map<String, String> hm = new HashMap<>();
hm.put(null, "ok");                  // HashMap: one null key, null values allowed; not synchronized

Map<String, String> ht = new Hashtable<>();
// ht.put(null, "x");                // NullPointerException: Hashtable allows no nulls
// Hashtable synchronizes every method (legacy). For thread safety use ConcurrentHashMap.
Map<String, String> chm = new ConcurrentHashMap<>();
```

</details>

<details><summary>

## [Easy] What is constructor chaining?
</summary>

Constructor chaining is the process of calling one constructor from another constructor in the same class. It is used to initialize the object with some default values. Constructor chaining can be done in two ways:

- Using the this() keyword to call the constructor in the same class.
- Using the super() keyword to call the constructor in the parent class.

The following is an example of constructor chaining using the this() keyword:

```
public class Person {

    private String name;
    private int age;

    public Person(String name) {
        this.name = name;
    }

    public Person(String name, int age) {
        this(name); // Chaining to the constructor with one parameter
        this.age = age;
    }

}
```

The following is an example of constructor chaining using the super() keyword:

```
public class Car extends Vehicle {

    private String make;
    private String model;

    public Car(String make, String model) {
        super(make, model); // Chaining to the constructor in the parent class
        this.make = make;
        this.model = model;
    }

}
```

Constructor chaining is a powerful feature that can help to make your code more concise and efficient.
</details>

<details><summary>

## [Medium] What is reflection API in Java?
</summary>

The Java Reflection API is a set of classes and interfaces that allows Java code to examine or modify the runtime behavior of a class at run time. The java.lang.Class class provides many methods that can be used to get metadata, and examine and change the run time behavior of a class. The java.lang and java.lang.reflect packages provide classes for Java reflection.

The Reflection API is mainly used in:
- IDE (Integrated Development Environment) e.g., Eclipse, MyEclipse, NetBeans, etc.
- Debugger
- Test Tools etc.

Here are some examples of how the Reflection API can be used:
- To get information about the fields, methods, and constructors of a class.
- To create instances of classes at runtime.
- To invoke methods at runtime.
- To get and set the values of fields at runtime.
- To override the access control restrictions on classes and members.

The Reflection API is a powerful tool that can be used to do things that would not be possible without it. However, it is important to use it carefully, as it can also be used to do things that could have unintended consequences.

**Example:**

```java
Class<?> clazz = Class.forName("com.example.User");
Object user = clazz.getDeclaredConstructor().newInstance();

Field name = clazz.getDeclaredField("name");
name.setAccessible(true);                  // bypass private
name.set(user, "Asha");

Method greet = clazz.getMethod("greet");
System.out.println(greet.invoke(user));

for (Method m : clazz.getDeclaredMethods()) {
    if (m.isAnnotationPresent(Deprecated.class)) System.out.println(m.getName());
}
```

</details>

<details><summary>

## [Medium] Where is the Java Reflection API used in the Spring Framework?
</summary>

Spring uses reflection throughout its container and web layer:
- **Creating beans:** instantiating classes found by component scanning or declared with `@Bean`.
- **Dependency injection:** calling constructors, setting `@Autowired` fields (even private ones) and invoking setter methods.
- **Reading annotations:** discovering `@Component`, `@Transactional`, `@RequestMapping`, `@Value`, etc. at startup.
- **Calling lifecycle and handler methods:** `@PostConstruct`, `@EventListener`, `@Scheduled`, controller methods mapped to URLs.
- **Data binding:** mapping request parameters and JSON (Jackson) onto objects, and Spring Data mapping rows/documents to entities.
- **AOP proxies:** JDK dynamic proxies and CGLIB subclasses for `@Transactional`, `@Cacheable`, `@Async`.

Because reflection is slow and hard for native compilation, Spring 6 / Boot 3 added **AOT processing**, which generates much of this wiring at build time (used for GraalVM native images).

**Example:**

```java
@Service
class OrderService {
    @Autowired private PaymentClient client;   // Spring sets this private field via reflection
}
// Also: scanning @Component classes, calling @PostConstruct/@EventListener methods,
// binding JSON to objects (Jackson), creating proxies for @Transactional.
```

</details>

<details><summary>

## [Medium] What is the stored procedure in JDBC?
</summary>

A **stored procedure** is a named block of SQL and procedural logic saved **in the database** (written in the database's language, e.g. MySQL's SQL/PSM or Oracle's PL/SQL). It can take **IN**, **OUT** and **INOUT** parameters and return result sets.

In JDBC you call it with a **`CallableStatement`**, using the escape syntax `{call procedure_name(?, ?)}`: set IN parameters with `setXxx`, register OUT parameters with `registerOutParameter`, then `execute()` and read OUT values with `getXxx`.

Pros: fewer network round trips for multi-step logic, logic shared by many applications, permissions at the procedure level. Cons: business logic hidden in the database, harder to version, test and scale, and tied to one database vendor. Spring offers `SimpleJdbcCall` to call procedures with less code.

**Example:**

```java
try (Connection conn = dataSource.getConnection();
     CallableStatement cs = conn.prepareCall("{call get_order_total(?, ?)}")) {
    cs.setLong(1, orderId);                         // IN parameter
    cs.registerOutParameter(2, Types.DECIMAL);      // OUT parameter
    cs.execute();
    BigDecimal total = cs.getBigDecimal(2);
}
```

</details>

<details><summary>

## [Medium] What is a connection pool? How is it used to improve performance in database applications?
</summary>

Opening a database connection is expensive (TCP handshake, TLS, authentication, session setup – often tens of milliseconds). A **connection pool** opens a set of connections up front and **reuses** them: the app borrows a connection, runs its queries, and returns it to the pool instead of closing it.

Benefits:
- Much lower latency per request (no connect cost).
- Caps the number of concurrent connections, protecting the database from overload.
- Health checks, timeouts and recycling of stale connections.

In Spring Boot the default pool is **HikariCP**. Key settings: `maximum-pool-size`, `minimum-idle`, `connection-timeout` (how long a request waits for a free connection), and `max-lifetime`.

A bigger pool is not always faster: the database can only do so much in parallel, and connections held during slow calls (e.g. a remote API call inside a transaction) exhaust the pool. Keep transactions short.

**Example:**

Spring Boot uses **HikariCP** by default:

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/app
    hikari:
      maximum-pool-size: 20       # max connections; size for DB capacity, not request count
      minimum-idle: 5
      connection-timeout: 3000    # ms to wait for a free connection before failing
      max-lifetime: 1800000       # recycle connections before DB/firewall timeouts
```

Pool exhaustion shows as `SQLTransientConnectionException: Connection is not available`; check `hikaricp_connections_pending` metrics, long transactions and slow queries.

</details>

<details><summary>

## [Medium] What is the difference between a ClassCastException and a ClassNotFoundException in Java?
</summary>

| | `ClassCastException` | `ClassNotFoundException` |
|---|---|---|
| Type | **Unchecked** (`RuntimeException`) | **Checked** (`Exception` → `ReflectiveOperationException`) |
| When | Casting an object to a type it isn't an instance of | Loading a class **by name** at runtime when it isn't on the classpath |
| Typical cause | Wrong cast, raw types / unchecked generics, two class loaders loading the same class | Missing JAR or dependency, typo in a class name, wrong JDBC driver name |
| Thrown by | The JVM during a cast | `Class.forName()`, `ClassLoader.loadClass()`, `findSystemClass()` |

```java
Object o = Integer.valueOf(10);
String s = (String) o;                    // ClassCastException: Integer cannot be cast to String

try {
	Class.forName("com.mysql.cj.jdbc.Driver");   // throws if the MySQL driver JAR is missing
} catch (ClassNotFoundException e) {
	System.out.println("Driver not on classpath");
}
```

Related: **`NoClassDefFoundError`** is an `Error` thrown when a class that was present **at compile time** can't be found or initialised at runtime (e.g. a JAR missing from the deployment, or a static initializer that failed earlier).

</details>

<details><summary>

## [Medium] What configurations do you need to make in web.xml to deploy a servlet in a web application?
</summary>

To configure a servlet in web.xml, you need to:
- Define the servlet name and class name using the <servlet> element
- Map the servlet to a URL or URL pattern
- Add initializations and security roles for the servlet
- Define mappings between URL paths and the servlets that handle requests with those paths

The web server uses this configuration to identify the servlet to handle a given request. For example, the doGet() method for HTTP GET requests.

The web.xml file is located in the WEB-INF directory. It does not represent the entire configuration that is available for the web application. Other servlets, filters, and listeners can be defined using programmatic configurations, annotations, and web fragments.
</details>

<details><summary>

## [Medium] Explain how the session is utilized for security implementation. Please explain who creates the session and how is session information exchanged between the browser and server.
</summary>

HTTP is stateless, so after login the server needs a way to recognise the same user on later requests. A **session** does that.

1. The user submits credentials.
2. The **server** validates them and **creates the session**: a server-side record (in memory, Redis, or a database) holding the user's identity and roles.
3. The server generates a random, unguessable **session ID** and sends it to the browser in a `Set-Cookie` header (in Java servlet containers the cookie is named `JSESSIONID`).
4. The **browser automatically sends the cookie** back on every request to that site.
5. The server looks up the session by ID and treats the request as authenticated.
6. On logout or timeout, the server invalidates the session.

Security practices:
- Mark the cookie **`HttpOnly`** (JavaScript can't read it), **`Secure`** (sent only over HTTPS) and **`SameSite`** (limits cross-site sending, helps against CSRF).
- **Regenerate the session ID after login** to prevent session fixation (Spring Security does this by default).
- Use short idle timeouts and server-side invalidation on logout.
- Keep CSRF protection enabled for cookie-based sessions.
- With several app instances, store sessions centrally (Spring Session + Redis) or use sticky sessions.

</details>

<details><summary>

## [Medium] What is meant by an entity-relationship (E-R) model? Explain the terms Entity, Entity Type, and Entity Set in a DBMS.
</summary>

An **E-R model** is a high-level, conceptual way to design a database by describing the things in a domain and how they relate. It is drawn as an **E-R diagram** and later converted into tables.

- **Entity:** one real-world object you store data about, e.g. the student "Asha, roll no. 17".
- **Entity type:** the category/definition, with a name and attributes, e.g. `Student(roll_no, name, age, mobile)`. It becomes a table.
- **Entity set:** the collection of all entities of one type at a point in time, e.g. all students currently stored. It corresponds to the rows of the table.
- **Attributes:** properties of an entity (simple, composite, multi-valued, derived); a **key attribute** uniquely identifies an entity (primary key).
- **Relationships:** associations between entities, with **cardinality** one-to-one, one-to-many or many-to-many (e.g. a Student *enrolls in* many Courses). Many-to-many becomes a join table.
- **Weak entity:** depends on another entity for its identity (e.g. an `OrderItem` belongs to an `Order`).

</details>

<details><summary>

## [Medium] What is a database trigger? How is it used to enforce business rules?
</summary>

A **trigger** is procedural code the database runs **automatically** when a specific event happens on a table:

- **Timing:** `BEFORE`, `AFTER`, or `INSTEAD OF` (the latter mainly on views).
- **Events:** `INSERT`, `UPDATE`, `DELETE` (and in some databases DDL or login events).
- **Granularity:** for each row, or once per statement (depending on the database).

Uses: enforcing rules the application might forget (no negative stock), writing audit/history rows, keeping derived columns or summary tables in sync.

Trade-offs: logic becomes hidden from application developers, harder to test and debug, can slow down writes, and is vendor-specific. Prefer constraints (`CHECK`, `FOREIGN KEY`, `UNIQUE`) for simple rules, and application code or events for business workflows.

**Example:**

```sql
CREATE TRIGGER trg_prevent_negative_stock
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
  IF NEW.stock < 0 THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Stock cannot be negative';
  END IF;
END;
```

Use sparingly: business logic hidden in triggers is hard to test and debug; prefer application code or constraints (`CHECK (stock >= 0)`).

</details>

<details><summary>

## [Medium] How does your computer know what path to take to reach the external server
</summary>

1. **DNS resolution:** the computer asks a DNS resolver (usually from the router/ISP or a public one like 8.8.8.8) to translate the hostname (`api.example.com`) into an IP address. Results are cached in the browser/OS for the record's TTL.
2. **Local or remote?** Using its IP address and subnet mask, the computer decides whether the destination is on the local network. If not, it sends the packet to its **default gateway** (the router), using ARP to find the router's MAC address.
3. **Routing hop by hop:** each router looks up the destination IP in its **routing table** and forwards the packet to the best next hop. Across the internet, ISPs exchange routes using **BGP**.
4. The packet reaches the server; then TCP (and TLS for HTTPS) connections are set up and the request is sent.

`traceroute` (`tracert` on Windows) shows the hops, and `nslookup`/`dig` shows DNS results.

</details>

<details><summary>

## [Medium] What objects are implicitly available in JSP? Explain their usage
</summary>

JSP has **nine implicit objects**, created by the container when it translates the page into a servlet:

| Object | Type | Use |
|---|---|---|
| `request` | `HttpServletRequest` | Request parameters, headers, attributes |
| `response` | `HttpServletResponse` | Set headers, cookies, redirect |
| `out` | `JspWriter` | Write output to the page |
| `session` | `HttpSession` | Per-user data across requests |
| `application` | `ServletContext` | Application-wide data and config |
| `config` | `ServletConfig` | Init parameters for this JSP |
| `pageContext` | `PageContext` | Access to all the others and to the four scopes |
| `page` | `Object` (`this`) | The servlet instance itself (rarely used) |
| `exception` | `Throwable` | Available only in error pages (`isErrorPage="true"`) |

Attributes can be stored in four scopes: page, request, session and application. JSP is legacy today; Spring Boot apps typically use Thymeleaf or a separate front end consuming REST APIs.

</details>

<details><summary>

## [Hard] Handling and fixing 'Out of Memory' exceptions?
</summary>

`OutOfMemoryError` is an **Error** thrown when the JVM can't allocate memory and the GC can't free enough. First read the message, because it tells you which area ran out:

| Message | Cause | Typical fix |
|---|---|---|
| `Java heap space` | Too many live objects, or a leak | Find the leak (heap dump); stream/paginate large data; then size `-Xmx` |
| `GC overhead limit exceeded` | GC runs constantly but frees almost nothing | Same as above – usually a leak or too-small heap |
| `Metaspace` | Too many classes loaded (dynamic proxies, class loader leaks on redeploy) | Fix the leak; raise `-XX:MaxMetaspaceSize` |
| `unable to create native thread` | Too many threads or OS limits | Use bounded thread pools; check `ulimit` |
| `Direct buffer memory` | Off-heap NIO buffers | Tune `-XX:MaxDirectMemorySize`, release buffers |

Steps:
1. Enable `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/dumps`.
2. Analyse the dump with Eclipse MAT or VisualVM (dominator tree, path to GC roots).
3. Fix the root cause: unbounded caches/collections, `ThreadLocal` leaks, loading whole result sets into memory.
4. Only then tune memory: `-Xmx`, or `-XX:MaxRAMPercentage=75` in containers.

Note: PermGen (`-XX:MaxPermSize`) was removed in Java 8 and replaced by Metaspace.

**Example:**

```bash
# capture a heap dump automatically when OOM happens
java -Xmx1g -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/dumps -jar app.jar

# or take one from a running JVM
jcmd <pid> GC.heap_dump /dumps/app.hprof
```

Open the `.hprof` in Eclipse MAT, check the dominator tree for the largest retained objects, and follow the path to GC roots to find who holds them (often an unbounded cache or a static collection).

</details>
