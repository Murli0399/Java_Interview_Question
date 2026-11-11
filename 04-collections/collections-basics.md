<details><summary>
	
## [Easy] Why do we need Collections in Java?
</summary>

Before JDK 1.2, Java had only arrays, `Vector`, `Hashtable` and `Stack`, each with its own unrelated API. The **Collections Framework** gives a common set of interfaces (`List`, `Set`, `Queue`, `Map`), ready-made implementations, and algorithms (`sort`, `binarySearch`, `shuffle`) that work the same way across all collections.

| | Array | Collection |
|---|---|---|
| Size | Fixed at creation | Grows and shrinks dynamically |
| Element types | Primitives and objects | Objects only (primitives are autoboxed) |
| Type safety | Checked at runtime (`ArrayStoreException`) | Checked at compile time with generics |
| Built-in operations | Few (`length`, `Arrays` helpers) | Rich API: add, remove, contains, iterate, sort, stream |
| Data structures | Just indexed storage | Lists, sets, queues, maps, trees, hash tables |
| Performance | Fastest for fixed-size primitive data | Small overhead, far more flexible |

Use arrays for fixed-size, performance-critical primitive data; use collections for almost everything else.

**Example:**

```java
int[] arr = new int[3];          // fixed size, no built-in search/sort helpers
List<Integer> list = new ArrayList<>();   // grows as needed
list.add(5); list.add(1); list.add(3);
Collections.sort(list);          // [1, 3, 5]
System.out.println(list.contains(3)); // true
```

</details>

<details><summary>
	
## [Easy] What are the important interfaces in the Collection Hierarchy?
</summary>

The Java Collections Framework provides several important interfaces in its collection hierarchy. These interfaces define common behaviors and operations that are shared among different types of collections. Here are some of the important interfaces in the Collection Hierarchy:

- **Collection** This is the root interface in the collection hierarchy. It defines the basic operations that are common to all collections, such as adding, removing, and querying elements. The Collection interface extends the Iterable interface, which enables iteration over the elements in the collection.

- **List** The List interface represents an ordered collection of elements where duplicate elements are allowed. It provides additional operations for element insertion, removal, and retrieval at specific positions. Implementations of List include ArrayList, LinkedList, and Vector.

- **Set** The Set interface represents a collection that does not allow duplicate elements. It defines methods for adding and removing elements, as well as checking for the presence of specific elements. Common implementations of Set are HashSet, TreeSet, and LinkedHashSet.

- **Queue** The Queue interface models a collection that follows the FIFO (First-In-First-Out) principle. It provides methods for adding elements at the end and removing elements from the beginning of the queue. The Queue interface extends the Collection interface and includes additional methods for queue-specific operations. Implementations of Queue include LinkedList, PriorityQueue, and ArrayDeque.

- **Map** The Map interface represents a mapping between keys and values, where each key is unique. It allows you to store and retrieve values based on their associated keys. The Map interface provides methods for adding, removing, and accessing key-value pairs. Common implementations of Map are HashMap, TreeMap, and LinkedHashMap.

- **Iterator** The Iterator interface provides a way to iterate over the elements in a collection. It defines methods for checking if there are more elements, retrieving the next element, and removing elements during iteration.

These interfaces, along with their respective implementations, form the foundation of the Java Collections Framework. They provide a wide range of functionality for working with collections and enable you to choose the most appropriate collection type based on your specific requirements.

**Example:**

```text
Iterable
└── Collection
    ├── List   -> ArrayList, LinkedList, Vector
    ├── Set    -> HashSet, LinkedHashSet
    │   └── SortedSet -> NavigableSet -> TreeSet
    └── Queue  -> PriorityQueue
        └── Deque -> ArrayDeque, LinkedList

Map (separate hierarchy) -> HashMap, LinkedHashMap, Hashtable
└── SortedMap -> NavigableMap -> TreeMap
```

</details>

<details><summary>
	
## [Easy] What are the important methods that are declared in the Collection Interface?
</summary>

The Collection interface in the Java Collections Framework defines a set of common methods that are shared by all collection types. Here are some of the important methods declared in the Collection interface:

- **int size()** Returns the number of elements in the collection.

- **boolean isEmpty()** Checks if the collection is empty (contains no elements).

- **boolean contains(Object obj)** Checks if the collection contains the specified object.

- **boolean add(E obj)** Adds the specified element to the collection.

- **boolean remove(Object obj)** Removes a single instance of the specified object from the collection.

- **boolean containsAll(Collection<?> c)** Checks if the collection contains all the elements in the specified collection.

- **boolean addAll(Collection<? extends E> c)** Adds all the elements from the specified collection to the collection.

- **boolean removeAll(Collection<?> c)** Removes all the elements in the specified collection from the collection.

- **boolean retainAll(Collection<?> c)** Removes all elements from the collection except those that are present in the specified collection.

- **void clear()** Removes all elements from the collection.

- **Object[] toArray()** Returns an array containing all the elements in the collection.

- **<T> T[] toArray(T[] a)** Returns an array containing all the elements in the collection, using the provided array if it is large enough. The runtime type of the returned array is the same as the specified array.

