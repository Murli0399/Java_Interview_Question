# Functional programming

<details><summary>

## [Easy] What is functional programming?
</summary>

Functional programming is a programming paradigm that focuses on using pure functions to structure and solve problems. It is a declarative style of programming where programs are constructed by composing functions, rather than by changing the state of variables.

It is a declarative type of programming style. Its main focus is on “what to solve” in contrast to an imperative style where the main focus is “how to solve”. the functional programming method focuses on results, not the process.

In functional programming, functions are treated as first-class citizens, meaning that they can be bound to names (including local identifiers), passed as arguments, and returned from other functions, just as any other data type can.

Here are some key concepts and features of functional programming in Java:

**1. Pure Functions:** Pure functions are functions that always produce the same output for the same input and have no side effects. They don't modify the state of variables or the program's environment.

**2. Immutability:** Functional programming encourages the use of immutable data structures, where objects cannot be modified once created. Immutable objects are thread-safe and can be easily shared across different parts of the program.

**3. Higher-Order Functions:** In functional programming, functions can take other functions as arguments or return functions as results. This enables the composition of functions and promotes code reuse.

**4. Lambda Expressions:** Lambda expressions provide a concise syntax for defining anonymous functions. They allow you to write functional interfaces inline, reducing the need for verbose anonymous inner classes.

**5. Streams:** The Stream API introduced in Java 8 enables functional-style operations on collections of data. Streams provide a way to process data in a declarative manner, allowing operations like filtering, mapping, and reducing.

By incorporating functional programming principles into your Java code, you can write more concise, modular, and maintainable programs. However, it's important to note that Java is a multi-paradigm language, and functional programming is just one aspect of its capabilities.

**Example:**

```java
List<Integer> nums = List.of(1, 2, 3, 4, 5, 6);

// Imperative: how to do it, mutating state
int sum = 0;
for (int n : nums) if (n % 2 == 0) sum += n * n;

// Functional: what to do, no mutation
int sum2 = nums.stream().filter(n -> n % 2 == 0).mapToInt(n -> n * n).sum();  // 56
```

</details>

<details><summary>

## [Easy] Can you give an example of functional programming?
</summary>

import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

```
public class FunctionalProgrammingExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Example 1: Mapping and filtering using streams and lambda expressions
        List<Integer> squaredEvenNumbers = numbers.stream()
                .filter(n -> n % 2 == 0)  // Filter even numbers
                .map(n -> n * n)         // Square each number
                .collect(Collectors.toList());

        System.out.println("Squared even numbers: " + squaredEvenNumbers);

        // Example 2: Summing the squares of even numbers using streams and reduce operation
        int sumOfSquaredEvenNumbers = numbers.stream()
                .filter(n -> n % 2 == 0)  // Filter even numbers
                .map(n -> n * n)         // Square each number
                .reduce(0, Integer::sum); // Sum the squared numbers

        System.out.println("Sum of squared even numbers: " + sumOfSquaredEvenNumbers);
    }
}
```

In this example, we have a list of numbers [1, 2, 3, 4, 5]. We apply functional programming concepts to manipulate and process this list:

- Mapping and Filtering: We use the stream() method to convert the list into a stream of elements. Then, we apply the filter() method to keep only the even numbers and the map() method to square each number. Finally, we collect the results into a new list using collect().

- Summing Squares: We perform the same filtering and mapping operations as before. Then, we use the reduce() method to sum the squared numbers. The reduce() operation takes an initial value (0 in this case) and a binary operator (Integer::sum) to perform the summation.

Both examples demonstrate how functional programming allows us to express the desired operations in a declarative and concise manner, without explicitly iterating over the elements or managing mutable state.
</details>

<details><summary>

## [Easy] What is a Functional Interface?
</summary>

A **functional interface** has **exactly one abstract method** (a SAM – Single Abstract Method – type). Because of that, it can be implemented with a lambda or a method reference. It may still have any number of `default` and `static` methods, and methods inherited from `Object` (like `equals`) don't count.

`@FunctionalInterface` is optional; it makes the compiler fail if someone adds a second abstract method.

```java
@FunctionalInterface
interface Greeter {
	String greet(String name);                       // the single abstract method
	default Greeter twice() { return n -> greet(greet(n)); }
}

Greeter hello = name -> "Hello, " + name;            // lambda implements greet()
System.out.println(hello.greet("Admin"));            // Hello, Admin
```

