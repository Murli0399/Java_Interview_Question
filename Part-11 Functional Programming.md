<details><summary>

## What is functional programming?
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
</details>
<details><summary>

## Can you give an example of functional programming?
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

## What is a Functional Interface?
</summary>
A functional interface is an interface that has only one abstract method. It is a key concept in functional programming and is used extensively in Java to support lambda expressions and method references.

In Java, functional interfaces are also known as SAM (Single Abstract Method) interfaces or functional types. They provide a way to define and work with functions as objects. By having only one abstract method, functional interfaces can be implemented using lambda expressions or method references, which provide a more concise syntax compared to traditional anonymous inner classes.

Functional interfaces are annotated with the @FunctionalInterface annotation, although it is optional. The purpose of this annotation is to indicate that the interface is intended to be used as a functional interface, and the compiler will enforce that there is only one abstract method within it.

Some of the predefined interfaces in java which can be consider as functional interface :
### java.lang.Comparable: public int compareTo(Object obj);
### java.util.Comparator: public int compare(Object obj1, Object obj2);
### java.lang.Runnable: public void run();
```
@FunctionalInterface
interface Intr{
abstract void sayHello(String name);
}
class X implements Intr{
public void sayHello(String name){
System.out.println("Welcome "+name);
}
public static void main(String[] args) {
Intr i1 = new X();
i1.sayHello("Admin");
}
}
```
</details>
<details><summary>

## What is a stream?
</summary>
This API is also introduced in java 8. This API belongs to java.util.stream package.
The Stream API is used to process collections of objects. A stream is a sequence of objects that supports various methods which can be pipelined to produce the desired result.

java.util.stream package contains some library classes and interfaces by using which we can perform functional style of programming on the group of objects(collection of data).
This API has one main interface:

```
java.util.stream.Stream
```

**Note**:- Object of this Stream interface represents sequence of object from a source like collections.

The feature of java stream:

- The stream does not stores the elements, it only represents elements in a sequence.
Example: wire does not store the electricity.

- It holds only objects, primitives are not allowed.

- Operation(filtering) performed on the stream does not modify its source.
Example: filtering a stream obtained from a source(collection) produces a new stream with the filtered element rather than removing the elements from the source collection.

- With the help of stream obj we can perform various operations on the collection of objects in functional style, like filtering some elements, transform some elements, manipulate, sort, etc.

- Stream is lazy and evaluates code only when required.

- The elements of a stream are only visited once during the life of a stream. a new stream must be generated to revisit the same elements of the source.
</details>
<details><summary>

## Explain about streams with an example?
</summary>
Suppose we have a list of Person objects representing individuals with their names and ages:

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

## What are intermediate operations in streams?
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

## What are terminal operations in streams?
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

## What are method references?
</summary>
Method references in Java provide a way to refer to methods or constructors without invoking them. They are a concise and expressive syntax for passing behavior or referencing methods as functional interfaces.

Java provides a new feature called method reference in Java 8. Method reference is used to refer method of functional interface. It is compact and easy form of lambda expression.

Instead of creating a Lambda Expression with all the details, with the help of method reference we can refer an existing class method to the functional interface implementation, which matches the condition of Lambda Expression.

There are four types of method references in Java:

### Reference to a static method: It references a static method using the 
```
syntax Class::staticMethod.

// Example: Reference to the static method Integer.parseInt(String)
Function<String, Integer> parser = Integer::parseInt;
Integer number = parser.apply("123"); // invokes Integer.parseInt("123")
```
### Reference to an instance method of a particular object: It references an instance method of a specific object using the 
```
syntax object::instanceMethod.

// Example: Reference to the instance method String.length()
String str = "Hello, world!";
Function<String, Integer> lengthGetter = String::length;
Integer length = lengthGetter.apply(str); // invokes str.length()
```
### Reference to an instance method of an arbitrary object of a particular type: It references an instance method of any object of a specific type using the 
```
syntax Class::instanceMethod.

// Example: Reference to the instance method String.toUpperCase()
Function<String, String> upperCaseConverter = String::toUpperCase;
String result = upperCaseConverter.apply("hello"); // invokes "hello".toUpperCase()
```
### Reference to a constructor: It references a constructor of a class using the 
```
syntax ClassName::new.

// Example: Reference to the constructor of ArrayList
Supplier<List<String>> listSupplier = ArrayList::new;
List<String> list = listSupplier.get(); // invokes new ArrayList<>()
```
Method references are particularly useful when working with functional interfaces, such as in the context of streams or functional programming in general. They allow you to pass method references as arguments to higher-order functions or assign them to functional interface variables.