- **Iterator<E> iterator()** Returns an iterator over the elements in the collection, allowing sequential access to the elements.

These methods provide the basic operations for adding, removing, querying, and manipulating elements in a collection. Implementations of the Collection interface, such as ArrayList, HashSet, and LinkedList, provide their own specific implementations of these methods to suit their respective collection types.

It's important to note that the Collection interface does not specify methods for indexed access or positional operations. For those functionalities, you would typically use the List interface, which extends Collection and provides additional methods for working with ordered collections.

**Example:**

```java
Collection<String> c = new ArrayList<>(List.of("a", "b"));
c.add("c");
c.addAll(List.of("d", "e"));
c.remove("a");
c.removeIf(s -> s.equals("e"));
System.out.println(c.size() + " " + c.contains("b") + " " + c.isEmpty()); // 3 true false
c.retainAll(List.of("b", "c"));      // keep only these
Object[] arr = c.toArray();
c.stream().forEach(System.out::println);
c.clear();
```

</details>

<details><summary>
	
## [Easy] Can you explain briefly about the List Interface?
</summary>

The List interface is a fundamental part of the Java Collections Framework. It represents an ordered collection of elements, allowing duplicate values and maintaining the insertion order. In other words, a List is an ordered sequence of elements that can be accessed by their index.

Here are some key characteristics of the List interface:

- **Ordered** Elements in a List are arranged in a specific order. The order of elements is typically determined by the order of their insertion into the List.

- **Indexed Access** Each element in a List has an associated index value starting from 0. This allows for efficient random access to elements by their index. You can retrieve, update, or remove elements using their index.

- **Duplicates** Unlike some other collection types, Lists allow duplicate elements. It means you can have multiple occurrences of the same value within a List.

The List interface defines several methods to work with lists, including:

- **Adding and removing elements** You can add elements to the List using methods like add() and addAll(), and remove elements using remove() or removeAll(). The List interface also provides methods for removing elements at specific indices.

- **Accessing elements** You can access elements by their index using get(). The size of the List can be obtained using size().

- **Searching and sorting** The List interface includes methods such as contains(), indexOf(), and lastIndexOf() to search for elements within the list. It also provides a sort() method to sort the elements of the List.

- **Iterating over elements** You can iterate over the elements of a List using traditional for loops, enhanced for loops, or the Iterator and ListIterator interfaces.

- **Modifying elements** The List interface provides methods to modify elements at specific indices using set(), which allows you to update an element at a given position.

Several classes in Java implement the List interface, such as ArrayList, LinkedList, and Vector. These classes provide different implementations with varying performance characteristics and usage scenarios.

By utilizing the List interface, you can easily work with ordered collections of elements, perform operations like insertion, deletion, retrieval, and modification efficiently.

**Example:**

```java
List<String> names = new ArrayList<>(List.of("Asha", "Ravi"));
names.add(1, "Kiran");              // insert at index -> [Asha, Kiran, Ravi]
names.add("Asha");                  // duplicates allowed
System.out.println(names.get(0));   // Asha (index-based access)
System.out.println(names.indexOf("Asha") + " " + names.lastIndexOf("Asha")); // 0 3
names.set(2, "Meena");
List<String> sub = names.subList(0, 2);
```

</details>

<details><summary>
	
## [Easy] Explain about ArrayList with an example?
</summary>

The ArrayList class in Java is an implementation of the List interface that uses a dynamically resizable array to store elements. It provides a flexible and efficient way to work with ordered collections of objects. Let's walk through an example to understand how ArrayList works:

```java
  import java.util.ArrayList;

  public class ArrayListExample {
      public static void main(String[] args) {
          // Create an ArrayList to store integers
          ArrayList<Integer> numbers = new ArrayList<>();

          // Add elements to the ArrayList
          numbers.add(10);
          numbers.add(20);
          numbers.add(30);
          numbers.add(40);

          // Access elements by index
          System.out.println("Element at index 2: " + numbers.get(2));  // Output: 30

          // Update an element at a specific index
          numbers.set(1, 25);
          System.out.println("Updated element at index 1: " + numbers.get(1));  // Output: 25

          // Remove an element by value
          numbers.remove(Integer.valueOf(30));

          // Remove an element by index
          numbers.remove(0);

          // Iterate over the elements using a for-each loop
          for (Integer number : numbers) {
              System.out.println(number);
          }
      }
  }
```

</details>

<details><summary>
	
## [Easy] Can an ArrayList have Duplicate elements?
</summary>

Yes, an ArrayList can have duplicate elements. The ArrayList class allows duplicate elements, meaning you can add multiple occurrences of the same value to the list.

Here's an example to demonstrate adding duplicate elements to an ArrayList:
      
```java
  import java.util.ArrayList;

  public class ArrayListExample {
      public static void main(String[] args) {
          ArrayList<String> fruits = new ArrayList<>();

          // Adding duplicate elements
          fruits.add("apple");
          fruits.add("banana");
          fruits.add("apple");
          fruits.add("orange");
          fruits.add("banana");

          System.out.println(fruits);
      }
  }
```

In this example, we create an ArrayList named fruits to store strings. We add multiple elements to the list, including duplicates such as "apple" and "banana". When we print the ArrayList, it will display all the elements, including the duplicate ones:

