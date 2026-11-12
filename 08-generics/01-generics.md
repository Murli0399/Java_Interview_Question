# Generics

<details><summary>

### [Easy] What are Generics?
</summary>

**Generics** (Java 5) let classes, interfaces and methods take **type parameters** (like `<T>`), so the same code works with different types while the compiler checks type safety.

```java
public <T> void printAll(List<T> items) { items.forEach(System.out::println); }

List<String> names = new ArrayList<>();   // only Strings allowed
names.add("Asha");
String first = names.get(0);              // no cast needed
```

Benefits:
- **Type safety at compile time:** wrong types are compile errors instead of `ClassCastException` at runtime.
- **No casts:** the compiler inserts them for you.
- **Reusable code:** one `Box<T>` or `Repository<T, ID>` for every type.

Generics are implemented with **type erasure**: type parameters exist only at compile time and are replaced by their bounds (usually `Object`) in the bytecode. So generics have **no runtime performance benefit or cost**; their value is correctness and readability.

</details>

<details><summary>

### [Easy] Why do we need Generics? Can you give an example of how Generics make a program more flexible?
</summary>

Without generics, collections hold `Object`, so you must cast on every read and mistakes show up only at runtime. With generics, one piece of code works for many types, and mistakes are caught by the compiler.

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

### [Easy] How do you declare a generic class?
</summary>

Put the type parameter(s) in angle brackets after the class name, then use them like normal types inside the class. Common names: `T` (type), `E` (element), `K`/`V` (key/value), `R` (result). The diamond `<>` lets the compiler infer the type when you create an instance.

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

### [Easy] Can you give an example of a generic method?
</summary>

A generic method declares its own type parameter **before the return type**, independent of the class. The compiler usually infers the type from the arguments.

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

<details><summary>

### [Medium] What are the restrictions in using a generic type that is declared in a class declaration?
</summary>

Because of type erasure, the type parameter `T` isn't available at runtime, which leads to these restrictions: you can't create `new T()` or `new T[]`, use `instanceof T`, declare `static` fields of type `T`, use primitives as type arguments (`List<int>`), create generic exception classes, or overload methods that differ only by generic type (`m(List<String>)` vs `m(List<Integer>)`).

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

### [Medium] How can we restrict Generics to a subclass of a particular class?
</summary>

Use an **upper bound**: `<T extends Number>` accepts `Number` or any subclass, and lets you call `Number`'s methods on `T`. For interfaces you also use `extends`, and you can combine bounds: `<T extends Number & Comparable<T>>`. With wildcards, `List<? extends Number>` accepts a list of any Number subtype, but you can only **read** from it ("producer extends").

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

### [Medium] How can we restrict Generics to a superclass of a particular class?
</summary>

Use a **lower-bounded wildcard**: `List<? super Integer>` accepts `List<Integer>`, `List<Number>` or `List<Object>`. You can safely **add** `Integer`s to it, but reading gives you only `Object` ("consumer super"). Lower bounds work only with wildcards (`? super T`), not with type parameter declarations.

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

### [Hard] What is type erasure?
</summary>

Java implements generics with **type erasure**: generic type information is checked by the compiler and then **removed** from the bytecode. Type parameters are replaced by their bound (`Object` if unbounded), and the compiler inserts casts where needed. This kept new generic code compatible with pre-Java 5 code.

Consequences:
- At runtime, `List<String>` and `List<Integer>` are the **same class**: `new ArrayList<String>().getClass() == new ArrayList<Integer>().getClass()` is `true`.
- You can't do `new T()`, `new T[10]`, `x instanceof List<String>`, or overload `m(List<String>)` and `m(List<Integer>)` (same erasure).
- Primitive type arguments aren't allowed (`List<int>`).
- The compiler may generate **bridge methods** to keep overriding working after erasure.

Workaround when you need the type at runtime: pass a `Class<T>` (`Class<T> type`) or a "type token" (e.g. Jackson's `TypeReference<List<User>>`, Spring's `ParameterizedTypeReference`).

```java
static <T> T create(Class<T> type) throws ReflectiveOperationException {
	return type.getDeclaredConstructor().newInstance();   // new T() is impossible; Class<T> works
}
```
</details>

<details><summary>

### [Hard] What is the difference between List<?>, List<Object> and List<? extends Number>?
</summary>

| Type | Accepts | Can read as | Can add |
|---|---|---|---|
| `List<Object>` | Only `List<Object>` (not `List<String>`!) | `Object` | Anything |
| `List<?>` (unbounded wildcard) | A list of **any** type | `Object` | Only `null` |
| `List<? extends Number>` | `List<Number>`, `List<Integer>`, `List<Double>`… | `Number` | Only `null` |
| `List<? super Integer>` | `List<Integer>`, `List<Number>`, `List<Object>` | `Object` | `Integer` |

Key point: generics are **invariant** – `List<String>` is **not** a subtype of `List<Object>`, even though `String` is a subtype of `Object`. Wildcards are how you write methods that accept families of generic types.

**PECS** – *Producer Extends, Consumer Super*: if a parameter **produces** values you read, use `? extends T`; if it **consumes** values you write, use `? super T`. Example: `Collections.copy(List<? super T> dest, List<? extends T> src)`.

```java
static double sum(List<? extends Number> nums) {          // producer: we only read
	double total = 0;
	for (Number n : nums) total += n.doubleValue();
	return total;
}

static void fill(List<? super Integer> target) {          // consumer: we only write
	for (int i = 0; i < 3; i++) target.add(i);
}
```
</details>

<details><summary>

### [Hard] What is a bounded type parameter with multiple bounds?
</summary>

A type parameter can have **one class bound plus any number of interface bounds**, joined with `&`. The class (if any) must come first.

```java
static <T extends Number & Comparable<T>> T maxOf(List<T> values) {
	T best = values.get(0);
	for (T v : values) if (v.compareTo(best) > 0) best = v;   // Comparable method
	System.out.println(best.doubleValue());                    // Number method
	return best;
}

maxOf(List.of(3, 9, 4));      // 9
```

The erasure of `T` is the **first** bound (`Number` here).
</details>
