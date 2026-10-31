<details><summary>

### What are Generics?
</summary>

Generics in Java are a way to create classes and methods that can work with different types of data. This is done by using a type parameter, which is a placeholder for a specific type. For example, the following generic method can work with any type of data:

```
public <T> void doSomething(T data) {
  // Do something with data
}
```

This method can be used like this:

```
doSomething(1); // Works with integers
doSomething("Hello"); // Works with strings
```

Generics can be used to make code more reusable and maintainable. They can also help to prevent errors, such as trying to use an invalid type of data in a method.

Here are some of the benefits of using generics in Java:
- Reusability:
Generic classes and methods can be reused with different types of data, which makes code more concise and maintainable.
- Type safety:
Generics help to prevent errors, such as trying to use an invalid type of data in a method.
- Performance:
Generics can improve performance by allowing the compiler to optimize code.

Generics are a powerful feature that can be used to make Java code more reusable, maintainable, and efficient.
</details>
<details><summary>

### Why do we need Generics? Can you give an example of how Generics make a program more flexible?
</summary>

**Example:**

```java
// Without generics: casts and runtime errors
List raw = new ArrayList();
raw.add("hello");
raw.add(42);
String s = (String) raw.get(1);    // ClassCastException at runtime

// With generics: checked at compile time, no casts
List<String> names = new ArrayList<>();
names.add("hello");
// names.add(42);                  // compile error
String first = names.get(0);
```

</details>
<details><summary>

### How do you declare a generic class?
</summary>

**Example:**

```java
public class ApiResponse<T> {
    private final T data;
    private final String error;

    private ApiResponse(T data, String error) { this.data = data; this.error = error; }
    public static <T> ApiResponse<T> ok(T data) { return new ApiResponse<>(data, null); }
    public static <T> ApiResponse<T> fail(String err) { return new ApiResponse<>(null, err); }
    public T getData() { return data; }
}

ApiResponse<User> res = ApiResponse.ok(new User("Asha"));
User u = res.getData();      // no cast needed
```

</details>
<details><summary>

### What are the restrictions in using a generic type that is declared in a class declaration?
</summary>

**Example:**

```java
class Box<T> {
    // T value = new T();              // can't instantiate a type parameter
    // static T cached;                // can't use T in a static field
    // T[] arr = new T[10];            // can't create a generic array
    // if (obj instanceof T) {}        // can't use instanceof with T (type erasure)
}
// List<int> nums;                     // primitives not allowed: use List<Integer>
```

</details>
<details><summary>

### How can we restrict Generics to a subclass of a particular class?
</summary>

**Example:**

```java
// Upper bound: T must be Number or a subclass
static <T extends Number> double sum(List<T> nums) {
    return nums.stream().mapToDouble(Number::doubleValue).sum();
}
sum(List.of(1, 2, 3));        // Integer ok
sum(List.of(1.5, 2.5));       // Double ok
// sum(List.of("a"));         // compile error

// Wildcard version for reading ("producer extends"):
static double total(List<? extends Number> nums) { return nums.stream().mapToDouble(Number::doubleValue).sum(); }
```

</details>
<details><summary>

### How can we restrict Generics to a superclass of a particular class?
</summary>

**Example:**

```java
// Lower bound: accepts List<Integer>, List<Number>, List<Object> ("consumer super")
static void addNumbers(List<? super Integer> target) {
    target.add(1);
    target.add(2);
}
List<Number> numbers = new ArrayList<>();
addNumbers(numbers);   // ok
// PECS rule: Producer Extends, Consumer Super  (e.g. Collections.copy(dest super, src extends))
```

</details>
<details><summary>

### Can you give an example of a generic method?
</summary>

**Example:**

```java
public static <T extends Comparable<T>> T max(List<T> items) {
    T best = items.get(0);
    for (T item : items) if (item.compareTo(best) > 0) best = item;
    return best;
}
System.out.println(max(List.of(3, 9, 4)));          // 9
System.out.println(max(List.of("kiwi", "apple")));  // kiwi
```

</details>