</details>

<details><summary>
	
## [Easy] How do you iterate around an ArrayList using Iterator?
</summary>

To iterate over an ArrayList using an Iterator, you can follow these steps:

1. Create an instance of the ArrayList and add elements to it.
2. Obtain an Iterator object by calling the iterator() method on the ArrayList.
3. Use the hasNext() method of the Iterator to check if there are more elements in the ArrayList.
4. Inside a loop, use the next() method of the Iterator to retrieve the next element.
5. Perform the desired operations with each element within the loop.
Here's an example that demonstrates iterating over an ArrayList using an Iterator:

```java
      import java.util.ArrayList;
      import java.util.Iterator;
      public class ArrayListIteratorExample {
        public static void main(String[] args) {
          ArrayList<String> fruits = new ArrayList<>();
          // Add elements to the ArrayList
          fruits.add("apple");
          fruits.add("banana");
          fruits.add("orange");

          // Obtain an Iterator object
          Iterator<String> iterator = fruits.iterator();

          // Iterate over the ArrayList using the Iterator
          while (iterator.hasNext()) {
              String fruit = iterator.next();
              System.out.println(fruit);
          }
        }
      }
```

</details>

<details><summary>
	
## [Easy] How do you sort an ArrayList?
</summary>

To sort an ArrayList in Java, you can use the Collections.sort() method. The Collections class provides a static sort() method that allows you to sort a List in ascending order based on the natural ordering of its elements or a specified comparator.

Here's an example that demonstrates sorting an ArrayList of integers:

```java
    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.Comparator;

    public class ArrayListSortExample {
        public static void main(String[] args) {
            ArrayList<String> fruits = new ArrayList<>();

            // Add elements to the ArrayList
            fruits.add("apple");
            fruits.add("banana");
            fruits.add("orange");
            fruits.add("pear");

            // Sort the ArrayList in acending order
            Collections.sort(fruits);

            // Print the sorted ArrayList
            System.out.println(fruits);

            // Sort the ArrayList in descending order
            Collections.sort(fruits, Comparator.reverseOrder());

            // Print the sorted ArrayList
            System.out.println(fruits);
        }
    }
```

</details>

<details><summary>
	
## [Easy] How do you sort elements in an ArrayList using Comparable interface?
</summary>

To sort elements in an ArrayList using the Comparable interface, you need to implement the Comparable interface in the class of the elements you want to sort. The Comparable interface provides a method called compareTo() that defines the natural ordering of objects.

Here's an example that demonstrates sorting an ArrayList of custom objects using the Comparable interface:

```java
    import java.util.ArrayList;
    import java.util.Collections;

    public class Student implements Comparable<Student> {
        private int id;
        private String name;

        public Student(int id, String name) {
            this.id = id;
            this.name = name;
        }

        public int getId() {
            return id;
        }

        public String getName() {
            return name;
        }

        @Override
        public int compareTo(Student other) {
            // Compare students based on their IDs
            return Integer.compare(this.id, other.id);
        }

        @Override
        public String toString() {
            return "Student{" +
                    "id=" + id +
                    ", name='" + name + '\'' +
                    '}';
        }

        public static void main(String[] args) {
            ArrayList<Student> students = new ArrayList<>();
            students.add(new Student(2, "Alice"));
            students.add(new Student(1, "Bob"));
            students.add(new Student(3, "Charlie"));

            // Sort the ArrayList
            Collections.sort(students);

            // Print the sorted ArrayList
            System.out.println(students);
        }
    }
```

</details>

<details><summary>
	
## [Easy] How do you sort elements in an ArrayList using Comparator interface?
</summary>

To sort elements in an ArrayList using the Comparator interface, you need to create a separate class that implements the Comparator interface or use an anonymous class or lambda expression. The Comparator interface allows you to define custom comparison logic for sorting objects.

Here's an example that demonstrates sorting an ArrayList of custom objects using the Comparator interface:

```java
    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.Comparator;

    public class Student {
        private int id;
        private String name;

        public Student(int id, String name) {
            this.id = id;
            this.name = name;
        }

        public int getId() {
            return id;
        }

        public String getName() {
            return name;
        }

        @Override
        public String toString() {
            return "Student{" +
                    "id=" + id +
                    ", name='" + name + '\'' +
                    '}';
        }

        public static void main(String[] args) {
            ArrayList<Student> students = new ArrayList<>();
            students.add(new Student(2, "Alice"));
            students.add(new Student(1, "Bob"));
            students.add(new Student(3, "Charlie"));

            // Create a Comparator to sort students based on their IDs
            Comparator<Student> idComparator = new Comparator<Student>() {
                @Override
                public int compare(Student s1, Student s2) {
                    return Integer.compare(s1.getId(), s2.getId());
                }
            };

            // Sort the ArrayList using the Comparator
            Collections.sort(students, idComparator);

            // Print the sorted ArrayList
            System.out.println(students);
        }
    }
```

</details>

<details><summary>
	
## [Easy] What is Vector class? How is it different from an ArrayList?
</summary>

`Vector` is a legacy (Java 1.0) resizable array, later retrofitted to implement `List`.