Built-in examples:
- `java.lang.Runnable` – `void run()`
- `java.util.concurrent.Callable<V>` – `V call() throws Exception`
- `java.util.Comparator<T>` – `int compare(T a, T b)`
- `java.util.function`: `Function<T,R>`, `Predicate<T>`, `Consumer<T>`, `Supplier<T>`, `UnaryOperator<T>`, `BinaryOperator<T>`, `BiFunction<T,U,R>`, and primitive versions such as `IntPredicate`, `ToIntFunction<T>`.

(`Comparable` also has one abstract method, but it is meant to be implemented by the class itself, not written as a lambda.)

</details>

<details><summary>

## [Easy] What is a stream?
</summary>

A **stream** (`java.util.stream.Stream`, Java 8) is a sequence of elements from a source (collection, array, I/O, generator) that you process with a **pipeline** of operations: a source → zero or more **intermediate** operations (`filter`, `map`, `sorted`) → one **terminal** operation (`collect`, `forEach`, `count`).

Key properties:
- **Doesn't store data.** It pulls elements from the source on demand.
- **Doesn't modify the source.** `filter` produces a new stream; the original list is unchanged.
- **Lazy.** Intermediate operations run only when a terminal operation is called, and short-circuiting operations (`findFirst`, `anyMatch`, `limit`) can stop early.
- **Single use.** A stream can be consumed once; reusing it throws `IllegalStateException`.
- **Objects and primitives.** `Stream<T>` holds objects; **`IntStream`, `LongStream` and `DoubleStream`** handle primitives without boxing and add `sum()`, `average()`, `range()`.
- **Can run in parallel** with `parallelStream()` / `.parallel()` (use with care).

```java
List<String> names = List.of("Asha", "Ravi", "Kiran", "Amit");
List<String> result = names.stream()
	.filter(n -> n.startsWith("A"))   // intermediate
	.map(String::toUpperCase)         // intermediate
	.sorted()                         // intermediate
	.toList();                        // terminal -> [AMIT, ASHA]

int total = IntStream.rangeClosed(1, 5).sum();   // 15, primitive stream
```

</details>

<details><summary>

## [Easy] Explain about streams with an example?
</summary>

Suppose we have a list of Person objects representing individuals with their names and ages:

```java
        import java.util.ArrayList;
        import java.util.List;

        class Person {
            private String name;
            private int age;

            public Person(String name, int age) {
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

        public class StreamExample {
            public static void main(String[] args) {
                List<Person> people = new ArrayList<>();
                people.add(new Person("John", 25));
                people.add(new Person("Alice", 32));
                people.add(new Person("Bob", 18));
                people.add(new Person("Emily", 27));
                people.add(new Person("David", 40));
            }
        }
```

Now, let's use streams to perform some operations on this list.

**1. Filtering:** Suppose we want to find all the people who are older than 30. We can use the filter operation to achieve this:

```
List<Person> olderThan30 = people.stream()
        .filter(person -> person.getAge() > 30)
        .collect(Collectors.toList());
```

In this code, we create a stream from the people list, apply a filter operation to keep only the persons whose age is greater than 30, and finally collect the filtered persons into a new list olderThan30.

**2. Mapping:** Suppose we want to extract only the names of the people in the list. We can use the map operation to transform each Person object into its corresponding name:

```
List<String> names = people.stream()
        .map(Person::getName)
        .collect(Collectors.toList());
```

In this example, we use the map operation to convert each Person object into its name using a method reference Person::getName. Finally, we collect the names into a new list.

**3. Aggregation:** Suppose we want to find the average age of all the people in the list. We can use the mapToInt and average operations for this:

```
double averageAge = people.stream()
        .mapToInt(Person::getAge)
        .average()
        .orElse(0.0);
```

Here, we first use the mapToInt operation to convert each Person object into its age as an integer. Then, we apply the average operation to compute the average of all the ages. The orElse(0.0) is used to handle the case where the stream is empty, returning 0.0 as the default value.

These are just a few examples of how streams can be used in Java to filter, transform, and aggregate data. Streams provide a powerful and expressive way to work with collections, allowing you to write more concise and readable code. They also support parallel processing, making it easier to leverage the capabilities of multi-core processors for improved performance.
</details>

<details><summary>

## [Easy] What are intermediate operations in streams?
</summary>

Intermediate operations in streams are operations that transform or filter the elements of a stream. These operations are applied to the elements of the stream in a lazy manner, meaning they are not executed until a terminal operation is encountered.

Intermediate operations are typically chained together to form a pipeline of operations that are applied sequentially to the elements of the stream.

these methods returns a new stream object, these intermediate methods never
gives the final result.

Here are some commonly used intermediate operations in Java streams:

- **filter:** It takes a predicate as an argument and returns a stream consisting of the elements that match the predicate.

