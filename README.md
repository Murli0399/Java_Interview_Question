# Java Interview Questions

Java interview questions with clear answers and **runnable code examples**, from core Java to concurrency, JVM internals, Java 8–21 features, DSA coding problems and low-level design.

**369 questions** · 198 Easy · 146 Medium · 25 Hard · every answer is collapsible, so try to answer first, then click to check.

Companion repo for Spring and Spring Boot: [SpringBoot_Interview_Questions](https://github.com/Murli0399/SpringBoot_Interview_Questions)

## Difficulty levels

Every question is tagged by difficulty, and within each file questions run from **Easy → Medium → Hard** (numbered DSA problems keep their order):

| Level | Meaning |
|---|---|
| **[Easy]** | Fundamentals every Java developer is expected to answer (freshers, screening rounds) |
| **[Medium]** | Follow-ups and practical usage (1–3 years of experience) |
| **[Hard]** | Internals, production troubleshooting and design trade-offs (3+ years, senior rounds) |

## How to use this repo

1. Pick a topic and read the questions **without opening the answers**.
2. Answer out loud (about 1 minute each), then expand the answer and compare.
3. For `10-dsa-coding`, solve on paper or LeetCode first (links included), then check the solution and complexity.
4. Revisit the questions you got wrong the day before the interview.

## Suggested study path

| Stage | Focus |
|---|---|
| 1. Foundations | All **[Easy]** questions in `01` to `04`, plus `10-dsa-coding/06-classic-java-programs` |
| 2. Working knowledge | **[Medium]** questions in collections, multithreading, Java 8 streams, exceptions; DSA problems 1–20 |
| 3. Experienced rounds | **[Hard]** questions: HashMap/ConcurrentHashMap internals, JMM and volatile, JVM troubleshooting, generics; DSA 21–33 and LLD |

## Topics

### Java Basics

<details><summary><b><a href="01-java-basics/core-java-essentials.md">Core Java essentials</a></b> (11: 6 Easy · 5 Medium)</summary>

- [Easy] What is the main method signature and why is it public static void?
- [Easy] What does the static keyword mean for variables, methods, blocks and classes?
- [Easy] What is the difference between this and super?
- [Easy] What is the difference between == and equals() for Strings?
- [Easy] What are varargs?
- [Easy] What is the difference between final, finally and finalize?
- [Medium] Is Java pass-by-value or pass-by-reference?
- [Medium] How do you create an immutable class in Java?
- [Medium] What is a marker interface? Give examples.
- [Medium] What is the difference between shallow copy and deep copy? How does clone() work?
- [Medium] What are records and sealed classes, and why were they added?

</details>

<details><summary><b><a href="01-java-basics/java-platform.md">Java platform</a></b> (5: 4 Easy · 1 Medium)</summary>

- [Easy] Why is Java so Popular?
- [Easy] What is Platform Independence?
- [Easy] What is ByteCode?
- [Easy] Compare JDK vs JVM VS JRE.
- [Medium] What is the role of class loader in java ?

</details>

<details><summary><b><a href="01-java-basics/strings.md">Strings</a></b> (7: 4 Easy · 3 Medium)</summary>

- [Easy] Are all String’s immutable?
- [Easy] What are differences between String and StringBuffer?
- [Easy] What are differences between StringBuilder and StringBuffer?
- [Easy] Can you give examples of different utility methods in String class?
- [Medium] Where are string values stored in memory?
- [Medium] Why should you be careful about String Concatenation(+) operator in Loops?
- [Medium] How do you avoid the cost of String concatenation in loops?

</details>

<details><summary><b><a href="01-java-basics/wrapper-classes-and-casting.md">Wrapper classes and casting</a></b> (8: 6 Easy · 2 Medium)</summary>

- [Easy] What are wrapper classes?
- [Easy] Why do we need Wrapper Classes in Java?
- [Easy] What is Auto Boxing?
- [Easy] What is Casting?
- [Easy] What is Implicit Casting?
- [Easy] What is Explicit Casting?
- [Medium] What are the different ways of creating Wrapper Class Instances?
- [Medium] What are the advantages of Auto Boxing?

</details>


### OOP, SOLID and Design Patterns

<details><summary><b><a href="02-oops/access-and-non-access-modifiers.md">Access and non-access modifiers</a></b> (15: 11 Easy · 3 Medium · 1 Hard)</summary>

- [Easy] What is default class modifier?
- [Easy] What is private access modifier?
- [Easy] What is default or package access modifier?
- [Easy] What is public access modifier?
- [Easy] What access types of variables can be accessed from a Class in Same Package?
- [Easy] What access types of variables can be accessed from a Class in Different Package?
- [Easy] What is the use of a final modifier on a class ?
- [Easy] What is the use of a final modifier on a method ?
- [Easy] What is a Final Variable ?
- [Easy] What is a Final Argument ?
- [Easy] What is a Static Variable ?
- [Medium] What is protected access modifier?
- [Medium] What access types of variables can be accessed from a Sub Class in Same Package?
- [Medium] What access types of variables can be accessed from a Sub Class in Different Package?
- [Hard] What happens when a variable is marked as volatile?

</details>

<details><summary><b><a href="02-oops/advanced-oops.md">Advanced OOP</a></b> (9: 5 Easy · 4 Medium)</summary>

- [Easy] What is Polymorphism?
- [Easy] What is the use of instanceof Operator in Java?
- [Easy] What is Coupling?
- [Easy] What is Cohesion?
- [Easy] What is Encapsulation?
- [Medium] What is an Inner Class?
- [Medium] What is a Static Inner Class?
- [Medium] Can you create an inner class inside a method?
- [Medium] What is an Anonymous Class?

</details>

<details><summary><b><a href="02-oops/oops-basics.md">OOP basics</a></b> (32: 26 Easy · 6 Medium)</summary>

- [Easy] What is a Class?
- [Easy] What is an Object?
- [Easy] What is state of an Object?
- [Easy] What is behavior of an Object?
- [Easy] What is the super class of every class in Java?
- [Easy] Explain about toString method ?
- [Easy] Explain inheritance with Examples?
- [Easy] What is Method Overloading?
- [Easy] What is Method Overriding?
- [Easy] Can super class reference variable can hold an object of sub class?
- [Easy] Is Multiple Inheritance allowed in Java?
- [Easy] What is an Interface?
- [Easy] How do you define an Interface?
- [Easy] How do you implement an interface?
- [Easy] Can you extend an interface?
- [Easy] Can a class implement multiple interfaces?
- [Easy] What is an Abstract Class?
- [Easy] When do you use an Abstract Class?
- [Easy] How do you define an abstract method?
- [Easy] What is a Constructor?
- [Easy] What is a Default Constructor?
- [Easy] Will this code compile? (no-arg and one-arg constructors)
- [Easy] How do you call a Super Class Constructor from a Constructor?
- [Easy] What is the use of this()?
- [Easy] Can a constructor be called directly from a method?
- [Easy] Is a super class constructor called even when there is no explicit call from a sub class constructor?
- [Medium] What is the use of equals method in Java ?
- [Medium] What are the important things to consider when implementing equals method?
- [Medium] What is the hashCode method used for in Java?
- [Medium] Can you explain a few tricky things about interfaces?
- [Medium] Compare Abstract Class vs Interface?
- [Medium] Will this code compile? (statement before super())

</details>

<details><summary><b><a href="02-oops/solid-and-design-patterns.md">SOLID and design patterns</a></b> (8: 2 Easy · 6 Medium)</summary>

- [Easy] What is the Factory pattern? Give a real example.
- [Easy] What is the Builder pattern?
- [Medium] Explain the SOLID principles with examples.
- [Medium] Write a thread-safe Singleton. Which approach is best?
- [Medium] What is the Strategy pattern?
- [Medium] What is the Observer pattern?
- [Medium] What are Adapter, Decorator, Proxy and Template Method?
- [Medium] Composition vs inheritance: which should you prefer?

</details>


### Exception Handling

<details><summary><b><a href="03-exception-handling/exception-handling.md">Exception handling</a></b> (18: 13 Easy · 5 Medium)</summary>

- [Easy] Why is Exception Handling important?
- [Easy] What is the need for finally block?
- [Easy] In what scenarios is code in finally not executed?
- [Easy] Will finally be executed in the program below?
- [Easy] Is try without a catch is allowed?
- [Easy] Is try without catch and finally allowed?
- [Easy] Can you explain the hierarchy of Exception Handling classes?
- [Easy] What is the difference between Error and Exception?
- [Easy] What is the difference between Checked Exceptions and Unchecked Exceptions?
- [Easy] How do you throw an exception from a method?
- [Easy] What happens when you throw a Checked Exception from a method ?
- [Easy] How do you create a Custom Exception?
- [Easy] How do you handle multiple exception types with same exception handling block?
- [Medium] What design pattern is used to implement Exception handling Features in most languages?
- [Medium] What are the options you have to eliminate compilation errors when handling checked exceptions?
- [Medium] Can you explain about try with resources?
- [Medium] How does try with resources work?
- [Medium] Can you explain a few Exception Handling Best Practices?

</details>

<details><summary><b><a href="03-exception-handling/exceptions-advanced.md">Exceptions (advanced)</a></b> (8: 1 Easy · 5 Medium · 2 Hard)</summary>

- [Easy] What is the difference between throw and throws?
- [Medium] What happens if both try and finally contain a return statement?
- [Medium] What is exception chaining and why does it matter?
- [Medium] What are the exception rules for method overriding?
- [Medium] When would you create a checked vs an unchecked custom exception?
- [Medium] What is the difference between ClassNotFoundException and NoClassDefFoundError?
- [Hard] What are suppressed exceptions?
- [Hard] What is ExceptionInInitializerError?

</details>


### Collections

<details><summary><b><a href="04-collections/collections-basics.md">Collections basics</a></b> (27: 22 Easy · 5 Medium)</summary>

- [Easy] Why do we need Collections in Java?
- [Easy] What are the important interfaces in the Collection Hierarchy?
- [Easy] What are the important methods that are declared in the Collection Interface?
- [Easy] Can you explain briefly about the List Interface?
- [Easy] Explain about ArrayList with an example?
- [Easy] Can an ArrayList have Duplicate elements?
- [Easy] How do you iterate around an ArrayList using Iterator?
- [Easy] How do you sort an ArrayList?
- [Easy] How do you sort elements in an ArrayList using Comparable interface?
- [Easy] How do you sort elements in an ArrayList using Comparator interface?
- [Easy] What is Vector class? How is it different from an ArrayList?
- [Easy] Can you briefly explain about the Set Interface?
- [Easy] What are the important interfaces related to the Set Interface?
- [Easy] What is the difference between Set and SortedSet interfaces?
- [Easy] Can you give examples of classes that implement the Set Interface?
- [Easy] What is a HashSet?
- [Easy] What is a LinkedHashSet? How is different from a HashSet?
- [Easy] Explain briefly about Queue Interface?
- [Easy] Can you briefly explain about the Map Interface?
- [Easy] What is a HashMap?
- [Easy] What are the different methods in a Hash Map?
- [Easy] Difference between Comparable and Comparator
- [Medium] What is LinkedList? How is it different from an ArrayList?
- [Medium] What is a TreeSet? How is different from a HashSet?
- [Medium] Can you give examples of implementations of NavigableSet?
- [Medium] What is difference between Map and SortedMap?
- [Medium] What is a TreeMap? How is different from a HashMap?

</details>

<details><summary><b><a href="04-collections/collections-comparison-and-complexity.md">Choosing collections and complexity</a></b> (6: 1 Easy · 4 Medium · 1 Hard)</summary>

- [Easy] What is the difference between Iterator and ListIterator?
- [Medium] What is the time complexity of common collection operations?
- [Medium] What is the difference between List.of(), Arrays.asList() and Collections.unmodifiableList()?
- [Medium] How does HashSet work internally?
- [Medium] How do you choose the right collection?
- [Hard] What are EnumMap, WeakHashMap and IdentityHashMap used for?

</details>

<details><summary><b><a href="04-collections/collections-internals-and-concurrent.md">Collections internals and concurrent collections</a></b> (20: 5 Easy · 13 Medium · 2 Hard)</summary>

- [Easy] What is the difference between HashMap, LinkedHashMap and TreeMap?
- [Easy] What are the important interfaces related to the Queue interface?
- [Easy] Explain the Deque interface.
- [Easy] What are the important static methods in the Collections class?
- [Easy] When does a collection throw UnsupportedOperationException?
- [Medium] How does HashMap work internally?
- [Medium] What is the initial capacity and load factor of a collection?
- [Medium] Why must HashMap keys be immutable?
- [Medium] How do you build an LRU cache with LinkedHashMap?
- [Medium] What is a PriorityQueue?
- [Medium] Explain the BlockingQueue interface and give implementations.
- [Medium] Can you give an example of the NavigableMap interface?
- [Medium] What is the difference between synchronized and concurrent collections?
- [Medium] Explain the copy-on-write approach.
- [Medium] What is a Lock? How is it different from synchronized?
- [Medium] What is the difference between fail-fast and fail-safe iterators?
- [Medium] What are atomic operations and atomic classes in Java?
- [Medium] Comparable vs Comparator: how do you sort by multiple fields?
- [Hard] How does ConcurrentHashMap work in Java 8+?
- [Hard] What is the compare-and-swap (CAS) approach?

</details>


### Multithreading and Concurrency

<details><summary><b><a href="05-multithreading/concurrency-advanced.md">Advanced concurrency</a></b> (14: 2 Easy · 9 Medium · 3 Hard)</summary>

- [Easy] Describe a few other important methods in threads.
- [Easy] What is the difference between wait() and sleep()?
- [Medium] What are the important methods for inter-thread communication?
- [Medium] Can you write a producer-consumer program with wait and notify?
- [Medium] Write a program where two threads print odd and even numbers alternately.
- [Medium] What does volatile guarantee, and what doesn't it?
- [Medium] How do you prevent deadlocks?
- [Medium] What is CompletableFuture? Give an example.
- [Medium] What are CountDownLatch, CyclicBarrier and Semaphore?
- [Medium] What is ReadWriteLock?
- [Medium] What are virtual threads (Java 21)?
- [Hard] What is the Java Memory Model's happens-before relationship?
- [Hard] What is a ThreadPoolExecutor and how do you size it?
- [Hard] What is ThreadLocal and when can it cause a memory leak?

</details>

<details><summary><b><a href="05-multithreading/multithreading-basics.md">Multithreading basics</a></b> (14: 11 Easy · 3 Medium)</summary>

- [Easy] What is the need for Threads in Java?
- [Easy] How do you create a thread?
- [Easy] What are the different states of a Thread?
- [Easy] What is priority of a thread? How do you change the priority of a thread?
- [Easy] What is ExecutorService?
- [Easy] What is Callable? How do you execute a Callable from ExecutionService?
- [Easy] What is Synchronization of threads ?
- [Easy] Can you give an example of a Synchronization block ?
- [Easy] What is the use of join methods in threads ?
- [Easy] What is the use of yield method?
- [Easy] What is Deadlock ?
- [Medium] Explain different ways of creating Executor Services?
- [Medium] How do you check whether an ExecutionService task executed successfully?
- [Medium] Can a static method be synchronized ?

</details>

<details><summary><b><a href="05-multithreading/threading-pitfalls-and-executors.md">Threading pitfalls and executors</a></b> (8: 2 Easy · 5 Medium · 1 Hard)</summary>

- [Easy] What is a daemon thread?
- [Easy] What is the difference between Runnable and Callable?
- [Medium] What is a race condition? How do you fix it?
- [Medium] What makes a class thread-safe?
- [Medium] What are deadlock, livelock and starvation?
- [Medium] What is the difference between shutdown() and shutdownNow()?
- [Medium] What do invokeAll() and invokeAny() do?
- [Hard] What is the Fork/Join framework and work stealing?

</details>


### JVM, Memory and GC

<details><summary><b><a href="06-jvm-memory-gc/gc-and-serialization.md">GC and serialization</a></b> (12: 6 Easy · 5 Medium · 1 Hard)</summary>

- [Easy] What is a Garbage Collection?
- [Easy] Can you explain the Garbage Collection with an example?
- [Easy] What is Serialization?
- [Easy] How do you serialize an object using Serializable interface?
- [Easy] How do you de-serialize in Java?
- [Easy] What do you do if only parts of the object have to be serialized?
- [Medium] When is the Garbage Collection run?
- [Medium] What are the best practices for Garbage Collection?
- [Medium] What are Initialization Blocks?
- [Medium] How do you serialize a hierarchy of objects?
- [Medium] Are the values of static variables stored when an object is serialized?
- [Hard] Are the constructors in an object invoked when it is de-serialized?

</details>

<details><summary><b><a href="06-jvm-memory-gc/jvm-memory-and-performance.md">JVM memory and performance</a></b> (9: 5 Medium · 4 Hard)</summary>

- [Medium] What are the memory areas of the JVM?
- [Medium] How does generational garbage collection work?
- [Medium] Can a Java application have a memory leak? Give examples.
- [Medium] Explain class loading and the delegation model.
- [Medium] What is JIT compilation?
- [Hard] Which garbage collectors are available, and which would you choose?
- [Hard] How do you troubleshoot an OutOfMemoryError or high memory in production?
- [Hard] How do you diagnose high CPU or a hung Java service?
- [Hard] What is the difference between strong, soft, weak and phantom references?

</details>


### Java 8, Streams and Functional Programming

<details><summary><b><a href="07-java8-functional/functional-programming.md">Functional programming</a></b> (16: 14 Easy · 2 Medium)</summary>

- [Easy] What is functional programming?
- [Easy] Can you give an example of functional programming?
- [Easy] What is a Functional Interface?
- [Easy] What is a stream?
- [Easy] Explain about streams with an example?
- [Easy] What are intermediate operations in streams?
- [Easy] What are terminal operations in streams?
- [Easy] What are lambda expressions?
- [Easy] Can you give an example of lambda expression?
- [Easy] Can you explain the relationship between lambda expression and functional interfaces?
- [Easy] What is a Function Functional Interface?
- [Easy] What is a Predicate Functional Interface?
- [Easy] What is a Consumer Functional Interface?
- [Easy] What is a Supplier Functional Interface?
- [Medium] What are method references?
- [Medium] Can you give examples of functional interfaces with multiple arguments?

</details>

<details><summary><b><a href="07-java8-functional/java8-advanced.md">Java 8 (advanced)</a></b> (8: 3 Easy · 5 Medium)</summary>

- [Easy] Explain the Java 8 Date and Time API.
- [Easy] What is the difference between a Collection and a Stream?
- [Easy] What are the main functional interfaces in java.util.function?
- [Medium] What are default methods, and how is the diamond problem resolved?
- [Medium] Why must variables used in a lambda be effectively final?
- [Medium] What happens with Collectors.toMap() when there are duplicate keys?
- [Medium] What is the difference between map(), flatMap() and peek() in streams?
- [Medium] What are the different forms of reduce()?

</details>

<details><summary><b><a href="07-java8-functional/streams-coding-questions.md">Streams coding questions</a></b> (16: 8 Easy · 7 Medium · 1 Hard)</summary>

- [Easy] Find the second highest salary.
- [Easy] Partition numbers into even and odd.
- [Easy] Flatten a list of lists and sort unique words.
- [Easy] Join names of employees older than 30, comma-separated.
- [Easy] Sum, max and statistics in one pass.
- [Easy] Reverse each word of a sentence.
- [Easy] Check whether two strings are anagrams using streams.
- [Easy] What is the difference between map and flatMap?
- [Medium] Group employees by department and count / average salary.
- [Medium] Find the highest-paid employee in each department.
- [Medium] Count the frequency of each character in a string.
- [Medium] Find the first non-repeating character in a string.
- [Medium] Find duplicate elements in a list.
- [Medium] Are streams lazy? What happens without a terminal operation?
- [Medium] What is Optional and how should you use it?
- [Hard] When should you avoid parallel streams?

</details>


### Generics

<details><summary><b><a href="08-generics/generics.md">Generics</a></b> (10: 4 Easy · 3 Medium · 3 Hard)</summary>

- [Easy] What are Generics?
- [Easy] Why do we need Generics? Can you give an example of how Generics make a program more flexible?
- [Easy] How do you declare a generic class?
- [Easy] Can you give an example of a generic method?
- [Medium] What are the restrictions in using a generic type that is declared in a class declaration?
- [Medium] How can we restrict Generics to a subclass of a particular class?
- [Medium] How can we restrict Generics to a superclass of a particular class?
- [Hard] What is type erasure?
- [Hard] What is the difference between List<?>, List<Object> and List<? extends Number>?
- [Hard] What is a bounded type parameter with multiple bounds?

</details>


### Miscellaneous and Java Versions

<details><summary><b><a href="09-misc/arrays-enums-misc.md">Arrays, enums and misc</a></b> (9: 7 Easy · 2 Medium)</summary>

- [Easy] What are the default values in an array?
- [Easy] How do you print the content of an array?
- [Easy] How do you compare two arrays?
- [Easy] What is an enum?
- [Easy] Can you use a switch statement around an enum?
- [Easy] What is tokenizing?
- [Easy] Can you give an example of tokenizing?
- [Medium] What are asserts used for?
- [Medium] When should asserts be used?

</details>

<details><summary><b><a href="09-misc/extra-knowledge.md">Extra knowledge (web, DB, OS)</a></b> (26: 14 Easy · 11 Medium · 1 Hard)</summary>

- [Easy] Difference between API and REST API?
- [Easy] What is domain vs. endpoint in API?
- [Easy] Difference between Http and Https?
- [Easy] What is the difference between authentication and authorization in api?
- [Easy] Difference between Abstract class vs. interface?
- [Easy] Difference between heap and stack memory?
- [Easy] What is JSON? How is it utilized?
- [Easy] What is the usage of the PATH variable in an operating system? How is it utilized, when would you like to update it?
- [Easy] What is the difference between a database view and a table in a database?
- [Easy] What all commands in Unix are you aware of? Please explain their usage.
- [Easy] What is shell scripting? What purpose is it used for?
- [Easy] Explain how you can read fields sent in a request from the browser using a servlet.
- [Easy] Difference between hashmap and hashtable?
- [Easy] What is constructor chaining?
- [Medium] What is reflection API in Java?
- [Medium] Where is the Java Reflection API used in the Spring Framework?
- [Medium] What is the stored procedure in JDBC?
- [Medium] What is a connection pool? How is it used to improve performance in database applications?
- [Medium] What is the difference between a ClassCastException and a ClassNotFoundException in Java?
- [Medium] What configurations do you need to make in web.xml to deploy a servlet in a web application?
- [Medium] Explain how the session is utilized for security implementation. Please explain who creates the session and how is session information exchanged between the browser and server.
- [Medium] What is meant by an entity-relationship (E-R) model? Explain the terms Entity, Entity Type, and Entity Set in a DBMS.
- [Medium] What is a database trigger? How is it used to enforce business rules?
- [Medium] How does your computer know what path to take to reach the external server
- [Medium] What objects are implicitly available in JSP? Explain their usage
- [Hard] Handling and fixing 'Out of Memory' exceptions?

</details>

<details><summary><b><a href="09-misc/java-version-features.md">Java version features (5 → 21)</a></b> (7: 4 Easy · 3 Medium)</summary>

- [Easy] What are the new features in Java 5?
- [Easy] What are the new features in Java 6 and 7?
- [Easy] What are the new features in Java 8?
- [Easy] What is a record and when would you use it?
- [Medium] What changed in Java 9, 10 and 11?
- [Medium] What are the key features from Java 12 to 17?
- [Medium] What are the key features of Java 21?

</details>


### DSA, Coding Programs and LLD

<details><summary><b><a href="10-dsa-coding/01-strings.md">Strings</a></b> (6: 2 Easy · 4 Medium)</summary>

- [Medium] 1. Check whether a pattern exists in a text (substring search)
- [Easy] 2. Valid palindrome (ignore case and non-alphanumerics)
- [Medium] 3. Longest palindromic substring
- [Medium] 4. Longest substring without repeating characters
- [Medium] 5. Group anagrams
- [Easy] 6. String compression

</details>

<details><summary><b><a href="10-dsa-coding/02-arrays-and-hashing.md">Arrays and hashing</a></b> (6: 2 Easy · 4 Medium)</summary>

- [Easy] 7. Two sum
- [Easy] 8. Best time to buy and sell stock (I and II)
- [Medium] 9. Maximum subarray sum (Kadane's algorithm)
- [Medium] 10. Merge overlapping intervals
- [Medium] 11. Product of array except self (no division)
- [Medium] 12. Subarray sum equals K

</details>

<details><summary><b><a href="10-dsa-coding/03-linked-list-matrix-stack.md">Linked list, matrix, stack</a></b> (5: 3 Easy · 2 Medium)</summary>

- [Easy] 13. Reverse a linked list
- [Medium] 14. Detect a cycle and return where it starts
- [Easy] 15. Merge two sorted lists
- [Medium] 16. Word search in a matrix
- [Easy] 17. Valid parentheses

</details>

<details><summary><b><a href="10-dsa-coding/04-trees-and-binary-search.md">Trees and binary search</a></b> (4: 1 Easy · 3 Medium)</summary>

- [Medium] 18. Level order traversal (BFS)
- [Medium] 19. Lowest common ancestor of a binary tree
- [Medium] 20. Search in a rotated sorted array
- [Easy] Before you say "done" in an interview

</details>

<details><summary><b><a href="10-dsa-coding/05-lld-problems.md">Low-level design (LLD)</a></b> (3: 2 Medium · 1 Hard)</summary>

- [Medium] Design an LRU cache with O(1) get and put
- [Medium] Design a parking lot
- [Hard] Design a rate limiter (token bucket)

</details>

<details><summary><b><a href="10-dsa-coding/06-classic-java-programs.md">Classic Java programs</a></b> (9: 9 Easy)</summary>

- [Easy] Reverse a string without using reverse()
- [Easy] Check whether a number is prime
- [Easy] Fibonacci series (iterative and memoised)
- [Easy] Check whether two strings are anagrams
- [Easy] Find the missing number in 1..n
- [Easy] Move all zeros to the end, keeping order
- [Easy] Remove duplicates from a sorted array in place
- [Easy] Print a pattern (Floyd's triangle)
- [Easy] FizzBuzz

</details>

<details><summary><b><a href="10-dsa-coding/07-medium-hard-problems.md">Medium and hard problems</a></b> (13: 9 Medium · 4 Hard)</summary>

- [Medium] 21. Top K frequent elements
- [Medium] 22. Kth largest element in an array
- [Medium] 23. Longest consecutive sequence
- [Medium] 24. Three sum
- [Medium] 25. Container with most water
- [Medium] 26. Number of islands
- [Medium] 27. Course schedule (cycle detection / topological sort)
- [Medium] 28. Coin change (dynamic programming)
- [Medium] 29. Validate a binary search tree
- [Hard] 30. Trapping rain water
- [Hard] 31. Merge k sorted lists
- [Hard] 32. Sliding window maximum
- [Hard] 33. Minimum window substring

</details>

## Contributing

Found a mistake or want to add a question? Open an issue or a pull request. Keep the existing format:

~~~html
<details><summary>

## [Medium] Your question?
</summary>

Short answer in your own words.

**Example:**

```java
// minimal code that compiles
```
</details>
~~~

⭐ Star the repo if it helped you prepare.
