# Wrapper classes and casting

<details><summary>
	
## [Easy] What are wrapper classes?
</summary>

Wrapper classes in Java are a set of classes that encapsulate primitive data types (such as int, float, char, etc.) and provide object-oriented representations for them. They allow primitive types to be used as objects in Java programs by wrapping them within instances of the corresponding wrapper classes.
Here are the wrapper classes for each primitive type:

- Boolean: Represents the boolean type.
- Byte: Represents the byte type.
- Short: Represents the short type.
- Integer: Represents the int type.
- Long: Represents the long type.
- Float: Represents the float type.
- Double: Represents the double type.
- Character: Represents the char type.

**Example:**

```java
int primitive = 10;
Integer wrapped = Integer.valueOf(primitive);   // boxing
int back = wrapped.intValue();                  // unboxing

List<Integer> list = new ArrayList<>();         // collections need objects, not primitives
list.add(5);                                    // autoboxed

int parsed = Integer.parseInt("42");            // utility methods live in wrappers
System.out.println(Integer.MAX_VALUE);          // 2147483647
```

</details>

<details><summary>
	
## [Easy] Why do we need Wrapper Classes in Java?
</summary>

The Java programming language treats primitive types and objects differently. Primitive types are not considered objects and do not have the capabilities of objects, such as methods and additional functionalities. However, there are situations where we may need to treat primitive types as objects, such as when working with collections, generics, or when using methods that require objects as arguments.
Wrapper classes bridge this gap by providing a way to wrap primitive types and use them as objects.

**Example:**

```java
Map<String, Integer> stock = new HashMap<>();   // generics only accept objects
Integer qty = stock.get("apple");               // null means "absent" - an int can't be null

// Integer cache pitfall: values -128..127 are cached
Integer a = 127, b = 127;
Integer c = 128, d = 128;
System.out.println(a == b);       // true  (same cached object)
System.out.println(c == d);       // false (different objects!)
System.out.println(c.equals(d));  // true  -> always compare wrappers with equals()

// Unboxing null throws NullPointerException
Integer missing = stock.get("mango");
// int n = missing;               // NullPointerException
```

</details>

<details><summary>
	
## [Easy] What is Auto Boxing?
</summary>

### Autoboxing
The automatic conversion of primitive types to the object of their corresponding wrapper classes is known as autoboxing. For example – conversion of int to Integer, long to Long, double to Double, etc. 

```java
int num = 10;
Integer myInteger = num;  // Autoboxing int to Integer
```

### Unboxing
It is just the reverse process of autoboxing. Automatically converting an object of a wrapper class to its corresponding primitive type is known as unboxing. For example – conversion of Integer to int, Long to long, Double to double, etc. 
	
```java
Integer myInteger = 20;
int num = myInteger;  // Unboxing Integer to int
```

</details>

<details><summary>
	
## [Easy] What is Casting?
</summary>

Casting is a method or process that converts a data type into another data type in both ways manually and automatically. The automatic conversion is done by the compiler and manual conversion performed by the programmer.
Convert a value from one data type to another data type is known as type casting.

Types of Type Casting
There are two types of type casting:

Widening Type Casting (Implicit Casting)
Narrowing Type Casting (Explicit Casting)

**Example:**

```java
int i = 100;
long l = i;              // implicit widening: int -> long
double d = 9.99;
int whole = (int) d;     // explicit narrowing: 9 (decimal lost)
byte overflow = (byte) 200;  // -56 (wraps around)

Object o = "text";
String s = (String) o;   // reference downcast, safe here
// Integer n = (Integer) o; // ClassCastException at runtime
if (o instanceof String str) System.out.println(str.length()); // safe pattern-matching check
```

</details>

<details><summary>
	
## [Easy] What is Implicit Casting?
</summary>

**Implicit (widening) casting** converts a smaller primitive type to a larger one automatically. It is also called *widening conversion* (not "down casting"; up/down casting refers to class references).

Widening paths:

```text
byte → short → int → long → float → double
              char ↗
```

`char` widens to `int` (and beyond), but `byte`/`short` cannot widen to `char`, because `char` is unsigned.

```java
int value = 100;
long number = value;   // int -> long
float f = 100;         // int -> float
double d = 'A';        // char -> double (65.0)
```

Widening never loses the *magnitude*, but `int → float`, `long → float` and `long → double` can lose **precision**:

```java
int big = 123_456_789;
float f2 = big;
System.out.println((int) f2);   // 123456792
```

</details>

<details><summary>
	
## [Easy] What is Explicit Casting?
</summary>

**Explicit (narrowing) casting** converts a larger type to a smaller one. The programmer must write the cast, because data can be lost. It is also called *narrowing conversion* (not "up casting").

```text
double → float → long → int → short → byte
                         int → char
```

```java
long number1 = 25678;
int number2 = (int) number1;   // explicit
// int x = 35.35;              // COMPILER ERROR
int x = (int) 35.35;           // 35 - decimal part truncated, not rounded
```

If the value doesn't fit, the extra high-order bits are discarded:

```java
int bigValue = 280;
byte small = (byte) bigValue;
System.out.println(small);     // 24  (280 - 256), only the low 8 bits remain
```

For references, **upcasting** (subclass → superclass) is implicit and always safe; **downcasting** (superclass → subclass) needs an explicit cast and can throw `ClassCastException`. Check first with `instanceof`.

</details>

<details><summary>
	
## [Medium] What are the different ways of creating Wrapper Class Instances?
</summary>

### 1. `valueOf()` (preferred)
```java
Integer i = Integer.valueOf(10);
Integer fromText = Integer.valueOf("100");
Boolean b = Boolean.valueOf(true);
```
`valueOf` can return **cached** instances: `Integer`, `Short`, `Byte`, `Long` cache -128 to 127, `Character` caches 0–127, and `Boolean` has only `TRUE`/`FALSE`.

### 2. Autoboxing
```java
Integer i = 10;      // compiler calls Integer.valueOf(10)
Double d = 3.14;
```

### 3. Parsing to a primitive (not a wrapper)
```java
int n = Integer.parseInt("42");     // returns int
double x = Double.parseDouble("3.5");
```

### 4. Constructors (deprecated)
`new Integer(10)` and `new Integer("100")` were **deprecated in Java 9 and marked for removal in Java 16**. They always create a new object and skip the cache. Don't use them in new code.

Wrapper objects are immutable; arithmetic on them unboxes, computes, and boxes a new object.

</details>

<details><summary>
	
## [Medium] What are the advantages of Auto Boxing?
</summary>

- **Less code:** primitives can be used directly with collections and generics (`list.add(5)`).
- **Reuse of cached objects:** autoboxing calls `valueOf()`, so values in the cache range (-128 to 127 for `Integer`) reuse the same object instead of allocating a new one.

```java
Integer nineC = 9;
Integer nineD = 9;
System.out.println(nineC == nineD);       // true  - 9 is cached, same object
Integer big1 = 1000;
Integer big2 = 1000;
System.out.println(big1 == big2);         // false - outside the cache, two objects
System.out.println(big1.equals(big2));    // true
```

**Pitfalls to mention in interviews:**
- Always compare wrappers with `equals()`, never `==`.
- Unboxing `null` throws `NullPointerException` (`int x = map.get("missing");`).
- Boxing inside hot loops (`Long sum = 0L; sum += i;`) creates many objects; use primitives there.

</details>