```
List<Integer> evenNumbers = numbers.stream()
                                  .filter(n -> n % 2 == 0)
                                  .collect(Collectors.toList());
```

- **map:** It takes a function as an argument and applies the function to each element of the stream, returning a stream of the transformed elements.

```
List<String> names = people.stream()
                           .map(Person::getName)
                           .collect(Collectors.toList());
```

- **distinct:** It returns a stream consisting of the distinct elements of the original stream, removing duplicates.

```
List<Integer> distinctNumbers = numbers.stream()
                                       .distinct()
                                       .collect(Collectors.toList());
```

- **sorted:** It returns a stream with the elements sorted according to the natural order or a provided comparator.

```
List<Integer> sortedNumbers = numbers.stream()
                                     .sorted()
                                     .collect(Collectors.toList());
```

- **limit and skip:** limit returns a stream consisting of the first n elements, while skip discards the first n elements and returns the rest.

```
List<Integer> firstThree = numbers.stream()
                                 .limit(3)
                                 .collect(Collectors.toList());

List<Integer> skipFirstTwo = numbers.stream()
                                    .skip(2)
                                    .collect(Collectors.toList());
```

These are just a few examples of intermediate operations. There are more operations available in the Stream API that can be used to transform, filter, and manipulate the elements of a stream.
</details>

<details><summary>

## [Easy] What are terminal operations in streams?
</summary>

Terminal operations in streams are operations that produce a final result or a side-effect. When a terminal operation is invoked on a stream, it triggers the processing of the stream and consumes the elements of the stream.

Unlike intermediate operations, which are lazy and do not perform any computation until a terminal operation is encountered, terminal operations are eagerly executed.

Here are some commonly used terminal operations in Java streams:

- **forEach:** It performs an action for each element of the stream.

```
numbers.stream()
       .forEach(System.out::println);
```

- **collect:** It accumulates the elements of the stream into a collection or a single value.

```
List<Integer> evenNumbers = numbers.stream()
                                  .filter(n -> n % 2 == 0)
                                  .collect(Collectors.toList());
```

- **count:** It returns the number of elements in the stream.

```
long count = numbers.stream()
                    .count();
```

- **anyMatch, allMatch, and noneMatch:** These operations check if any, all, or none of the elements of the stream match a given predicate, respectively.

```
boolean anyMatch = numbers.stream()
                          .anyMatch(n -> n > 5);

boolean allMatch = numbers.stream()
                          .allMatch(n -> n > 0);

boolean noneMatch = numbers.stream()
                           .noneMatch(n -> n < 0);
```

- **reduce:** It performs a reduction on the elements of the stream using a binary operator and returns an Optional that may contain the reduced value.

```
Optional<Integer> sum = numbers.stream()
                               .reduce((a, b) -> a + b);
```

These are just a few examples of terminal operations. Terminal operations are the final step in a stream pipeline and produce a result or a side-effect. They allow you to consume or transform the elements of a stream into a final output.
</details>

<details><summary>

## [Easy] What are lambda expressions?
</summary>

A **lambda expression** (Java 8) is an anonymous function: a short way to provide the implementation of a **functional interface's** single abstract method. It doesn't run by itself; it becomes an instance of the target interface.

Syntax: `(parameters) -> expression` or `(parameters) -> { statements; }`

```java
Runnable r = () -> System.out.println("run");                    // no parameters
Predicate<String> isEmpty = s -> s.isEmpty();                    // one parameter, no parentheses needed
Comparator<String> byLen = (a, b) -> Integer.compare(a.length(), b.length());
BiFunction<Integer, Integer, Integer> add = (Integer a, Integer b) -> {   // explicit types, block body
	return a + b;
};
```

Three parts: **parameter list**, the arrow **`->`**, and the **body**.

Rules worth knowing:
- Variables captured from the enclosing scope must be **effectively final**.
- `this` inside a lambda refers to the enclosing object (unlike an anonymous class).
- Lambdas aren't compiled into separate `.class` files on disk; the JVM creates the implementation at runtime via `invokedynamic` (`LambdaMetafactory`).

Typical uses: stream operations, comparators, callbacks, `Runnable`/`Callable` tasks, event handlers.

**Example:**

```java
Runnable r = () -> System.out.println("run");                 // no params
Function<String, Integer> len = s -> s.length();              // one param
Comparator<String> byLen = (a, b) -> Integer.compare(a.length(), b.length()); // two params
BiFunction<Integer, Integer, Integer> add = (a, b) -> {
    int result = a + b;                                        // block body
    return result;
};
```

</details>

<details><summary>

## [Easy] Can you give an example of lambda expression?
</summary>

