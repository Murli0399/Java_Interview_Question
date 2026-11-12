# Core Java essentials

<details><summary>

## [Easy] What is the main method signature and why is it public static void?
</summary>

```java
public static void main(String[] args)
```

- **`public`** – the JVM, which is outside your class, must be able to call it.
- **`static`** – the JVM calls it without creating an object of the class first.
- **`void`** – it returns nothing; exit codes are set with `System.exit(code)`.
- **`String[] args`** – command-line arguments (`String... args` also works).

Variations that still work: `final`, `synchronized` or `strictfp` modifiers, and any parameter name. Since **Java 21 (preview) / Java 25 (final, JEP 512)**, simple programs can use an instance `void main()` with no `static` or arguments, but in interviews the classic signature is what's expected.
</details>

<details><summary>

## [Easy] What does the static keyword mean for variables, methods, blocks and classes?
</summary>

`static` means "belongs to the class, not to an instance".

| Usage | Meaning |
|---|---|
| **Static variable** | One copy shared by all instances; created when the class is initialised |
| **Static method** | Called on the class (`Math.max`); has no `this`, so it can't use instance fields/methods directly; can't be overridden (only hidden) |
| **Static block** | Runs once when the class is initialised, to set up static state |
| **Static nested class** | A nested class that doesn't need an outer instance |
| **Static import** | `import static java.lang.Math.*;` to use static members without the class name |

```java
public class IdGenerator {
	private static long next;                 // shared counter
	static { next = 1000; }                   // runs once

	public static synchronized long nextId() { return next++; }
}

long id = IdGenerator.nextId();               // no object needed
```

Common follow-ups: a static method **can't** access instance variables directly; local variables **can't** be static; static fields of mutable objects are a common source of memory leaks and thread-safety bugs.
</details>

<details><summary>

## [Easy] What is the difference between this and super?
</summary>

| | `this` | `super` |
|---|---|---|
| Refers to | The current object | The parent-class part of the current object |
| Field access | `this.name` – distinguishes a field from a parameter | `super.name` – parent's field hidden by a child field |
| Method call | `this.save()` – current class's method | `super.save()` – parent's version of an overridden method |
| Constructor call | `this(...)` – another constructor of the same class | `super(...)` – a parent constructor |
| Rule | `this(...)`/`super(...)` must be the first statement; you can use only one of them | |

Neither can be used in a `static` context, because there is no current object.

```java
class Account {
	protected double balance;
	void describe() { System.out.println("Account"); }
}

class SavingsAccount extends Account {
	private final double rate;

	SavingsAccount(double rate) { this(rate, 0); }                       // this(...)
	SavingsAccount(double rate, double opening) {
		super();                                                         // super(...)
		this.rate = rate;                                                // this.field
		this.balance = opening;
	}

	@Override
	void describe() {
		super.describe();                                                // parent's method
		System.out.println("Savings at " + rate + "%");
	}
}
```
</details>

<details><summary>

## [Easy] What is the difference between == and equals() for Strings?
</summary>

- **`==`** compares **references**: are both variables pointing to the same object?
- **`equals()`** compares **content**: do both strings have the same characters?

```java
String a = "java";                 // from the string pool
String b = "java";                 // same pooled object
String c = new String("java");     // new object on the heap
String d = c.intern();             // pooled copy

System.out.println(a == b);        // true  - same pooled literal
System.out.println(a == c);        // false - different objects
System.out.println(a.equals(c));   // true  - same content
System.out.println(a == d);        // true  - intern() returns the pooled instance

String e = "ja" + "va";            // compile-time constant -> pooled
System.out.println(a == e);        // true
String part = "ja";
String f = part + "va";            // computed at runtime -> new object
System.out.println(a == f);        // false
```

Always use `equals()` (or `equalsIgnoreCase()`) to compare strings. Write `"ACTIVE".equals(status)` to avoid a `NullPointerException` when `status` is null, or use `Objects.equals(a, b)`.
</details>

<details><summary>

## [Easy] What are varargs?
</summary>

**Varargs** (variable arguments, Java 5) let a method accept zero or more arguments of a type, written as `Type... name`. Inside the method it's an array.

```java
static int sum(int... numbers) {
	int total = 0;
	for (int n : numbers) total += n;
	return total;
}

sum();               // 0
sum(1, 2, 3);        // 6
sum(new int[]{4, 5}); // 9 - an array works too
```

Rules:
- Only **one** varargs parameter per method, and it must be the **last** parameter: `log(String format, Object... args)`.
- Overload resolution tries exact matches and widening/boxing before varargs.
- Generic varargs (`List<String>...`) can trigger "heap pollution" warnings; `@SafeVarargs` suppresses them for methods that are safe.

Examples in the JDK: `String.format`, `List.of(...)`, `Arrays.asList(...)`, `System.out.printf`.
</details>

<details><summary>

## [Easy] What is the difference between final, finally and finalize?
</summary>

| | What it is | Purpose |
|---|---|---|
| `final` | Keyword | Variable can't be reassigned, method can't be overridden, class can't be extended |
| `finally` | Block after `try`/`catch` | Code that always runs (cleanup), whether or not an exception occurs |
| `finalize()` | Method in `Object` | Called by the GC before reclaiming an object. **Deprecated (Java 9) and marked for removal (Java 18)**; unreliable and slow |

Use try-with-resources for cleanup and `java.lang.ref.Cleaner` for the rare cases that need a post-GC hook.
</details>

<details><summary>

## [Medium] Is Java pass-by-value or pass-by-reference?
</summary>

