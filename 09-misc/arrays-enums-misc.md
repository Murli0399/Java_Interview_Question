<details><summary>

## [Easy] What are the default values in an array?
</summary>

When you create an array with `new`, every element gets the default value of its type:

| Element type | Default |
|---|---|
| `byte`, `short`, `int`, `long` | `0` |
| `float`, `double` | `0.0` |
| `char` | `'\u0000'` (the null character) |
| `boolean` | `false` |
| Any object reference (`String`, `Integer`, custom classes) | `null` |

The same defaults apply to instance and static fields. **Local variables** get no default; using one before assignment is a compile error.

**Example:**

```java
int[] ints = new int[2];           // [0, 0]
double[] ds = new double[2];       // [0.0, 0.0]
boolean[] flags = new boolean[2];  // [false, false]
char[] cs = new char[2];           // ['\u0000', '\u0000']
String[] strs = new String[2];     // [null, null] - any object type defaults to null
System.out.println(Arrays.toString(ints) + Arrays.toString(strs));
```

</details>

<details><summary>

## [Easy] How do you print the content of an array?
</summary>

There are two ways to print the contents of an array in Java:

- Using a for loop
- Using the Arrays.toString() method

### Using a for loop

1. Declare and initialize an array.
2. Create a for loop that iterates through the array.
3. Inside the for loop, print the current element of the array.

Example:

```
int[] array = {1, 2, 3, 4, 5};

for (int i = 0; i < array.length; i++) {
  System.out.println(array[i]);
}
```

### Using the Arrays.toString() method

1. Import the java.util.Arrays class.
2. Call the Arrays.toString() method on the array.
3. Print the result of the Arrays.toString() method.

Example:

```
import java.util.Arrays;

int[] array = {1, 2, 3, 4, 5};

System.out.println(Arrays.toString(array));
```

The output of both methods will be the same.
</details>

<details><summary>

## [Easy] How do you compare two arrays?
</summary>

`==` and `array1.equals(array2)` only compare **references**, so they are false for two different arrays with the same content. Use the `Arrays` helpers:

- **`Arrays.equals(a, b)`** – true if both have the same length and equal elements in the same order. Different lengths simply return `false`.
- **`Arrays.deepEquals(a, b)`** – for nested arrays (`int[][]`).
- **`Arrays.compare(a, b)`** (Java 9) – lexicographic comparison returning a **negative, zero or positive** number (like `compareTo`).
- **`Arrays.mismatch(a, b)`** (Java 9) – index of the first difference, or `-1` if equal.

```java
int[] a = {1, 2, 3};
int[] b = {1, 2, 3};
int[] c = {1, 2, 4};

System.out.println(a == b);                 // false - different objects
System.out.println(Arrays.equals(a, b));    // true
System.out.println(Arrays.compare(a, c) < 0);   // true - a comes before c
System.out.println(Arrays.mismatch(a, c));  // 2

int[][] g1 = {{1}, {2}};
int[][] g2 = {{1}, {2}};
System.out.println(Arrays.equals(g1, g2));      // false - compares inner array references
System.out.println(Arrays.deepEquals(g1, g2));  // true
```

A manual loop must check lengths first, otherwise it can throw `ArrayIndexOutOfBoundsException`.

</details>

<details><summary>

## [Easy] What is an enum?
</summary>

An **enum** is a special class with a fixed set of named constants, such as days of the week, order statuses or HTTP methods. Each constant is a `public static final` instance of the enum.

```java
enum OrderStatus {
	PLACED("Order received"), SHIPPED("On the way"), DELIVERED("Delivered");

	private final String label;                       // enums can have fields,
	OrderStatus(String label) { this.label = label; } // constructors (always private)
	public String label() { return label; }           // and methods

	public boolean isFinal() { return this == DELIVERED; }
}

OrderStatus s = OrderStatus.valueOf("SHIPPED");
System.out.println(s.label() + " " + s.ordinal());   // On the way 1
for (OrderStatus st : OrderStatus.values()) System.out.println(st);
```

