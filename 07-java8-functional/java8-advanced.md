<details><summary>

## [Easy] Explain the Java 8 Date and Time API.
</summary>

`java.time` (Java 8) replaced the old `Date`/`Calendar`/`SimpleDateFormat`, which were mutable, not thread-safe, and confusing (months started at 0).

| Class | Represents | Example |
|---|---|---|
| `LocalDate` | Date without time or zone | Birthday, invoice date |
| `LocalTime` | Time without date or zone | Store opening time |
| `LocalDateTime` | Date + time, no zone | A local appointment |
| `ZonedDateTime` | Date + time + time zone | Meeting across countries |
| `Instant` | A point on the UTC timeline | Timestamps in logs, DB, APIs |
| `Duration` | Time-based amount (seconds, nanos) | Timeout of 30 s |
| `Period` | Date-based amount (years, months, days) | Subscription of 1 month |
| `DateTimeFormatter` | Thread-safe formatting/parsing | `ISO_LOCAL_DATE`, custom patterns |

```java
LocalDate due = LocalDate.of(2026, 11, 3).plusDays(30);
long days = ChronoUnit.DAYS.between(LocalDate.of(2026, 1, 1), due);
ZonedDateTime ist = ZonedDateTime.now(ZoneId.of("Asia/Kolkata"));
Instant now = Instant.now();
String text = due.format(DateTimeFormatter.ofPattern("dd-MM-yyyy"));
Duration timeout = Duration.ofSeconds(30);
```

All classes are **immutable and thread-safe**. Backend best practice: store and transmit **`Instant`/UTC**, and convert to a user's zone only for display.
</details>

<details><summary>

## [Easy] What is the difference between a Collection and a Stream?
</summary>

| | Collection | Stream |
|---|---|---|
| Purpose | **Stores** data | **Processes** data from a source |
| Evaluation | Eager – elements exist in memory | Lazy – computed on demand by the terminal operation |
| Reuse | Iterate as many times as you like | **One-time use** |
| Modification | Add/remove elements | Never modifies the source; produces new results |
| Size | Finite | Can be infinite (`Stream.iterate`, `generate`) with `limit` |
| Iteration | External (`for`, `Iterator`) | Internal (the library iterates; can parallelise) |

A collection is like a DVD (all data stored), a stream is like video streaming (data flows as you watch).
</details>

<details><summary>

## [Easy] What are the main functional interfaces in java.util.function?
</summary>

| Interface | Method | Input → Output | Typical use |
|---|---|---|---|
| `Function<T, R>` | `apply` | T → R | `map` |
| `BiFunction<T, U, R>` | `apply` | T, U → R | `Map.merge`, `compute` |
| `UnaryOperator<T>` | `apply` | T → T | `List.replaceAll` |
| `BinaryOperator<T>` | `apply` | T, T → T | `reduce` |
| `Predicate<T>` | `test` | T → boolean | `filter`, `removeIf` |
| `BiPredicate<T, U>` | `test` | T, U → boolean | |
| `Consumer<T>` | `accept` | T → void | `forEach` |
| `BiConsumer<T, U>` | `accept` | T, U → void | `Map.forEach` |
| `Supplier<T>` | `get` | () → T | `orElseGet`, lazy creation |

Primitive specialisations (`IntPredicate`, `ToIntFunction<T>`, `IntUnaryOperator`, `IntSupplier`, …) avoid boxing. Many have helpful default methods: `Predicate.and/or/negate`, `Function.andThen/compose`, `Consumer.andThen`.
</details>

<details><summary>

## [Medium] What are default methods, and how is the diamond problem resolved?
</summary>

A **default method** (Java 8) is an interface method with a body, marked `default`. It lets library authors add methods to interfaces (like `List.sort`, `Map.forEach`, `Collection.stream`) without breaking existing implementations.

**Diamond problem:** if a class implements two interfaces that both provide a default method with the same signature, the compiler can't choose, so the class **must override it**. Inside the override it can call a specific one with `InterfaceName.super.method()`.

```java
interface Camera { default String capture() { return "photo"; } }
interface Scanner { default String capture() { return "scan"; } }

class SmartDevice implements Camera, Scanner {
	@Override
	public String capture() {                       // required, otherwise compile error
		return Camera.super.capture() + "+" + Scanner.super.capture();
	}
}
```

Resolution rules, in order:
1. **Class wins:** a method in the class or a superclass beats any interface default.
2. **More specific interface wins:** if `B extends A`, B's default overrides A's.
3. Otherwise it's ambiguous and the class must override.
</details>