| | `Vector` | `ArrayList` |
|---|---|---|
| Synchronized | Yes, every method | No |
| Speed (single thread) | Slower (lock on every call) | Faster |
| Growth when full | **Doubles** capacity by default (or grows by `capacityIncrement` if set) | Grows by **50%** |
| Iteration | `Iterator` and legacy `Enumeration` | `Iterator`/`ListIterator` |
| Since | Java 1.0 (legacy) | Java 1.2 |

Even with synchronized methods, compound actions on a `Vector` (check-then-add, iterate-and-modify) still need external locking. For thread safety today, use `Collections.synchronizedList(new ArrayList<>())` or `CopyOnWriteArrayList` (read-heavy), or avoid sharing.

**Example:**

```java
List<Integer> vector = new Vector<>();      // every method synchronized (slow, legacy)
List<Integer> arrayList = new ArrayList<>(); // not synchronized (fast)

// Need thread safety today? Prefer these over Vector:
List<Integer> sync = Collections.synchronizedList(new ArrayList<>());
List<Integer> cow = new CopyOnWriteArrayList<>();   // read-heavy lists
```

</details>

<details><summary>
	
## [Easy] Can you briefly explain about the Set Interface?
</summary>

In Java, the Set interface is part of the Java Collections Framework and represents a collection of unique elements. It is an interface that extends the Collection interface and defines the behavior of a set, which is a mathematical concept where each element occurs only once.

**Example:**

```java
Set<String> emails = new HashSet<>();
System.out.println(emails.add("a@x.com"));  // true
System.out.println(emails.add("a@x.com"));  // false - duplicates ignored
System.out.println(emails.size());          // 1

// Common use: remove duplicates from a list
List<Integer> unique = new ArrayList<>(new LinkedHashSet<>(List.of(3, 1, 3, 2))); // [3, 1, 2]
```

</details>

<details><summary>
	
## [Easy] What are the important interfaces related to the Set Interface?
</summary>

The Set interface in Java provides a collection of unique elements with no defined order. It is part of the Java Collections Framework and is implemented by classes such as HashSet, TreeSet, and LinkedHashSet. The Set interface itself doesn't declare any new methods but inherits methods from the Collection interface.

Here are some important interfaces related to the Set interface:

- **Set** The Set interface itself is an important interface related to the Set interface. It defines the basic behavior and operations for a collection that stores unique elements. It extends the Collection interface and doesn't introduce any additional methods.

- **SortedSet** The SortedSet interface extends the Set interface and adds sorting functionality to the Set. It maintains the elements in ascending order or according to a specified Comparator. This interface introduces methods for retrieving elements based on their position in the sorted set, such as first(), last(), headSet(), tailSet(), and subSet().

- **NavigableSet** The NavigableSet interface extends the SortedSet interface and provides additional navigation methods for retrieving elements based on their relationship to other elements in the set. It introduces methods like lower(), floor(), ceiling(), higher(), pollFirst(), and pollLast().

- **HashSet** HashSet is a class that implements the Set interface and stores elements using a hash table data structure. It provides constant-time performance for basic operations like adding, removing, and searching for elements. However, it doesn't guarantee any specific order for the elements.

- **TreeSet** TreeSet is a class that implements both the SortedSet and NavigableSet interfaces. It stores elements in a sorted order defined by either their natural order or a custom Comparator. It provides efficient performance for accessing elements in sorted order but may have slightly slower performance for basic operations compared to HashSet.

- **LinkedHashSet** LinkedHashSet is a class that implements the Set interface and maintains the insertion order of elements, in addition to ensuring uniqueness. It uses a hash table with a linked list running through it to maintain the order of insertion. It provides predictable iteration order, which is the order in which elements were added.

These interfaces and classes provide various functionalities and implementations for working with sets in Java, allowing you to choose the one that best suits your requirements.
</details>

<details><summary>
	
## [Easy] What is the difference between Set and SortedSet interfaces?
</summary>

The main difference between the Set and SortedSet interfaces in Java is as follows:

### Set Interface:

- Represents an unordered collection of unique elements.
- Does not allow duplicate elements.
- No specific order is guaranteed.
- Examples: HashSet, LinkedHashSet.
### SortedSet Interface:

- Extends the Set interface.
- Represents a sorted collection of unique elements.
- Maintains elements in ascending order (natural order) or as per a specified Comparator.
- Does not allow duplicate elements.
- Provides additional methods for accessing elements based on their position in the sorted set.
- Examples: TreeSet.
In summary, while the Set interface does not impose any specific order on its elements, the SortedSet interface ensures that the elements are stored in a sorted order. The choice between these interfaces depends on whether you need a sorted collection and if maintaining a specific order is important for your use case.

**Example:**

```java
Set<Integer> set = new HashSet<>(List.of(5, 1, 3));        // no order guarantee
SortedSet<Integer> sorted = new TreeSet<>(List.of(5, 1, 3)); // [1, 3, 5]
System.out.println(sorted.first() + " " + sorted.last());   // 1 5
System.out.println(sorted.headSet(3));                      // [1]
System.out.println(sorted.tailSet(3));                      // [3, 5]
```

</details>

<details><summary>
	
