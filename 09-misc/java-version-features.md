# Java Version Features (5 → 21)

Interviewers usually ask "what's new in Java 8" and "which newer features have you used". Focus on 8, 11, 17 and 21 (the LTS releases).

<details><summary>

## What are the new features in Java 5?
</summary>

- **Generics:** `List<String>` instead of raw `List` with casts
- **Enhanced for loop:** `for (String s : list)`
- **Autoboxing/unboxing:** `Integer i = 5;`
- **Enums**, **varargs** (`void log(String... msgs)`), **annotations** (`@Override`), **static imports**
- **`java.util.concurrent`:** `ExecutorService`, `ConcurrentHashMap`, `AtomicInteger`, locks
</details>

<details><summary>

## What are the new features in Java 6 and 7?
</summary>

**Java 6:** scripting engine API (JSR 223), JDBC 4.0 (drivers auto-loaded), compiler API, performance improvements.

**Java 7:**

```java
// try-with-resources
try (BufferedReader br = Files.newBufferedReader(path)) { return br.readLine(); }

// multi-catch
try { parse(); } catch (IOException | ParseException e) { log(e); }

// diamond operator
Map<String, List<Integer>> m = new HashMap<>();

// strings in switch, underscores in numbers, binary literals
switch (status) { case "ACTIVE": break; }
int million = 1_000_000;  int mask = 0b1010;
```

Also NIO.2 (`Path`, `Files`) and the Fork/Join framework.
</details>

<details><summary>

## What are the new features in Java 8?
</summary>

The biggest release for interviews:

- **Lambdas** and **functional interfaces** (`Function`, `Predicate`, `Supplier`, `Consumer`)
- **Streams API**
- **Method references** (`String::toUpperCase`)
- **Default and static methods in interfaces**
- **Optional**
- **New Date/Time API** (`LocalDate`, `LocalDateTime`, `ZonedDateTime`, `Duration`) – immutable and thread-safe, replacing `Date`/`Calendar`
- **CompletableFuture**
- `ConcurrentHashMap` redesign, `HashMap` buckets become trees on collisions
- Metaspace replaces PermGen

```java
LocalDate due = LocalDate.now().plusDays(30);
long days = ChronoUnit.DAYS.between(LocalDate.of(2026, 1, 1), due);

interface Greeter {
    String name();
    default String greet() { return "Hello, " + name(); }  // default method
}
```
</details>

<details><summary>

## What changed in Java 9, 10 and 11?
</summary>

**Java 9:** module system (JPMS, `module-info.java`), `List.of()/Set.of()/Map.of()` immutable factories, JShell, private interface methods, `Stream.takeWhile/dropWhile`.

**Java 10:** local variable type inference with `var`.

```java
var users = new ArrayList<User>();   // type inferred; still statically typed
```

**Java 11 (LTS):** standard `HttpClient`, new String methods (`isBlank`, `strip`, `lines`, `repeat`), `Files.readString/writeString`, run a single file with `java Main.java`, `var` in lambda parameters.

```java
HttpClient client = HttpClient.newHttpClient();
HttpResponse<String> res = client.send(
    HttpRequest.newBuilder(URI.create("https://api.example.com/health")).build(),
    HttpResponse.BodyHandlers.ofString());
"  ".isBlank();          // true
"ab".repeat(3);          // ababab
```
</details>

<details><summary>

## What are the key features from Java 12 to 17?
</summary>

- **Switch expressions** (14)
- **Text blocks** (15)
- **Records** (16): immutable data carriers with `equals/hashCode/toString` generated
- **Pattern matching for `instanceof`** (16)
- **Sealed classes** (17): restrict which classes can extend a type
- Helpful `NullPointerException` messages (14)
- `Stream.toList()` (16)

```java
record Point(int x, int y) {}

String day = switch (dayNumber) {
    case 1, 7 -> "Weekend";
    case 2, 3, 4, 5, 6 -> "Weekday";
    default -> throw new IllegalArgumentException("Bad day " + dayNumber);
};

if (obj instanceof String s && !s.isBlank()) System.out.println(s.length());

String json = """
    {"name": "Murli", "role": "backend"}
    """;

sealed interface Shape permits Circle, Square {}
record Circle(double r) implements Shape {}
record Square(double side) implements Shape {}
```
</details>

<details><summary>

## What are the key features of Java 21?
</summary>

- **Virtual threads** (final): cheap threads for blocking IO at massive scale
- **Pattern matching for switch** and **record patterns**
- **Sequenced collections:** `getFirst()`, `getLast()`, `reversed()` on `List`, `Deque`, `LinkedHashSet`, `LinkedHashMap`
- Generational ZGC

```java
double area(Shape s) {
    return switch (s) {
        case Circle c -> Math.PI * c.r() * c.r();
        case Square(double side) -> side * side;   // record pattern
    };  // no default needed: Shape is sealed, compiler checks exhaustiveness
}

List<Integer> list = List.of(1, 2, 3);
list.getFirst(); list.getLast(); list.reversed();
```
</details>

<details><summary>

## What is a record and when would you use it?
</summary>

A `record` is a concise, immutable data class. The compiler generates the constructor, accessors (`name()`, not `getName()`), `equals`, `hashCode` and `toString`.

```java
public record UserDto(Long id, String email) {
    public UserDto {                       // compact constructor for validation
        if (email == null || !email.contains("@")) throw new IllegalArgumentException("Bad email");
    }
}
```

Use for DTOs, API responses, events, map keys and value objects. Not for JPA entities (entities need a no-arg constructor and mutable state for Hibernate proxies).
</details>