Overall, method references provide a concise and readable way to refer to existing methods or constructors without the need to explicitly define lambda expressions.
</details>
<details><summary>

## What are lambda expressions?
</summary>
Lambda expression is, essentially, an anonymous or unnamed method. The lambda expression does not execute on its own. Instead, it is used to implement a method defined by a functional interface.

Using Lambda Expression we can represent an object of a functional interface in much more concise way.

Lambda Expression saves a lot of code. In case of lambda expression, we don't need to define the method again for providing the implementation. Here, we just write the implementation code.
Java lambda expression is treated as a function, so compiler does not create .class file.

Java lambda expression is consisted of three components.
**1) Argument-list:** It can be empty or non-empty as well.
**2) Lambda operator:** **→** It is used to link arguments-list and body of expression.
**3) Body:** It contains expressions and statements for lambda expression.

Lambda expressions can be used in various contexts, such as:

**1. Functional interfaces:** Lambda expressions can be used to provide an implementation for functional interfaces, which are interfaces that have exactly one abstract method. This allows you to write more concise code when working with functional interfaces, such as in streams, threads, or event handling.

**2. Higher-order functions:** Lambda expressions can be passed as arguments to methods or assigned to variables, enabling you to create higher-order functions that take behavior as input.

**3. Stream operations:** Lambda expressions are commonly used with stream operations to specify transformations, filters, or aggregations on streams of data.
</details>
<details><summary>

## Can you give an example of lambda expression?
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

## Can you explain the relationship between lambda expression and functional interfaces?
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

## Can you give examples of functional interfaces with multiple arguments?
</summary>
While functional interfaces are defined as having a single abstract method, it is still possible to work with multiple arguments by leveraging Java's support for functional interfaces with default methods or by using predefined functional interfaces from the Java API. Here are a few examples:

### Consumer<T, U>:
```
import java.util.function.BiConsumer;

public class ConsumerExample {
    public static void main(String[] args) {
        BiConsumer<String, Integer> printLength = (str, length) -> System.out.println(str + " has length: " + length);
        printLength.accept("Hello", 5);
    }
}
```
In this example, we use the BiConsumer functional interface, which takes two arguments (String and Integer) and performs an action without returning a value. The accept() method is used to consume the arguments and print the length of the string.

### BiFunction<T, U, R>:
```
import java.util.function.BiFunction;

public class BiFunctionExample {
    public static void main(String[] args) {
        BiFunction<Integer, Integer, Integer> multiply = (a, b) -> a * b;
        int result = multiply.apply(4, 5);
        System.out.println("Result: " + result);
    }
}
```
Here, the BiFunction functional interface takes two arguments (Integer and Integer) and returns a result (Integer). The apply() method is used to apply the multiplication operation on the arguments and obtain the result.
</details>
<details><summary>

## What is a Function Functional Interface?
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

## What is a Predicate Functional Interface?
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

## What is a Consumer Functional Interface?
</summary>
It represents a function which takes in one argument and produces a result. However these kind of functions don’t return any value.

```
public void accept(T t);
```
### Example:
```
import java.util.function.Consumer;
public class Main {
    public static void main(String[] args) {
        Consumer<Student> c = s -> {
            System.out.println("Roll is "+s.getRoll());
            System.out.println("Name is "+s.getName());
            System.out.println("Marks is "+s.getMarks());
        };
        c.accept(new Student(10,"Amit",850));
    }
}
```
</details>
<details><summary>

## What is a Supplier Functional Interface?
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