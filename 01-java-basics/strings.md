# Strings

<details><summary>
	
## [Easy] Are all String’s immutable?
</summary>

Yes. Every `String` object is immutable: once created, its characters never change. Methods like `toUpperCase()`, `concat()` or `replace()` return a **new** String and leave the original untouched.

Why Java made String immutable:
- **String pool:** many references can safely share one literal (`"Sachin"`); if one reference could change it, every other reference would see the change.
- **Security:** values like file paths, URLs, class names and DB usernames can't be altered after validation.
- **Thread safety:** immutable objects can be shared across threads without synchronization.
- **Hash caching:** `hashCode()` is computed once and cached, which makes String a fast, reliable `HashMap` key.

Note: the *reference* can be reassigned (`s = s.toUpperCase()`); the *object* never changes.

**Example:**

```java
String s = "java";
s.toUpperCase();              // returns a NEW String, s is unchanged
System.out.println(s);        // java
s = s.toUpperCase();          // reassign the reference to the new object
System.out.println(s);        // JAVA

String a = "hi";
String b = "hi";
String c = new String("hi");
System.out.println(a == b);       // true  (same pooled literal)
System.out.println(a == c);       // false (new object on the heap)
System.out.println(a.equals(c));  // true  (same content)
System.out.println(a == c.intern()); // true (intern returns the pooled copy)
```

</details>

<details><summary>
	
## [Easy] What are differences between String and StringBuffer?
</summary>

| | String | StringBuffer |
|---|---|---|
| Mutability | Immutable | Mutable (modified in place) |
| Thread safety | Thread-safe *because* it is immutable | Thread-safe because its methods are `synchronized` |
| Concatenation | Creates a new object each time | Appends to the same buffer |
| Performance for many modifications | Poor | Good (slower than `StringBuilder` due to locking) |
| `equals()` | Compares content | Not overridden: compares references (use `compareTo` or `toString().equals`) |

Use `String` for values that don't change, `StringBuilder` for building strings in one thread, and `StringBuffer` only when one buffer really is shared across threads.

**Example:**

```java
String s = "a";
s.concat("b");                 // new object returned, s still "a"

StringBuffer sb = new StringBuffer("a");
sb.append("b");                // same object modified in place
System.out.println(sb);        // ab
```

</details>

<details><summary>
	
## [Easy] What are differences between StringBuilder and StringBuffer?
</summary>

StringBuilder is not thread-safe, while StringBuffer is thread-safe.
StringBuilder provides better performance due to the absence of synchronization.
Use StringBuilder in single-threaded scenarios or when manual synchronization is applied.
Use StringBuffer in multi-threaded scenarios where thread safety is required.

**Example:**

```java
// StringBuilder: not synchronized, faster -> use for local string building
StringBuilder csv = new StringBuilder();
for (String col : List.of("id", "name", "city")) csv.append(col).append(',');
csv.setLength(csv.length() - 1);   // remove trailing comma
System.out.println(csv);           // id,name,city

// StringBuffer: synchronized methods, only if one instance is shared between threads
StringBuffer shared = new StringBuffer();
```

</details>

<details><summary>
	
## [Easy] Can you give examples of different utility methods in String class?
</summary>

| Method | What it does | Example |
|---|---|---|
| `length()` | Number of chars | `"java".length()` → 4 |
| `charAt(i)` | Char at index | `"java".charAt(1)` → `'a'` |
| `substring(b, e)` | Part of string, `e` exclusive | `"backend".substring(0, 4)` → `"back"` |
| `indexOf / lastIndexOf` | Position of a char/substring | `"banana".indexOf("an")` → 1 |
| `contains`, `startsWith`, `endsWith` | Search | `"api/v1".startsWith("api")` → true |
| `equals`, `equalsIgnoreCase`, `compareTo` | Compare | `"a".compareTo("b")` → -1 |
| `toUpperCase`, `toLowerCase` | Case | |
| `trim()` / `strip()` (Java 11, Unicode-aware) | Remove surrounding whitespace | |
| `isEmpty()` / `isBlank()` (Java 11) | Empty / only whitespace | `"  ".isBlank()` → true |
| `replace`, `replaceAll` (regex) | Replace | `"a-b".replace("-", "_")` |
| `split(regex)` | Split into array | `"a,b".split(",")` |
| `String.join`, `String.valueOf` | Build / convert | `String.join("-", "a", "b")` → `"a-b"` |
| `repeat(n)` (Java 11), `lines()` (Java 11) | Repeat / split into lines | `"ab".repeat(2)` → `"abab"` |
| `chars()` | `IntStream` of characters | `"aab".chars().filter(c -> c == 'a').count()` → 2 |
| `intern()` | Returns the pooled copy | |

</details>

<details><summary>
	
## [Medium] Where are string values stored in memory?
</summary>

String is a class and strings in java treated as an object, hence the object of String class will be stored in Heap area. But depends on how we are create them. So we have two method for creating String value.

Approach 1
In the below example we are directly referencing a String literal.
	
```java
String str1 = "value";
```

This value will be stored in a "String constant pool" – which is inside the 
Heap memory. If compiler finds a String literal, JVM checks the if String constant pool if exists in the pool. it is reused.

Approach 2
However, if new operator is used to create string object, the new object is created on the heap. There will not be any case to reuse of values.

```java
//String Object - created on the heap
String str2 = new String("value");
```

</details>

<details><summary>
	
## [Medium] Why should you be careful about String Concatenation(+) operator in Loops?
</summary>

Because `String` is immutable, `s = s + x` inside a loop creates a **new String object every iteration** and copies all existing characters into it.

- For n iterations the total copying is 1 + 2 + … + n characters, so the cost is **O(n²)** (quadratic, not exponential).
- Each iteration also leaves a garbage object behind, increasing GC work.

```java
String s3 = "Value1";
String s2 = "Value2";

for (int i = 0; i < 100000; ++i) {
	s3 = s3 + s2;   // a new String (and a growing copy) every time
}
```

About 100,000 intermediate String objects are created. A single `a + b + c` outside a loop is fine: the compiler optimises it (since Java 9 via `invokedynamic` / `StringConcatFactory`).

</details>

<details><summary>
	
## [Medium] How do you avoid the cost of String concatenation in loops?
</summary>

Use a mutable `StringBuilder` (or `StringBuffer` if one instance is shared between threads). It appends into an internal resizable buffer, so the loop becomes O(n).

```java
StringBuilder s3 = new StringBuilder("Value1");
String s2 = "Value2";

for (int i = 0; i < 100000; ++i) {
	s3.append(s2);
}
String result = s3.toString();
```

Other options: `String.join(",", list)`, `Collectors.joining(",")`, or `StringJoiner` when building delimited text.

</details>