<details><summary>

## [Medium] Why must variables used in a lambda be effectively final?
</summary>

A lambda can read local variables from the enclosing method only if they're **final or effectively final** (never reassigned after initialisation).

Reasons:
- The lambda may run **later or on another thread**, after the method has returned and its stack frame is gone. So Java captures a **copy** of the value; allowing reassignment would make the copy and the original disagree.
- It prevents data races on local variables.

```java
int threshold = 10;
List<Integer> big = nums.stream().filter(n -> n > threshold).toList();   // OK
// threshold = 20;                // would make the lambda above a compile error

int[] counter = {0};                                // workaround (avoid): mutable holder
nums.forEach(n -> counter[0]++);
long count = nums.stream().count();                 // better: use the stream itself
```

Instance fields and static fields can be modified inside lambdas (they aren't copied), but doing so from parallel streams is a thread-safety bug.
</details>

<details><summary>

## [Medium] What happens with Collectors.toMap() when there are duplicate keys?
</summary>

`Collectors.toMap(keyFn, valueFn)` throws **`IllegalStateException: Duplicate key`** if two elements produce the same key. Provide a **merge function** to decide what to keep, and optionally a map supplier to choose the map type. It also throws `NullPointerException` if a value is `null`.

```java
record Employee(String name, String dept, double salary) {}
List<Employee> emps = List.of(
	new Employee("Asha", "Eng", 120_000),
	new Employee("Ravi", "Eng", 95_000),
	new Employee("Meena", "Sales", 70_000));

// Map<String, String> m = emps.stream().collect(Collectors.toMap(Employee::dept, Employee::name)); // IllegalStateException

Map<String, Double> maxSalary = emps.stream().collect(Collectors.toMap(
	Employee::dept,
	Employee::salary,
	Math::max,                    // merge: keep the higher salary
	TreeMap::new));               // sorted map
// {Eng=120000.0, Sales=70000.0}

Map<String, List<String>> namesByDept = emps.stream().collect(
	Collectors.groupingBy(Employee::dept, Collectors.mapping(Employee::name, Collectors.toList())));
// {Eng=[Asha, Ravi], Sales=[Meena]}  (key order not guaranteed: groupingBy returns a HashMap)
```

If several values per key are expected, `groupingBy` is usually the right collector.
</details>

<details><summary>

## [Medium] What is the difference between map(), flatMap() and peek() in streams?
</summary>

- **`map(f)`** – transforms each element into **exactly one** element.
- **`flatMap(f)`** – transforms each element into a **stream** of zero or more elements and flattens them into one stream.
- **`peek(action)`** – runs an action on each element as it passes through, **without changing** it. Meant for **debugging** (e.g. logging); it's an intermediate operation, so it runs only if a terminal operation pulls elements, and it may not run for elements that short-circuiting or optimisations skip.

```java
List<List<String>> tags = List.of(List.of("java", "kafka"), List.of("redis"));

List<Integer> sizes = tags.stream().map(List::size).toList();             // [2, 1]
List<String> all = tags.stream().flatMap(List::stream).toList();          // [java, kafka, redis]
List<String> upper = all.stream()
	.peek(t -> System.out.println("saw " + t))                             // debugging only
	.map(String::toUpperCase)
	.toList();
```

Don't use `peek` to modify state or for business logic; use `map` (for transformations) or `forEach` (for side effects at the end).
</details>

<details><summary>

## [Medium] What are the different forms of reduce()?
</summary>

`reduce` combines all elements into one result.

```java
List<Integer> nums = List.of(1, 2, 3, 4);

Optional<Integer> sum1 = nums.stream().reduce(Integer::sum);        // 1. no identity -> Optional (empty stream gives empty)
int sum2 = nums.stream().reduce(0, Integer::sum);                   // 2. identity + accumulator -> 10
int totalLength = Stream.of("ab", "cde").reduce(0,                  // 3. identity + accumulator + combiner
	(acc, s) -> acc + s.length(),                                   //    (needed when the result type differs
	Integer::sum);                                                  //     or for parallel streams) -> 5
```

The identity must be neutral for the operation (0 for sum, 1 for product, "" for concatenation), and the operation must be **associative** so parallel streams give the same result. For common cases prefer the specialised methods: `mapToInt(...).sum()`, `max()`, `count()`, `Collectors.joining()`.
</details>