Facts interviewers ask about:
- Enums implicitly extend `java.lang.Enum`, so they **can't extend another class**, but they **can implement interfaces**.
- You can't create enum instances with `new`; constructors are implicitly private.
- Compare with `==` (safe, since each constant is a singleton).
- Use `EnumMap` / `EnumSet` for fast, compact maps and sets keyed by enum.
- An enum with one constant is the recommended thread-safe, serialization-safe **singleton**.

</details>

<details><summary>

## [Easy] Can you use a switch statement around an enum?
</summary>

Yes. In a `switch` on an enum you write the constant names **without** the enum prefix (`case MONDAY`, not `case Day.MONDAY` in the classic syntax).

Points to remember:
- Enum constants are implicitly `public static final`.
- Enums can have fields, constructors and methods, and can implement interfaces, but can't extend a class (they already extend `Enum`).
- You can't create enum instances with `new`.
- With Java 14+ switch **expressions**, the compiler checks you covered every constant (no `default` needed); if a new constant is added later, the code stops compiling instead of silently doing nothing.

**Example:**

```java
enum Status { ACTIVE, SUSPENDED, CLOSED }

String label(Status s) {
    return switch (s) {               // Java 14+ switch expression
        case ACTIVE -> "Active";
        case SUSPENDED -> "On hold";
        case CLOSED -> "Closed";
    };                                // compiler checks all enum values are covered
}
```

</details>

<details><summary>

## [Easy] What is tokenizing?
</summary>

**Tokenizing** means splitting a string into smaller pieces (tokens) using a delimiter, for example splitting a CSV line on commas or a sentence on spaces. In Java you usually use `String.split(regex)`, `Scanner`, or the legacy `StringTokenizer`. Note that `split` takes a **regular expression**, so special characters like `.` or `|` must be escaped (`split("\\.")`).

**Example:**

```java
String csv = "id,name,,city";
String[] parts = csv.split(",");        // [id, name, , city] (keeps empty token)
String[] words = "  java   spring ".trim().split("\\s+"); // [java, spring]
```

</details>

<details><summary>

## [Easy] Can you give an example of tokenizing?
</summary>

`Scanner` reads typed tokens from a string or stream; `StringTokenizer` is legacy (it doesn't support regex) and `split()` is preferred in new code.

**Example:**

```java
Scanner sc = new Scanner("10 20 30");
int sum = 0;
while (sc.hasNextInt()) sum += sc.nextInt();
System.out.println(sum);   // 60

StringTokenizer st = new StringTokenizer("a;b;c", ";");   // legacy; prefer split()
while (st.hasMoreTokens()) System.out.println(st.nextToken());
```

</details>

<details><summary>

## [Medium] What are asserts used for?
</summary>

`assert condition : message;` checks an assumption during development and testing. If the condition is false, it throws `AssertionError`. Assertions are **disabled by default** and run only when the JVM starts with `-ea` (enable assertions).

**Example:**

```java
int divide(int a, int b) {
    assert b != 0 : "divisor must not be zero";   // checked only when run with: java -ea
    return a / b;
}
```

</details>

<details><summary>

## [Medium] When should asserts be used?
</summary>

Use asserts only for **internal invariants** that should be impossible if your code is correct (e.g. a private method's precondition). Don't use them to validate public method arguments, user input or anything with side effects, because they are switched off in production; throw `IllegalArgumentException`/`IllegalStateException` instead.

**Example:**

```java
// OK: internal invariants you believe can never be false
private void rebalance(Node n) {
    assert n.height >= 0 : "height corrupted";
}

// NOT OK: validating public input (asserts are disabled by default in production)
public void setAge(int age) {
    if (age < 0) throw new IllegalArgumentException("age must be >= 0");  // use this instead
}
```

</details>