```
interface Calculator {
    int calculate(int a, int b);
}
public class LambdaExample {
    public static void main(String[] args) {
        // Lambda expression as an implementation of the Calculator interface
        Calculator addition = (a, b) -> a + b;
        
        // Using the lambda expression to perform addition
        int result = addition.calculate(5, 3);
        System.out.println(result); // Output: 8
    }
}
```

In this example, we define a functional interface Calculator with a single abstract method calculate that takes two integer parameters and returns an integer. Then, we use a lambda expression (a, b) -> a + b to implement the calculate method.

The lambda expression (a, b) -> a + b represents an anonymous function that takes two integers a and b as parameters and returns their sum. The arrow -> separates the parameter list from the body of the lambda expression, and the body a + b specifies the addition operation.

We create an instance of the Calculator interface using the lambda expression Calculator addition = (a, b) -> a + b;. This allows us to use the lambda expression to perform addition by invoking the calculate method on the addition object.

In the main method, we use the addition object to calculate the sum of 5 and 3 by calling addition.calculate(5, 3). The result is stored in the result variable and printed, yielding 8 as the output.

Lambda expressions provide a concise and expressive way to represent behavior as anonymous functions, making code more readable and enabling functional programming paradigms in Java.
</details>

<details><summary>

## [Easy] Can you explain the relationship between lambda expression and functional interfaces?
</summary>

Lambda expressions and functional interfaces are closely related in Java. Lambda expressions are used to provide an implementation for functional interfaces.

A functional interface is an interface that has exactly one abstract method. It serves as a blueprint for a lambda expression or a method reference. Functional interfaces provide a way to define contracts for functional programming in Java.

Lambda expressions are used to implement the abstract method of a functional interface. They provide a concise and expressive syntax to define behavior inline, without the need for writing a separate class or implementing an interface explicitly.

When a lambda expression is assigned to a functional interface, it becomes an instance of that interface. This allows you to treat the lambda expression as an object and pass it around, assign it to variables, or use it as an argument in methods.

Here's an example to illustrate the relationship between lambda expressions and functional interfaces:

```
interface MyFunction {
    int calculate(int a, int b);
}

public class LambdaAndFunctionalInterface {
    public static void main(String[] args) {
        // Lambda expression as an implementation of the MyFunction functional interface
        MyFunction addition = (a, b) -> a + b;

        // Using the lambda expression to perform addition
        int result = addition.calculate(5, 3);
        System.out.println(result); // Output: 8
    }
}
```

In this example, we define a functional interface MyFunction with a single abstract method calculate. The calculate method takes two integer parameters and returns an integer.

We use a lambda expression (a, b) -> a + b to implement the calculate method of the MyFunction interface. The lambda expression specifies the addition operation by taking two integers a and b and returning their sum.

We create an instance of the MyFunction interface using the lambda expression MyFunction addition = (a, b) -> a + b;. This allows us to use the lambda expression as an object and invoke the calculate method on the addition object.

In the main method, we use the addition object to calculate the sum of 5 and 3 by calling addition.calculate(5, 3). The result is stored in the result variable and printed, yielding 8 as the output.

Lambda expressions enable us to provide a concise implementation of the abstract method of a functional interface, making code more readable and enabling functional programming patterns in Java. They are closely tied to functional interfaces and provide a powerful mechanism for writing code in a more functional and expressive style.
</details>

<details><summary>

## [Easy] What is a Function Functional Interface?
</summary>

This interface defines an abstract method which will takes T type of object as parameter and returns R type of object.

```
public R apply(T t);
```

### Example:

```
import java.util.function.Function;
public class Main {
    public static void main(String[] args) {
        Function<Integer,String> f = i -> "This is a numner "+i;
        System.out.println(f.apply(10));
        Function<String,Integer> f2 = s -> Integer.parseInt(s);
        System.out.println(f2.apply("200")+500);
        Function<String,Integer> f3 = Integer::parseInt;
        System.out.println(f3.apply("400")+200);
    }
}
```

</details>

<details><summary>

## [Easy] What is a Predicate Functional Interface?
</summary>

This interface contains only one abstract method called:

```
public boolean test(T t);
```

This method test() checks whether supplied obj satisfying a condition or not.

### Example:

```
import java.util.function.Predicate;
public class Main {
    public static void main(String[] args) {
        Predicate<Integer> p = i -> i > 0;
        System.out.println(p.test(10));//true
        System.out.println(p.test(-10));//false
    }
}
```

In java 8 Collection interface defines a method called:

```
public boolean removeIf(Predicate filter)
```