Java is **always pass-by-value**. For objects, the value that gets copied is the **reference** (the address of the object). So:

- A method **can change the object's state** through the copied reference (both references point to the same object).
- A method **cannot make the caller's variable point to a different object**, because reassigning the parameter changes only the copy.

```java
static void rename(StringBuilder sb) { sb.append(" Khaire"); }        // modifies the shared object
static void replace(StringBuilder sb) { sb = new StringBuilder("X"); }   // reassigns the local copy only
static void increment(int n) { n++; }                                    // primitive copy

StringBuilder name = new StringBuilder("Murli");
rename(name);
System.out.println(name);    // Murli Khaire
replace(name);
System.out.println(name);    // Murli Khaire (unchanged)

int count = 5;
increment(count);
System.out.println(count);   // 5
```

Interview one-liner: "Java passes a copy of the variable. For primitives that's the value; for objects it's a copy of the reference."
</details>

<details><summary>

## [Medium] How do you create an immutable class in Java?
</summary>

An immutable object's state can't change after construction. Rules:

1. Declare the class **`final`** (so subclasses can't add mutable behaviour).
2. Make all fields **`private final`**.
3. **No setters** or other methods that modify state.
4. Initialise everything in the constructor, and **defensively copy** mutable inputs (lists, dates, arrays).
5. **Return copies or unmodifiable views** of mutable fields from getters.
6. Don't let `this` escape during construction.

```java
public final class Employee {
	private final String name;
	private final List<String> skills;

	public Employee(String name, List<String> skills) {
		this.name = name;
		this.skills = List.copyOf(skills);       // defensive, unmodifiable copy
	}

	public String getName() { return name; }
	public List<String> getSkills() { return skills; }   // already unmodifiable

	public Employee withSkill(String skill) {      // "modification" returns a new object
		List<String> updated = new ArrayList<>(skills);
		updated.add(skill);
		return new Employee(name, updated);
	}
}
```

Benefits: thread-safe without locks, safe as `HashMap` keys, easy to cache and reason about. Java **records** (`record Employee(String name, List<String> skills)`) give you most of this automatically, but you still need a defensive copy in the compact constructor for mutable components.
</details>

<details><summary>

## [Medium] What is a marker interface? Give examples.
</summary>

A **marker interface** has **no methods**. It just "marks" a class so that the JVM or a framework treats it specially, usually checked with `instanceof`.

Examples from the JDK:
- **`Serializable`** – objects can be serialized by `ObjectOutputStream`.
- **`Cloneable`** – `Object.clone()` is allowed; otherwise it throws `CloneNotSupportedException`.
- **`RandomAccess`** – the list supports fast indexed access (`ArrayList` has it, `LinkedList` doesn't), so algorithms can choose a strategy.
- **`Remote`** (RMI).

```java
public interface Auditable { }                       // custom marker

class Order implements Auditable { }

void save(Object entity) {
	if (entity instanceof Auditable) writeAuditLog(entity);
	repository.save(entity);
}
```

Modern code often uses **annotations** instead (`@Entity`, `@Transactional`), since they can carry attributes and don't affect the type hierarchy. A marker interface still has one advantage: it's a real type, so the compiler can check it (e.g. a method parameter of type `Serializable`).
</details>

<details><summary>

## [Medium] What is the difference between shallow copy and deep copy? How does clone() work?
</summary>

- **Shallow copy:** a new object whose fields are copied as-is. Primitive values are copied, but **references point to the same nested objects**, so changing a nested object affects both copies.
- **Deep copy:** nested mutable objects are copied too, so the two objects are fully independent.

`Object.clone()` makes a **shallow** copy. To use it, the class must implement `Cloneable` (otherwise `CloneNotSupportedException`) and usually overrides `clone()` as `public`.

```java
class Team implements Cloneable {
	String name;
	List<String> members = new ArrayList<>();

	@Override
	public Team clone() {
		try {
			Team copy = (Team) super.clone();              // shallow: same members list
			copy.members = new ArrayList<>(this.members);  // make it deep for this field
			return copy;
		} catch (CloneNotSupportedException e) {
			throw new AssertionError(e);
		}
	}
}
```

`clone()` is widely considered a flawed API (it bypasses constructors, has awkward checked exceptions, and doesn't work with `final` fields). Prefer a **copy constructor** (`new Team(otherTeam)`), a static factory (`Team.copyOf(t)`), or immutable objects that never need copying.
</details>

<details><summary>

## [Medium] What are records and sealed classes, and why were they added?
</summary>

**Records (Java 16)** are concise, immutable data carriers. `record Point(int x, int y) {}` generates a canonical constructor, `private final` fields, accessors (`x()`, `y()`), `equals`, `hashCode` and `toString`. They can't extend another class (they implicitly extend `Record`) but can implement interfaces and add methods or validation in a compact constructor.

**Sealed classes/interfaces (Java 17)** restrict which classes may extend or implement them, using `permits`. The compiler then knows the complete set of subtypes, so a `switch` over them can be checked for exhaustiveness.

```java
sealed interface PaymentResult permits Success, Failure { }
record Success(String txnId) implements PaymentResult { }
record Failure(String reason, boolean retryable) implements PaymentResult { }

String describe(PaymentResult r) {
	return switch (r) {                                   // no default needed
		case Success s -> "Paid: " + s.txnId();
		case Failure f when f.retryable() -> "Retry: " + f.reason();
		case Failure f -> "Failed: " + f.reason();
	};
}
```

Together they model **algebraic data types**: closed sets of immutable variants, handled safely with pattern matching. Typical uses: DTOs, API responses, domain events, results that are either success or failure.
</details>