## [Easy] Can you give examples of classes that implement the Set Interface?
</summary>

The main classes that implement the Set interface:

- **HashSet** HashSet is one of the most commonly used implementations of the Set interface. It stores elements in a hash table, providing constant-time performance for basic operations such as adding, removing, and searching elements. However, it does not guarantee any specific order for the elements.

- **LinkedHashSet** LinkedHashSet is another implementation of the Set interface that maintains the insertion order of elements. It uses a combination of a hash table and a linked list, providing predictable iteration order based on the order in which elements were added.

- **TreeSet** TreeSet is an implementation of the SortedSet interface, which extends the Set interface. It stores elements in a sorted order defined by either their natural order or a custom Comparator. TreeSet uses a balanced binary tree (specifically, a red-black tree) internally, which allows for efficient access and retrieval of elements in sorted order.

These are just a few examples of classes that implement the Set interface in Java. Depending on your specific requirements, you can choose the appropriate implementation based on factors such as ordering, performance, and element uniqueness.
</details>

<details><summary>
	
## [Easy] What is a HashSet?
</summary>

HashSet is a class in Java that implements the Set interface. It provides a collection of unique elements with no defined order. Some important characteristics of HashSet include:

- **Uniqueness** HashSet does not allow duplicate elements. If you attempt to add an element that already exists in the set, it won't be added again.

- **Hash Table Implementation** HashSet uses a hash table data structure to store and retrieve elements efficiently. It internally employs hashing techniques to compute the hash code of elements, distributing them across buckets within the hash table.

- **Performance** HashSet offers constant-time performance (O(1)) for basic operations like adding, removing, and searching for elements. The performance remains consistent regardless of the size of the HashSet.

- **No Order** The elements in a HashSet are not stored in any particular order. When iterating over a HashSet, the order of element retrieval may vary between iterations or when elements are added or removed.

- **Null Values** HashSet allows storing a single null value. If you attempt to add multiple null values, only one null value will be stored.

HashSet provides an efficient way to store and work with a collection of unique elements, without any specific ordering requirements. It is commonly used when you need to check for element existence or eliminate duplicates from a collection.

**Example:**

```java
Set<String> tags = new HashSet<>();
tags.add("java"); tags.add("kafka"); tags.add("java");
System.out.println(tags.size());            // 2
System.out.println(tags.contains("kafka")); // true, O(1) average
// Internally a HashSet is a HashMap whose keys are the elements and values a dummy object.
```

</details>

<details><summary>
	
## [Easy] What is a LinkedHashSet? How is different from a HashSet?
</summary>

`LinkedHashSet` extends `HashSet` and keeps a **doubly linked list across its entries**, so it combines HashSet's fast O(1) lookups with **predictable insertion-order iteration** (like a LinkedList).

| | `HashSet` | `LinkedHashSet` |
|---|---|---|
| Iteration order | Undefined | Insertion order |
| Structure | Hash table (backed by `HashMap`) | Hash table + linked list (backed by `LinkedHashMap`) |
| add/remove/contains | O(1) average | O(1) average, slightly slower and more memory |
| Null | One null allowed | One null allowed |

Use `LinkedHashSet` when you need uniqueness and a stable order, e.g. removing duplicates from a list while keeping the original order.

**Example:**

```java
Set<String> hash = new HashSet<>(List.of("banana", "apple", "cherry"));
Set<String> linked = new LinkedHashSet<>(List.of("banana", "apple", "cherry"));
System.out.println(hash);    // order not guaranteed
System.out.println(linked);  // [banana, apple, cherry] - insertion order kept
```

</details>

<details><summary>
	
## [Easy] Explain briefly about Queue Interface?
</summary>

The Queue interface in Java represents a collection that orders elements in a specific way to facilitate specific operations like insertion, deletion, and retrieval of elements. It follows the FIFO (First-In-First-Out) principle, where elements are processed in the same order they were added to the queue.

Here are some key features of the Queue interface:

- **Ordering** The Queue interface maintains the order of elements according to the FIFO principle. The element that has been in the queue for the longest time is the first one to be processed (removed) when elements are retrieved.

- **Operations** The Queue interface provides various methods to perform operations on the queue, such as adding elements to the end of the queue (enqueue/offer), removing elements from the front of the queue (dequeue/poll), accessing the element at the front of the queue (peek), and checking if the queue is empty.

- **Implementations** Java provides several implementations of the Queue interface, including LinkedList, ArrayDeque, and PriorityQueue. The choice of implementation depends on factors such as the specific requirements of your application, the expected size of the queue, and the desired performance characteristics.

- **Interface Hierarchy** The Queue interface extends the Collection interface and adds specific queue-related operations. It also extends the Iterable interface, which allows iterating over the elements of the queue using the foreach loop or an iterator.

Queues are commonly used in scenarios where elements need to be processed in the order they were added, such as handling tasks in a multi-threaded environment, implementing job scheduling systems, or modeling real-life scenarios like waiting lines or event handling. The Queue interface provides a standardized way to work with such collections and offers flexibility in choosing the appropriate implementation based on your specific needs.

**Example:**

