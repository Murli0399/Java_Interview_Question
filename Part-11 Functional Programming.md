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