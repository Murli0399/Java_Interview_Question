# Java Interview Questions

Java interview questions with clear answers and **runnable code examples**, organised by topic, from core Java to concurrency, JVM internals, Java 8–21 features, DSA coding problems and low-level design.

**312 questions** · every answer is collapsible: try to answer first, then click to check.

Companion repo for Spring and Spring Boot: [SpringBoot_Interview_Questions](https://github.com/Murli0399/SpringBoot_Interview_Questions)

## How to use this repo

1. Pick a topic below and read the questions **without opening the answers**.
2. Answer out loud (≈1 minute each), then expand the answer and compare.
3. For `10-dsa-coding`, solve on paper or LeetCode first (links included), then check the solution and complexity.
4. Revisit what you got wrong the day before the interview.

## Suggested preparation order

| If you have… | Focus on |
|---|---|
| 1 day | `04-collections` internals, `05-multithreading`, `07-java8-functional/streams-coding-questions`, `02-oops/solid-and-design-patterns` |
| 1 week | All of the above + `10-dsa-coding` (3–4 problems a day) + `06-jvm-memory-gc` + `09-misc/java-version-features` |
| Experienced (2–5 yrs) | Concurrency, JVM troubleshooting, design patterns, LLD problems, plus the scenario questions in the Spring repo |

## Topics

### Java Basics

<details><summary><b><a href="01-java-basics/java-platform.md">Java platform</a></b> (5 questions)</summary>

- Why is Java so Popular?
- What is Platform Independence?
- What is ByteCode?
- Compare JDK vs JVM VS JRE.
- What is the role of class loader in java ?

</details>

<details><summary><b><a href="01-java-basics/strings.md">Strings</a></b> (7 questions)</summary>

- Are all String’s immutable?
- Where are string values stored in memory?
- Why should you be careful about String Concatenation(+) operator in Loops?
- How do you solve above problem?
- What are differences between String and StringBuffer?
- What are differences between StringBuilder and StringBuffer?
- Can you give examples of different utility methods in String class?

</details>

<details><summary><b><a href="01-java-basics/wrapper-classes-and-casting.md">Wrapper classes and casting</a></b> (8 questions)</summary>

- What are wrapper classes?
- Why do we need Wrapper Classes in Java?
- What are the different ways of creating Wrapper Class Instances?
- What is Auto Boxing?
- What are the advantages of Auto Boxing?
- What is Casting?
- What is Implicit Casting?
- What is Explicit Casting?

</details>


### OOP, SOLID and Design Patterns

<details><summary><b><a href="02-oops/access-and-non-access-modifiers.md">Access and non access modifiers</a></b> (15 questions)</summary>

- What is default class modifier?
- What is private access modifier?
- What is default or package access modifier?
- What is protected access modifier?
- What is public access modifier?
- What access types of variables can be accessed from a Class in Same Package?
- What access types of variables can be accessed from a Class in Different Package?
- What access types of variables can be accessed from a Sub Class in Same Package?
- What access types of variables can be accessed from a Sub Class in Different Package?
- What is the use of a final modifier on a class ?
- What is the use of a final modifier on a method ?
- What is a Final Variable ?
- What is a Final Argument ?
- What happens when a variable is marked as volatile?
- What is a Static Variable ?

</details>

<details><summary><b><a href="02-oops/advanced-oops.md">Advanced OOPs</a></b> (9 questions)</summary>

- What is Polymorphism?
- What is the use of instanceof Operator in Java?
- What is Coupling?
- What is Cohesion?
- What is Encapsulation?
- What is an Inner Class?
- What is a Static Inner Class?
- Can you create an inner class inside a method?
- What is an Anonymous Class?

</details>

<details><summary><b><a href="02-oops/oops-basics.md">OOPs basics</a></b> (32 questions)</summary>

- What is a Class?
- What is an Object?
- What is state of an Object?
- What is behavior of an Object?
- What is the super class of every class in Java?
- Explain about toString method ?
- What is the use of equals method in Java ?
- What are the important things to consider when implementing equals method?
- What is the hashCode method used for in Java?
- Explain inheritance with Examples?
- What is Method Overloading?
- What is Method Overriding?
- Can super class reference variable can hold an object of sub class?
- Is Multiple Inheritance allowed in Java?
- What is an Interface?
- How do you define an Interface?
- How do you implement an interface?
- Can you explain a few tricky things about interfaces?
- Can you extend an interface?
- Can a class extend multiple interfaces?
- What is an Abstract Class?
- When do you use an Abstract Class?
- How do you define an abstract method?
- Compare Abstract Class vs Interface?
- What is a Constructor?
- What is a Default Constructor?
- Will this code compile?
- How do you call a Super Class Constructor from a Constructor?
- Will this code Compile?
- What is the use of this()?
- Can a constructor be called directly from a method?
- Is a super class constructor called even when there is no explicit call from a sub class constructor?

</details>

<details><summary><b><a href="02-oops/solid-and-design-patterns.md">SOLID and design patterns</a></b> (8 questions)</summary>

- Explain the SOLID principles with examples.
- Write a thread-safe Singleton. Which approach is best?
- What is the Factory pattern? Give a real example.
- What is the Builder pattern?
- What is the Strategy pattern?
- What is the Observer pattern?
- What are Adapter, Decorator, Proxy and Template Method?
- Composition vs inheritance: which should you prefer?

</details>


### Exception Handling

<details><summary><b><a href="03-exception-handling/exception-handling.md">Exception handling</a></b> (18 questions)</summary>

- Why is Exception Handling important?
- What design pattern is used to implement Exception handling Features in most languages?
- What is the need for finally block?
- In what scenarios is code in finally not executed?
- Will finally be executed in the program below?
- Is try without a catch is allowed?
- Is try without catch and finally allowed?
- Can you explain the hierarchy of Exception Handling classes?
- What is the difference between Error and Exception?
- What is the difference between Checked Exceptions and Unchecked Exceptions?
- How do you throw an exception from a method?
- What happens when you throw a Checked Exception from a method ?
- What are the options you have to eliminate compilation errors when handling checked exceptions?
- How do you create a Custom Exception?
- How do you handle multiple exception types with same exception handling block?
- Can you explain about try with resources?
- How does try with resources work?
- Can you explain a few Exception Handling Best Practices?

</details>


### Collections

<details><summary><b><a href="04-collections/collections-basics.md">Collections basics</a></b> (27 questions)</summary>

- Why do we need Collections in Java?
- What are the important interfaces in the Collection Hierarchy?
- What are the important methods that are declared in the Collection Interface?
- Can you explain briefly about the List Interface?
- Explain about ArrayList with an example?
- Can an ArrayList have Duplicate elements?
- How do you iterate around an ArrayList using Iterator?
- How do you sort an ArrayList?
- How do you sort elements in an ArrayList using Comparable interface?
- How do you sort elements in an ArrayList using Comparator interface?
- What is Vector class? How is it different from an ArrayList?
- What is LinkedList? How is it different from an ArrayList?
- Can you briefly explain about the Set Interface?
- What are the important interfaces related to the Set Interface?
- What is the difference between Set and SortedSet interfaces?
- Can you give examples of classes that implement the Set Interface?
- What is a HashSet?
- What is a LinkedHashSet? How is different from a HashSet?
- What is a TreeSet? How is different from a HashSet?
- Can you give examples of implementations of NavigableSet?
- Explain briefly about Queue Interface?
- Can you briefly explain about the Map Interface?
- What is difference between Map and SortedMap?
- What is a HashMap?
- What are the different methods in a Hash Map?
- What is a TreeMap? How is different from a HashMap?
- Difference between Comparable and Comparator

</details>

<details><summary><b><a href="04-collections/collections-internals-and-concurrent.md">Collections internals and concurrent</a></b> (20 questions)</summary>

- How does HashMap work internally?
- What is the initial capacity and load factor of a collection?
- Why must HashMap keys be immutable?
- What is the difference between HashMap, LinkedHashMap and TreeMap?
- How do you build an LRU cache with LinkedHashMap?
- What are the important interfaces related to the Queue interface?
- Explain the Deque interface.
- What is a PriorityQueue?
- Explain the BlockingQueue interface and give implementations.
- Can you give an example of the NavigableMap interface?
- What are the important static methods in the Collections class?
- What is the difference between synchronized and concurrent collections?
- How does ConcurrentHashMap work in Java 8+?
- Explain the copy-on-write approach.
- What is the compare-and-swap (CAS) approach?
- What is a Lock? How is it different from synchronized?
- When does a collection throw UnsupportedOperationException?
- What is the difference between fail-fast and fail-safe iterators?
- What are atomic operations and atomic classes in Java?
- Comparable vs Comparator: how do you sort by multiple fields?

</details>


### Multithreading and Concurrency

<details><summary><b><a href="05-multithreading/concurrency-advanced.md">Concurrency advanced</a></b> (14 questions)</summary>

- Describe a few other important methods in threads.
- What are the important methods for inter-thread communication?
- What is the difference between wait() and sleep()?
- Can you write a producer-consumer program with wait and notify?
- Write a program where two threads print odd and even numbers alternately.
- What does volatile guarantee, and what doesn't it?
- What is the Java Memory Model's happens-before relationship?
- How do you prevent deadlocks?
- What is a ThreadPoolExecutor and how do you size it?
- What is CompletableFuture? Give an example.
- What is ThreadLocal and when can it cause a memory leak?
- What are CountDownLatch, CyclicBarrier and Semaphore?
- What is ReadWriteLock?
- What are virtual threads (Java 21)?

</details>

<details><summary><b><a href="05-multithreading/multithreading-basics.md">Multithreading basics</a></b> (14 questions)</summary>

- What is the need for Threads in Java?
- How do you create a thread?
- What are the different states of a Thread?
- What is priority of a thread? How do you change the priority of a thread?
- What is ExecutorService?
- Explain different ways of creating Executor Services?
- How do you check whether an ExecutionService task executed successfully?
- What is Callable? How do you execute a Callable from ExecutionService?
- What is Synchronization of threads ?
- Can you give an example of a Synchronization block ?
- Can a static method be synchronized ?
- What is the use of join methods in threads ?
- What is the use of yield method?
- What is Deadlock ?

</details>


### JVM, Memory and GC

<details><summary><b><a href="06-jvm-memory-gc/gc-and-serialization.md">GC and serialization</a></b> (12 questions)</summary>

- What is a Garbage Collection?
- Can you explain the Garbage Collection with an example?
- When is the Garbage Collection run?
- What are the best practices for Garbage Collection?
- What are Initialization Blocks?
- What is Serialization?
- How do you serialize an object using Serializable interface?
- How do you de-serialize in Java?
- What do you do if only parts of the object have to be serialized?
- How do you serialize a hierarchy of objects?
- Are the constructors in an object invoked when it is de-serialized?
- Are the values of static variables stored when an object is serialized?

</details>

<details><summary><b><a href="06-jvm-memory-gc/jvm-memory-and-performance.md">JVM memory and performance</a></b> (9 questions)</summary>

- What are the memory areas of the JVM?
- How does generational garbage collection work?
- Which garbage collectors are available, and which would you choose?
- Can a Java application have a memory leak? Give examples.
- How do you troubleshoot an OutOfMemoryError or high memory in production?
- How do you diagnose high CPU or a hung Java service?
- Explain class loading and the delegation model.
- What is the difference between strong, soft, weak and phantom references?
- What is JIT compilation?

</details>


### Java 8, Streams and Functional Programming

<details><summary><b><a href="07-java8-functional/functional-programming.md">Functional programming</a></b> (16 questions)</summary>

- What is functional programming?
- Can you give an example of functional programming?
- What is a Functional Interface?
- What is a stream?
- Explain about streams with an example?
- What are intermediate operations in streams?
- What are terminal operations in streams?
- What are method references?
- What are lambda expressions?
- Can you give an example of lambda expression?
- Can you explain the relationship between lambda expression and functional interfaces?
- Can you give examples of functional interfaces with multiple arguments?
- What is a Function Functional Interface?
- What is a Predicate Functional Interface?
- What is a Consumer Functional Interface?
- What is a Supplier Functional Interface?

</details>

<details><summary><b><a href="07-java8-functional/streams-coding-questions.md">Streams coding questions</a></b> (16 questions)</summary>

- Find the second highest salary.
- Group employees by department and count / average salary.
- Find the highest-paid employee in each department.
- Count the frequency of each character in a string.
- Find the first non-repeating character in a string.
- Find duplicate elements in a list.
- Partition numbers into even and odd.
- Flatten a list of lists and sort unique words.
- Join names of employees older than 30, comma-separated.
- Sum, max and statistics in one pass.
- Reverse each word of a sentence.
- Check whether two strings are anagrams using streams.
- What is the difference between map and flatMap?
- Are streams lazy? What happens without a terminal operation?
- When should you avoid parallel streams?
- What is Optional and how should you use it?

</details>


### Generics

<details><summary><b><a href="08-generics/generics.md">Generics</a></b> (7 questions)</summary>

- What are Generics?
- Why do we need Generics? Can you give an example of how Generics make a program more flexible?
- How do you declare a generic class?
- What are the restrictions in using a generic type that is declared in a class declaration?
- How can we restrict Generics to a subclass of a particular class?
- How can we restrict Generics to a superclass of a particular class?
- Can you give an example of a generic method?

</details>


### Miscellaneous and Java Versions

<details><summary><b><a href="09-misc/arrays-enums-misc.md">Arrays enums misc</a></b> (9 questions)</summary>

- What are the default values in an array?
- How do you print the content of an array?
- How do you compare two arrays?
- What is an enum?
- Can you use a switch statement around an enum?
- What are asserts used for?
- When should asserts be used?
- What is tokenizing?
- Can you give an example of tokenizing?

</details>

<details><summary><b><a href="09-misc/extra-knowledge.md">Extra knowledge</a></b> (26 questions)</summary>

- Difference between API and REST API?
- What is domain vs. endpoint in API?
- Difference between Http and Https?
- What is reflection API in Java?
- Where is the Java Reflection API used in the Spring Framework?
- What is the difference between authentication and authorization in api?
- Difference between Abstract class vs. interface?
- Difference between heap and stack memory?
- What is the stored procedure in JDBC?
- What is a connection pool? How is it used to improve performance in database applications?
- Handling and fixing 'Out of Memory' exceptions?
- What is the difference between a ClassCastException and a ClassNotFoundException in Java?
- What is JSON? How is it utilized?
- What is the usage of the PATH variable in an operating system? How is it utilized, when would you like to update it?
- What configurations do you need to make in web.xml to deploy a servlet in a web application?
- Explain how the session is utilized for security implementation. Please explain who creates the session and how is session information exchanged between the browser and server.
- What is the difference between a database view and a table in a database?
- What is meant by an entity-relationship (E-R) model? Explain the terms Entity, Entity Type, and Entity Set in
- What is a database trigger? How is it used to enforce business rules?
- What all commands in Unix are you aware of? Please explain their usage.
- What is shell scripting? What purpose is it used for?
- How does your computer know what path to take to reach the external server
- Explain how you can read fields sent in a request from the browser using a servlet.
- What objects are implicitly available in JSP? Explain their usage
- Difference between hashmap and hashtable?
- What is constructor chaining?

</details>

<details><summary><b><a href="09-misc/java-version-features.md">Java version features (5 → 21)</a></b> (7 questions)</summary>

- What are the new features in Java 5?
- What are the new features in Java 6 and 7?
- What are the new features in Java 8?
- What changed in Java 9, 10 and 11?
- What are the key features from Java 12 to 17?
- What are the key features of Java 21?
- What is a record and when would you use it?

</details>


### DSA, Coding Programs and LLD

<details><summary><b><a href="10-dsa-coding/01-strings.md">Strings</a></b> (6 questions)</summary>

- 1. Check whether a pattern exists in a text (substring search)
- 2. Valid palindrome (ignore case and non-alphanumerics)
- 3. Longest palindromic substring
- 4. Longest substring without repeating characters
- 5. Group anagrams
- 6. String compression

</details>

<details><summary><b><a href="10-dsa-coding/02-arrays-and-hashing.md">Arrays and hashing</a></b> (6 questions)</summary>

- 7. Two sum
- 8. Best time to buy and sell stock (I and II)
- 9. Maximum subarray sum (Kadane's algorithm)
- 10. Merge overlapping intervals
- 11. Product of array except self (no division)
- 12. Subarray sum equals K

</details>

<details><summary><b><a href="10-dsa-coding/03-linked-list-matrix-stack.md">Linked list matrix stack</a></b> (5 questions)</summary>

- 13. Reverse a linked list
- 14. Detect a cycle and return where it starts
- 15. Merge two sorted lists
- 16. Word search in a matrix
- 17. Valid parentheses

</details>

<details><summary><b><a href="10-dsa-coding/04-trees-and-binary-search.md">Trees and binary search</a></b> (4 questions)</summary>

- 18. Level order traversal (BFS)
- 19. Lowest common ancestor of a binary tree
- 20. Search in a rotated sorted array
- Before you say "done" in an interview

</details>

<details><summary><b><a href="10-dsa-coding/05-lld-problems.md">LLD problems</a></b> (3 questions)</summary>

- Design an LRU cache with O(1) get and put
- Design a parking lot
- Design a rate limiter (token bucket)

</details>

<details><summary><b><a href="10-dsa-coding/06-classic-java-programs.md">Classic java programs</a></b> (9 questions)</summary>

- Reverse a string without using reverse()
- Check whether a number is prime
- Fibonacci series (iterative and memoised)
- Check whether two strings are anagrams
- Find the missing number in 1..n
- Move all zeros to the end, keeping order
- Remove duplicates from a sorted array in place
- Print a pattern (Floyd's triangle)
- FizzBuzz

</details>

## Contributing

Found a mistake or want to add a question? Open an issue or a pull request. Keep the existing format:

~~~html
<details><summary>

## Your question?
</summary>

Short answer in your own words.

**Example:**

```java
// minimal code that compiles
```
</details>
~~~

⭐ Star the repo if it helped you prepare.