```java
Queue<String> tasks = new LinkedList<>();
tasks.offer("t1"); tasks.offer("t2");
System.out.println(tasks.peek());  // t1 (does not remove)
System.out.println(tasks.poll());  // t1 (removes)
System.out.println(tasks.poll());  // t2
System.out.println(tasks.poll());  // null when empty (remove() would throw)
```

</details>

<details><summary>
	
## [Easy] Can you briefly explain about the Map Interface?
</summary>

A `Map<K, V>` stores **key-value pairs**, with unique keys. Putting a value for an existing key replaces the old value (`put` returns the previous one).

Important: **`Map` does not extend `Collection`**. It is a separate hierarchy, but it offers three collection *views*: `keySet()`, `values()` and `entrySet()`.

Main implementations:
| | Order | Nulls | Thread-safe | Complexity |
|---|---|---|---|---|
| `HashMap` | None | 1 null key, null values | No | O(1) average |
| `LinkedHashMap` | Insertion (or access) order | Same as HashMap | No | O(1) average |
| `TreeMap` | Sorted by key | No null key (natural order) | No | O(log n) |
| `ConcurrentHashMap` | None | No null keys or values | Yes | O(1) average |
| `EnumMap` | Enum declaration order | No null keys | No | Very fast (array) |

Useful Java 8 methods: `getOrDefault`, `putIfAbsent`, `computeIfAbsent`, `merge`, `forEach`, `replaceAll`.

**Example:**

```java
Map<String, Integer> wordCount = new HashMap<>();
for (String w : "to be or not to be".split(" ")) {
    wordCount.merge(w, 1, Integer::sum);
}
System.out.println(wordCount);                     // {not=1, be=2, or=1, to=2}
System.out.println(wordCount.getOrDefault("is", 0)); // 0
wordCount.putIfAbsent("is", 1);
for (Map.Entry<String, Integer> e : wordCount.entrySet()) {
    System.out.println(e.getKey() + " -> " + e.getValue());
}
```

</details>

<details><summary>
	
## [Easy] What is a HashMap?
</summary>

In Java, HashMap is a class that implements the Map interface and provides a collection of key-value pairs. It uses a hash table data structure to store and retrieve elements efficiently. HashMap allows null keys and null values, and it does not maintain any specific order of elements.

Here are the key characteristics of HashMap:

- **Key-Value Pairs** HashMap stores elements as key-value pairs. Each key in the map is unique, and it is associated with a specific value. This allows for efficient retrieval of values based on their corresponding keys.

- **Hash Table Implementation** HashMap internally uses a hash table to store and organize its elements. It uses a hash function to compute the hash code of keys, which determines the position of the key-value pair in the hash table. This provides fast access and retrieval of elements.

- **Performance** HashMap offers constant-time performance (O(1)) for basic operations like adding, removing, and retrieving elements. The performance remains consistent regardless of the size of the HashMap, as long as the hash function distributes the elements evenly across the hash table.

- **No Order** HashMap does not maintain any specific order of elements. When iterating over a HashMap, the order of element retrieval may vary between iterations or when elements are added or removed. If you need a specific order, you can use the LinkedHashMap class, which extends HashMap and maintains the insertion order of elements.

- **Null Keys and Values** HashMap allows storing a single null key and multiple null values. If you attempt to add multiple entries with the same key, the previous value associated with that key will be overwritten.

HashMap is commonly used in various applications for efficient key-value storage and retrieval. It provides a flexible and efficient way to map keys to values, allowing for fast access to elements based on their keys.

**Example:**

```java
Map<Long, String> users = new HashMap<>();
users.put(1L, "Asha");
users.put(2L, "Ravi");
users.put(null, "unknown");          // one null key allowed
System.out.println(users.get(2L));   // Ravi, O(1) average
users.computeIfAbsent(3L, id -> "User-" + id);
users.forEach((id, name) -> System.out.println(id + "=" + name));
// See collections-internals-and-concurrent.md for how buckets, hashing and resizing work.
```

</details>

<details><summary>
	
## [Easy] What are the different methods in a Hash Map?
</summary>

HashMap in Java provides various methods to manipulate and access its elements. Here are some important methods of the HashMap class:

- **put(key, value)** Inserts the specified key-value pair into the HashMap. If the key already exists, the value is replaced with the new value. Returns the previous value associated with the key, or null if the key is new.

- **get(key)** Returns the value associated with the specified key in the HashMap. If the key is not found, it returns null.

- **remove(key)** Removes the key-value pair associated with the specified key from the HashMap. Returns the value that was removed, or null if the key is not found.

- **containsKey(key)** Checks if the HashMap contains the specified key. Returns true if the key is found, false otherwise.

- **containsValue(value)** Checks if the HashMap contains the specified value. Returns true if the value is found, false otherwise.

- **size()** Returns the number of key-value pairs (entries) in the HashMap.

- **isEmpty()** Checks if the HashMap is empty. Returns true if it contains no entries, false otherwise.

- **keySet()** Returns a Set of all the keys in the HashMap.

- **values()** Returns a Collection of all the values in the HashMap.

- **entrySet()** Returns a Set of all the key-value pairs (entries) in the HashMap as Map.Entry objects.

- **clear()** Removes all the key-value pairs from the HashMap, making it empty.