Based on the condition of Predicate, this method will remove/filter the elements
from the Collection classes
Example: Removing the Students from the List whose marks is less than 700

```
import java.util.List;
import java.util.ArrayList;
public class Main{
    public static void main(String[] args) {
        List<Student> students=new ArrayList<>();
        students.add(new Student(10, "name1", 650));
        students.add(new Student(12, "name2", 750));
        students.add(new Student(13, "name3", 550));
        students.add(new Student(14, "name4", 820));
        students.add(new Student(15, "name5", 720));
        students.add(new Student(16, "name6", 620));
        System.out.println(students);
        students.removeIf( student -> student.getMarks() < 700 );
        System.out.println(students);
    }
}
```

</details>

<details><summary>

## [Easy] What is a Consumer Functional Interface?
</summary>

`Consumer<T>` takes **one argument and returns nothing**; it is used for side effects such as printing, logging or saving.

```java
public void accept(T t);
```

```java
Consumer<String> log = msg -> System.out.println("[LOG] " + msg);
log.accept("Order placed");

Consumer<String> audit = msg -> System.out.println("[AUDIT] " + msg);
log.andThen(audit).accept("Payment done");   // runs log, then audit

List.of("a", "b").forEach(log);              // Iterable.forEach takes a Consumer
```

Related: `BiConsumer<T, U>` (two arguments, used by `Map.forEach`) and primitive versions like `IntConsumer`.

</details>

<details><summary>

## [Easy] What is a Supplier Functional Interface?
</summary>

It represents a function which does not take in any argument but produces a value of type T.

```
public T get();
```

### Example:

```
import java.util.function.Supplier;
public class Main {
    public static void main(String[] args) {
        Supplier<String> s = () -> "This is from Lambda Expression";
        System.out.println(s.get());
        Supplier<Student> s2 = () -> new Student(10,"Ram",850);
        System.out.println(s2.get().getName());
    }
}
```

</details>

<details><summary>

## [Medium] What are method references?
</summary>

A **method reference** is a shorthand for a lambda that only calls an existing method. The syntax uses `::`. There are four kinds:

| Kind | Syntax | Lambda equivalent |
|---|---|---|
| Static method | `Integer::parseInt` | `s -> Integer.parseInt(s)` |
| Instance method of a **particular object** | `System.out::println`, `greeting::concat` | `x -> System.out.println(x)` |
| Instance method of an **arbitrary object** of a type | `String::toUpperCase` | `s -> s.toUpperCase()` |
| Constructor | `ArrayList::new` | `() -> new ArrayList<>()` |

```java
// 1. Static method
Function<String, Integer> parser = Integer::parseInt;
parser.apply("123");                         // 123

// 2. Instance method of a particular object (the object is fixed)
String prefix = "Hello, ";
Function<String, String> greet = prefix::concat;
greet.apply("Murli");                        // "Hello, Murli"
Consumer<String> printer = System.out::println;

// 3. Instance method of an arbitrary object (the object is the first argument)
Function<String, Integer> length = String::length;
length.apply("backend");                     // 7
BiFunction<String, String, Boolean> eq = String::equalsIgnoreCase;

// 4. Constructor
Supplier<List<String>> listMaker = ArrayList::new;
Function<String, StringBuilder> sbMaker = StringBuilder::new;
```

</details>

<details><summary>

## [Medium] Can you give examples of functional interfaces with multiple arguments?
</summary>

A functional interface has one abstract method, but that method can take several parameters. The JDK provides two-argument versions; for three or more, define your own.

| Interface | Method | Use |
|---|---|---|
| `BiFunction<T, U, R>` | `R apply(T t, U u)` | Two inputs, one result |
| `BiConsumer<T, U>` | `void accept(T t, U u)` | Two inputs, side effect (e.g. `Map.forEach`) |
| `BiPredicate<T, U>` | `boolean test(T t, U u)` | Two inputs, condition |
| `BinaryOperator<T>` | `T apply(T a, T b)` | Two inputs and result of the same type (`reduce`) |

```java
BiConsumer<String, Integer> printLength = (str, len) -> System.out.println(str + " has length " + len);
printLength.accept("Hello", 5);

BiFunction<Integer, Integer, Integer> multiply = (a, b) -> a * b;
System.out.println(multiply.apply(4, 5));                 // 20

BinaryOperator<Integer> max = BinaryOperator.maxBy(Comparator.naturalOrder());

@FunctionalInterface
interface TriFunction<A, B, C, R> { R apply(A a, B b, C c); }   // custom: three arguments
TriFunction<Integer, Integer, Integer, Integer> sum3 = (a, b, c) -> a + b + c;
```

</details>