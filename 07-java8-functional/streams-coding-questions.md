# Java 8 Streams: Coding Questions

Very common in Java backend interviews: "solve this with streams". Each answer below compiles on Java 17+ (`toList()` needs Java 16+; use `collect(Collectors.toList())` on Java 8).

Sample data used below:

```java
record Employee(String name, String dept, double salary, int age) {}

List<Employee> emps = List.of(
    new Employee("Asha", "Eng", 120_000, 29),
    new Employee("Ravi", "Eng", 95_000, 34),
    new Employee("Meena", "Sales", 70_000, 41),
    new Employee("Kiran", "Sales", 82_000, 26),
    new Employee("Vikram", "HR", 60_000, 38));
```

<details><summary>

## Find the second highest salary.
</summary>

```java
Optional<Double> second = emps.stream()
    .map(Employee::salary)
    .distinct()
    .sorted(Comparator.reverseOrder())
    .skip(1)
    .findFirst();
System.out.println(second.orElse(null)); // 95000.0
```
</details>

<details><summary>

## Group employees by department and count / average salary.
</summary>

```java
Map<String, Long> countByDept = emps.stream()
    .collect(Collectors.groupingBy(Employee::dept, Collectors.counting()));
// {Eng=2, Sales=2, HR=1}

Map<String, Double> avgByDept = emps.stream()
    .collect(Collectors.groupingBy(Employee::dept, Collectors.averagingDouble(Employee::salary)));
// {Eng=107500.0, Sales=76000.0, HR=60000.0}
```
</details>

<details><summary>

## Find the highest-paid employee in each department.
</summary>

```java
Map<String, Optional<Employee>> topByDept = emps.stream()
    .collect(Collectors.groupingBy(Employee::dept,
             Collectors.maxBy(Comparator.comparingDouble(Employee::salary))));

// without Optional values:
Map<String, Employee> top = emps.stream()
    .collect(Collectors.toMap(Employee::dept, e -> e,
             BinaryOperator.maxBy(Comparator.comparingDouble(Employee::salary))));
```
</details>

<details><summary>

## Count the frequency of each character in a string.
</summary>

```java
String input = "tracxn";
Map<Character, Long> freq = input.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()));
// {t=1, r=1, a=1, c=1, x=1, n=1}
```
</details>

<details><summary>

## Find the first non-repeating character in a string.
</summary>

```java
String s = "swiss";
Character first = s.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
    .entrySet().stream()
    .filter(e -> e.getValue() == 1)
    .map(Map.Entry::getKey)
    .findFirst()
    .orElse(null);
System.out.println(first); // w
```

`LinkedHashMap` keeps the original order; a plain `HashMap` would give a wrong answer.
</details>

<details><summary>

## Find duplicate elements in a list.
</summary>

```java
List<Integer> nums = List.of(4, 2, 7, 2, 9, 4, 4);
Set<Integer> seen = new HashSet<>();
Set<Integer> duplicates = nums.stream()
    .filter(n -> !seen.add(n))      // add() returns false if already present
    .collect(Collectors.toSet());
// [2, 4]
```

(Stateful lambda: fine for a sequential stream; for parallel streams use the `groupingBy` + count approach.)
</details>

<details><summary>

## Partition numbers into even and odd.
</summary>

```java
Map<Boolean, List<Integer>> parts = IntStream.rangeClosed(1, 10).boxed()
    .collect(Collectors.partitioningBy(n -> n % 2 == 0));
// {false=[1, 3, 5, 7, 9], true=[2, 4, 6, 8, 10]}
```
</details>

<details><summary>

## Flatten a list of lists and sort unique words.
</summary>

```java
List<List<String>> tags = List.of(List.of("java", "kafka"), List.of("redis", "java"));
List<String> unique = tags.stream()
    .flatMap(List::stream)
    .distinct()
    .sorted()
    .toList();
// [java, kafka, redis]
```
</details>

<details><summary>

## Join names of employees older than 30, comma-separated.
</summary>

```java
String names = emps.stream()
    .filter(e -> e.age() > 30)
    .map(Employee::name)
    .collect(Collectors.joining(", ", "[", "]"));
// [Ravi, Meena, Vikram]
```
</details>

<details><summary>

## Sum, max and statistics in one pass.
</summary>

```java
DoubleSummaryStatistics stats = emps.stream()
    .mapToDouble(Employee::salary)
    .summaryStatistics();
System.out.println(stats.getMax() + " " + stats.getAverage() + " " + stats.getSum());
```
</details>

<details><summary>

## Reverse each word of a sentence.
</summary>

```java
String sentence = "build backend systems";
String result = Arrays.stream(sentence.split(" "))
    .map(w -> new StringBuilder(w).reverse().toString())
    .collect(Collectors.joining(" "));
// dliub dnekcab smetsys
```
</details>

<details><summary>

## Check whether two strings are anagrams using streams.
</summary>

```java
boolean isAnagram(String a, String b) {
    return a.length() == b.length() &&
        Arrays.equals(a.chars().sorted().toArray(), b.chars().sorted().toArray());
}
System.out.println(isAnagram("listen", "silent")); // true
```
</details>

<details><summary>

## What is the difference between map and flatMap?
</summary>

`map` transforms each element into exactly one element. `flatMap` transforms each element into a stream and flattens them into one stream.

```java
List<String> lines = List.of("a b", "c");
lines.stream().map(l -> l.split(" ")).toList();                      // List<String[]> of 2 arrays
lines.stream().flatMap(l -> Arrays.stream(l.split(" "))).toList();   // [a, b, c]
```
</details>

<details><summary>

## Are streams lazy? What happens without a terminal operation?
</summary>

Yes. Intermediate operations (`filter`, `map`, `sorted`) only build a pipeline; nothing runs until a terminal operation (`collect`, `forEach`, `count`, `findFirst`). Elements flow one at a time through the whole pipeline, and short-circuiting operations stop early.

```java
Stream.of("a", "bb", "ccc")
    .filter(s -> { System.out.println("filter " + s); return s.length() > 1; })
    .findFirst();
// prints: filter a, filter bb   (stops after first match; "ccc" never processed)
```

A stream can be consumed only once; reusing it throws `IllegalStateException`.
</details>

<details><summary>

## When should you avoid parallel streams?
</summary>

Parallel streams use the shared `ForkJoinPool.commonPool()`. Avoid them when:
- Work is small (splitting overhead > benefit).
- Tasks block on IO (they starve the common pool used by the whole JVM, including `CompletableFuture` defaults).
- The source splits poorly (`LinkedList`, `Stream.iterate`).
- Operations have side effects or depend on order.

Good fit: large in-memory arrays/`ArrayList`, CPU-heavy pure functions.
</details>

<details><summary>

## What is Optional and how should you use it?
</summary>

`Optional<T>` makes "maybe no value" explicit in return types.

```java
Optional<User> user = repo.findById(id);
String city = user.map(User::address)
                  .map(Address::city)
                  .orElse("Unknown");

User u = repo.findById(id).orElseThrow(() -> new NotFoundException("User " + id));
```

Avoid: `optional.get()` without a check, `Optional` as a field or method parameter, and `Optional` of collections (return an empty list instead).
</details>