These are some of the commonly used methods provided by the HashMap class. These methods allow you to add, retrieve, remove, and perform other operations on the key-value pairs stored in the HashMap.

**Example:**

```java
Map<String, Integer> m = new HashMap<>();
m.put("a", 1);
m.putIfAbsent("a", 5);                 // ignored, key exists
m.getOrDefault("z", 0);                // 0
m.containsKey("a"); m.containsValue(1);
m.merge("a", 10, Integer::sum);        // a=11
m.compute("a", (k, v) -> v == null ? 1 : v * 2);  // a=22
m.computeIfPresent("a", (k, v) -> v - 2);         // a=20
m.replace("a", 100);
m.remove("a");
m.keySet(); m.values(); m.entrySet();
```

</details>

<details><summary>
	
## [Easy] Difference between Comparable and Comparator
</summary>

| | `Comparable<T>` | `Comparator<T>` |
|---|---|---|
| Package | `java.lang` | `java.util` |
| Method | `int compareTo(T other)` | `int compare(T a, T b)` |
| Where | Implemented **inside** the class being sorted | Separate object (class, lambda, method reference) |
| How many orders | **One natural order** per class (can still compare several fields inside it) | **Any number** of orders, chosen at the call site |
| Modifies the class? | Yes | No – works for classes you can't change |
| Used by | `Collections.sort(list)`, `TreeSet`, `TreeMap` with no comparator | `list.sort(cmp)`, `Collections.sort(list, cmp)`, `new TreeSet<>(cmp)` |

```java
record Employee(String name, double salary) implements Comparable<Employee> {
	public int compareTo(Employee o) { return name.compareTo(o.name); }   // natural order: name
}

list.sort(Comparator.comparingDouble(Employee::salary).reversed()
                    .thenComparing(Employee::name));                   // custom order
```

Return negative / zero / positive; use `Integer.compare(a, b)` instead of `a - b`, which can overflow.

**Example:**

```java
class Product implements Comparable<Product> {
    String name; double price;
    Product(String n, double p) { name = n; price = p; }
    @Override public int compareTo(Product o) { return name.compareTo(o.name); } // natural order
    @Override public String toString() { return name + ":" + price; }
}

List<Product> list = new ArrayList<>(List.of(new Product("pen", 10), new Product("book", 250)));
Collections.sort(list);                                       // by name (Comparable)
list.sort(Comparator.comparingDouble(p -> p.price));          // by price (Comparator)
list.sort(Comparator.comparingDouble((Product p) -> p.price).reversed()); // price desc
```

</details>

<details><summary>
	
## [Medium] What is LinkedList? How is it different from an ArrayList?
</summary>

`LinkedList` is a **doubly linked list**: each node holds the element plus references to the previous and next nodes. It implements both `List` and `Deque`.

| Operation | `ArrayList` (resizable array) | `LinkedList` (doubly linked) |
|---|---|---|
| `get(i)` / `set(i)` | **O(1)** | O(n) – walks from the nearer end |
| `add` at end | Amortised O(1) | O(1) |
| `add`/`remove` at start | O(n) (shifts elements) | **O(1)** |
| `add`/`remove` in the middle | O(n) (shift) | O(n) to *find* the position, O(1) to relink; O(1) only via an existing `ListIterator` |
| Memory per element | Low (one array slot) | High (node object + two references) |
| CPU cache friendliness | Very good (contiguous) | Poor (nodes scattered) |

In practice `ArrayList` is faster for almost all workloads. Use `ArrayDeque` for queue/stack operations; `LinkedList` is rarely the best choice.

**Example:**

```java
List<Integer> array = new ArrayList<>();   // get(i) O(1); insert in middle O(n) (shifts elements)
LinkedList<Integer> linked = new LinkedList<>(); // get(i) O(n); add/remove at ends O(1)

linked.addFirst(1);
linked.addLast(2);
linked.removeFirst();

// In practice ArrayList (or ArrayDeque for queues) wins almost always due to CPU cache locality.
```

</details>

<details><summary>
	
## [Medium] What is a TreeSet? How is different from a HashSet?
</summary>

`TreeSet` is a `NavigableSet` backed by a **red-black tree** (a `TreeMap`). It keeps elements **sorted**, by natural order (`Comparable`) or by a `Comparator` you pass in.

| | `HashSet` | `TreeSet` |
|---|---|---|
| Order | None | Sorted |
| add/remove/contains | O(1) average | O(log n) |
| Duplicate check | `hashCode()` + `equals()` | `compareTo()`/`compare()` returning 0 |
| `null` | One null allowed | Not allowed with natural ordering (`NullPointerException`); possible only with a null-tolerant `Comparator` |
| Extra operations | – | `first`, `last`, `floor`, `ceiling`, `headSet`, `tailSet`, `subSet`, `descendingSet` |

Use `TreeSet` when you need sorted data or range queries; use `HashSet` when you only need fast membership checks.

**Example:**

```java
TreeSet<Integer> scores = new TreeSet<>(List.of(70, 95, 82));
System.out.println(scores);                 // [70, 82, 95] sorted, O(log n) operations
System.out.println(scores.ceiling(80));     // 82
TreeSet<String> byLength = new TreeSet<>(Comparator.comparing(String::length).thenComparing(s -> s));
// TreeSet uses compareTo/compare (not equals) to detect duplicates.
```

</details>

<details><summary>
	
## [Medium] Can you give examples of implementations of NavigableSet?
</summary>

`NavigableSet` (extends `SortedSet`) adds closest-match navigation: `lower`, `floor`, `ceiling`, `higher`, `pollFirst`, `pollLast`, `descendingSet`, and range views. It has two implementations in the JDK:

- **`TreeSet`** – red-black tree, not thread-safe, O(log n) operations.
- **`ConcurrentSkipListSet`** – skip list, **thread-safe** and lock-free, also O(log n); use it when several threads read and write a sorted set.

Both accept either natural ordering or a custom `Comparator` (e.g. `new TreeSet<>(Comparator.reverseOrder())`).

**Example:**

```java
NavigableSet<Integer> set = new TreeSet<>(List.of(10, 20, 30, 40));
System.out.println(set.lower(30));    // 20  (< 30)
System.out.println(set.floor(25));    // 20  (<= 25)
System.out.println(set.higher(30));   // 40  (> 30)
System.out.println(set.descendingSet()); // [40, 30, 20, 10]
System.out.println(set.pollFirst());  // 10 (removes it)
// Implementations: TreeSet, ConcurrentSkipListSet (thread-safe)
```

</details>

<details><summary>
	
## [Medium] What is difference between Map and SortedMap?
</summary>

- **`Map`** makes no ordering promise; iteration order depends on the implementation (`HashMap`: none, `LinkedHashMap`: insertion).
- **`SortedMap`** (extends `Map`) keeps keys **sorted** by natural order or a `Comparator`, and adds `firstKey()`, `lastKey()`, `headMap()`, `tailMap()`, `subMap()` and `comparator()`.
- **`NavigableMap`** (extends `SortedMap`) adds closest-match methods: `floorKey`, `ceilingEntry`, `higherKey`, `descendingMap`, `pollFirstEntry`.

Implementations: `TreeMap` (red-black tree, O(log n)) and `ConcurrentSkipListMap` (thread-safe).

Use a sorted map for ordered reports, range lookups ("all events between 10:00 and 11:00"), or slab-based pricing.

**Example:**

```java
Map<String, Integer> map = new HashMap<>(Map.of("b", 2, "a", 1, "c", 3));    // no order
SortedMap<String, Integer> sorted = new TreeMap<>(map);                      // {a=1, b=2, c=3}
System.out.println(sorted.firstKey() + " " + sorted.lastKey());             // a c
System.out.println(sorted.headMap("c"));                                    // {a=1, b=2}
```

</details>

<details><summary>
	
## [Medium] What is a TreeMap? How is different from a HashMap?
</summary>

In Java, TreeMap is a class that implements the SortedMap interface and provides a collection of key-value pairs. It uses a red-black tree data structure to store and retrieve elements efficiently. TreeMap maintains the elements in a sorted order based on the natural order of the keys or a specified Comparator.

Here are the key differences between TreeMap and HashMap:

- **Ordering** TreeMap maintains the keys in a sorted order, either according to their natural order or a specified Comparator. The elements are arranged based on the key values. On the other hand, HashMap does not maintain any specific order for its keys.

- **Data Structure** TreeMap uses a balanced binary search tree (specifically, a red-black tree) as its underlying data structure to store and organize elements. This data structure ensures that the keys are always sorted and allows for efficient searching, insertion, and deletion operations. HashMap, on the other hand, uses a hash table data structure.

- **Performance** TreeMap provides a logarithmic time complexity (O(log n)) for basic operations like adding, removing, and searching elements. The balanced binary search tree structure allows efficient access to elements in sorted order. In contrast, HashMap offers constant time complexity (O(1)) for these operations, but it does not provide any sorting guarantees.

- **Null Keys** TreeMap does not allow null keys because it relies on the natural order or the provided Comparator to determine the order of the keys. On the other hand, HashMap allows a single null key to be stored.

- **Use Case** TreeMap is particularly useful when you need the keys to be stored and accessed in a specific order or when you require operations like retrieving the first or last key, finding keys greater than or less than a given value, or obtaining a range of keys. HashMap, on the other hand, is suitable when you don't need any particular order or when you prioritize constant-time performance.

In summary, TreeMap maintains elements in a sorted order using a balanced binary search tree, providing efficient sorted operations. HashMap does not guarantee any specific order but offers constant-time performance for basic operations. The choice between TreeMap and HashMap depends on whether you require sorted order and additional sorted map operations or prefer constant-time performance and do not require any specific ordering.

**Example:**

```java
TreeMap<String, Integer> prices = new TreeMap<>();
prices.put("mango", 120); prices.put("apple", 80); prices.put("kiwi", 60);
System.out.println(prices);                      // {apple=80, kiwi=60, mango=120} sorted by key
System.out.println(prices.firstEntry());         // apple=80
System.out.println(prices.floorKey("lemon"));    // kiwi
// TreeMap: O(log n), sorted, no null key. HashMap: O(1) average, unordered, one null key.
```

</details>