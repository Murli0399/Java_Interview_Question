# OOP basics

<details><summary>

## [Easy] What is a Class?
</summary>

In object-oriented programming, a class is a blueprint or template that defines the structure and behavior of objects. It serves as a blueprint for creating instances, also known as objects, which are individual occurrences based on the class.

A class encapsulates data, known as attributes or fields, and defines the operations, known as methods or functions, that can be performed on that data. It provides a way to organize related data and behavior into a cohesive unit.

**Example:**

```java
public class BankAccount {                 // class = blueprint
    private final String accountNo;       // state (fields)
    private double balance;

    public BankAccount(String accountNo) { this.accountNo = accountNo; }

    public void deposit(double amount) {  // behaviour (methods)
        if (amount <= 0) throw new IllegalArgumentException("Amount must be positive");
        balance += amount;
    }

    public double getBalance() { return balance; }
}
```

</details>

<details><summary>

## [Easy] What is an Object?
</summary>

In object-oriented programming, an object is an instance of a class. It represents a specific occurrence or entity based on the structure and behavior defined by its class. An object combines data, known as attributes or properties, with the methods or functions that operate on that data.

**Example:**

```java
BankAccount a = new BankAccount("ACC-1");   // two objects (instances) of one class
BankAccount b = new BankAccount("ACC-2");
a.deposit(500);
System.out.println(a.getBalance());   // 500.0
System.out.println(b.getBalance());   // 0.0 - each object has its own state
```

</details>

<details><summary>

## [Easy] What is state of an Object?
</summary>

The state of an object refers to the set of values stored in its attributes or instance variables at a given point in time. It represents the current snapshot of the object's data. The state of an object can change over time as its attributes are modified.

**Example:**

```java
BankAccount acc = new BankAccount("ACC-1");  // state: balance = 0.0
acc.deposit(1000);                           // state changes: balance = 1000.0
```

</details>

<details><summary>

## [Easy] What is behavior of an Object?
</summary>

The behavior of an object refers to the actions or operations that an object can perform. It represents the functionality or capabilities associated with an object based on its class definition. The behavior is defined by the methods or functions defined within the class.

**Example:**

```java
acc.deposit(200);              // behaviour = methods that act on the object's state
double b = acc.getBalance();
```

</details>

<details><summary>

## [Easy] What is the super class of every class in Java?
</summary>

In Java, the superclass of every class is the Object class. The Object class is at the top of the class hierarchy and serves as the root class for all other classes in Java.

The Object class is defined in the java.lang package and provides a set of common methods and behaviors that are inherited by all classes. These methods include toString(), equals(), hashCode(), getClass(), and more.

Since every class in Java implicitly or explicitly extends the Object class, all objects in Java inherit the methods and behavior defined in Object. This allows for certain fundamental operations and provides a common interface for all objects in Java.

It's important to note that even if a class doesn't explicitly extend any other class, it still inherits from Object by default. This inheritance relationship establishes a foundation for the object-oriented features and functionality in Java.
	
```java
// Let’s look at a simple example:

String str = "Testing";
System.out.println(str.toString());
System.out.println(str.hashCode());
System.out.println(str.getClass()); // class java.lang.String

if(str instanceof Object){
	System.out.println("I extend Object");//Will be printed
}
```

In the above example, toString and hashCode come from Object (String overrides both) and getClass is inherited as-is. Note: clone() is protected in Object, so str.clone() would not compile.
</details>

<details><summary>

## [Easy] Explain about toString method ?
</summary>

The toString() method is a method defined in the Object class in Java. It is inherited by all classes in Java, as every class is a subclass of Object. The toString() method is used to obtain a string representation of an object.

By default, the toString() method in the Object class returns a string that consists of the class name, followed by an "at" symbol (@), and the hash code of the object in hexadecimal format. For example, ClassName@6e1408c6.

However, it is common practice to override the toString() method in custom classes to provide a more meaningful and human-readable representation of the object's state. By overriding the toString() method, you can define the format and content of the string representation according to your requirements.
	
```java
class Animal {
	public Animal(String name, String type) {
		this.name = name;
		this.type = type;
	}
	String name;
	String type;
	public String toString() {
		return "Animal [name=" + name + ", type=" + type + "]";
	}
}
// Run this piece of code:
Animal animal = new Animal("Tommy","Dog");
System.out.println(animal);//Animal [name=Tommy, type=Dog]
```

</details>

<details><summary>

## [Easy] Explain inheritance with Examples?
</summary>

Inheritance lets one **class** acquire the fields and methods of another class using `extends`. The child class reuses the parent's code and can add or override behaviour. It models an **IS-A** relationship (a `Hero` IS-A `Actor`).

```java
public class Actor {
	public void act() {
		System.out.println("Act");
	}
}

// IS-A relationship: Hero is-a Actor
public class Hero extends Actor {
	public void fight() {
		System.out.println("fight");
	}
}

// Comedian is-a Actor
public class Comedian extends Actor {
	public void performComedy() {
		System.out.println("Comedy");
	}
}

Hero hero = new Hero();
hero.act();             // Act  - inherited from Actor
hero.fight();           // fight

Comedian comedian = new Comedian();
comedian.act();         // Act
comedian.performComedy();
```

Key points: Java supports single inheritance for classes (one direct superclass), `private` members are not accessible in the subclass, constructors are not inherited, and every class ultimately extends `Object`. Prefer composition when the relationship isn't truly IS-A.

</details>

<details><summary>

## [Easy] What is Method Overloading?
</summary>

**Overloading** means several methods in the same class (or inherited into it) have the **same name but different parameter lists** (number, types or order of parameters). The compiler picks the method at **compile time** (static binding).

```java
class Calculator {
	int add(int a, int b) { return a + b; }
	int add(int a, int b, int c) { return a + b + c; }
	double add(double a, double b) { return a + b; }
}

class ScientificCalculator extends Calculator {
	long add(long a, long b) { return a + b; }   // overloads the inherited add methods
}
```

Rules:
- Changing only the **return type** is not overloading (compile error).
- Access modifiers and thrown exceptions can differ freely.
- With ambiguous calls the compiler prefers: exact match → widening → boxing → varargs.

</details>

<details><summary>

## [Easy] What is Method Overriding?
</summary>

**Overriding** means a subclass provides its own implementation of a method inherited from its superclass, with the **same name and parameters**. The JVM picks the implementation at **runtime** based on the actual object (dynamic dispatch). This is runtime polymorphism.

```java
public class Animal {
	public String sound() {
		return "Don't know!";
	}
}

class Cat extends Animal {
	@Override                       // compiler checks it really overrides
	public String sound() {
		return "Meow Meow";
	}
}

Animal a = new Cat();
System.out.println(a.sound());     // Meow Meow
```

Rules for overriding:
1. Same name and same parameter list.
2. Return type must be the same or a **subtype** (covariant return).
3. Access can't be **more restrictive** (a `public` method can't become `protected`).
4. Can't throw **new or broader checked exceptions** (unchecked are fine).
5. `final`, `static` and `private` methods can't be overridden (a static method with the same signature *hides* the parent's).
6. Use `super.sound()` to call the parent's version.

</details>

<details><summary>

## [Easy] Can super class reference variable can hold an object of sub class?
</summary>

Yes. Assigning a subclass object to a superclass reference is **upcasting**, and it is always safe and implicit. Through that reference you can call only the methods declared in the superclass, but the **overridden** version in the subclass runs (runtime polymorphism). To use subclass-only methods you must **downcast**, which should be guarded with `instanceof`.

```java
class Vehicle {
	public void drive() { System.out.println("Driving a vehicle."); }
}

class Car extends Vehicle {
	@Override
	public void drive() { System.out.println("Driving a car."); }
	public void accelerate() { System.out.println("Accelerating the car."); }
}

Vehicle vehicle = new Car();          // upcasting
vehicle.drive();                      // Driving a car. (Car's override runs)
// vehicle.accelerate();              // compile error: Vehicle has no accelerate()

if (vehicle instanceof Car car) {     // safe downcast (Java 16 pattern matching)
	car.accelerate();
}
```

</details>

<details><summary>

## [Easy] Is Multiple Inheritance allowed in Java?
</summary>

No, multiple inheritance is not allowed for classes in Java. Java supports single inheritance, where a class can inherit from only one superclass. However, multiple inheritance is supported through interfaces, allowing a class to implement multiple interfaces and inherit their abstract method contracts.

```java
class Dog extends Animal, Pet { //COMPILER ERROR
}

// However, we can create an Inheritance Chain
class Pet extends Animal {
}

class Dog extends Pet {
}
```

</details>

<details><summary>

## [Easy] What is an Interface?
</summary>

An interface is a **contract**: it declares what a class must do, not how. A class `implements` it and provides the method bodies. Interfaces give abstraction and let a class have many types (a class can implement many interfaces).

What an interface can contain:
- **Abstract methods** (implicitly `public abstract`)
- **Constants** (fields are implicitly `public static final`)
- **`default` methods** with a body (Java 8) – let interfaces evolve without breaking implementers
- **`static` methods** (Java 8)
- **`private` methods** (Java 9) – helpers for default methods

An interface can't have instance fields or constructors, and can't be instantiated. It represents an IS-A (or "can-do") relationship, e.g. `Comparable`, `Runnable`, `PaymentGateway`.

**Example:**

```java
public interface PaymentGateway {
    PaymentResult charge(String customerId, BigDecimal amount);   // abstract by default

    default boolean supportsRefund() { return false; }            // Java 8 default method

    static PaymentGateway noop() { return (c, a) -> PaymentResult.ok(); } // static method
}

class RazorpayGateway implements PaymentGateway {
    public PaymentResult charge(String customerId, BigDecimal amount) { /* call API */ return PaymentResult.ok(); }
    @Override public boolean supportsRefund() { return true; }
}
```

</details>

<details><summary>

## [Easy] How do you define an Interface?
</summary>

Use the `interface` keyword. Members are `public` by default; fields are `public static final`.

```java
public interface PaymentGateway {
	int MAX_RETRIES = 3;                                   // constant

	PaymentResult charge(String customerId, long amountPaise);   // abstract

	default boolean supportsRefund() { return false; }      // Java 8

	static PaymentGateway noop() { return (c, a) -> null; } // Java 8

	private void log(String msg) { System.out.println(msg); } // Java 9
}
```

A concrete class that `implements` the interface must implement all abstract methods (or be declared `abstract` itself). Default methods are inherited and may be overridden.

</details>

<details><summary>

## [Easy] How do you implement an interface?
</summary>

To implement an interface in Java:

1. Create a class that will implement the interface.
2. Use the implements keyword followed by the name of the interface(s) you want to implement.
3. Implement all the methods declared in the interface by providing their implementations in the class.
4. Use the @Override annotation to indicate that the methods are overriding the ones in the interface.
5. Instantiate the class and use its implemented methods.


```java
	interface Printable {
		void print();
	}

	class Printer implements Printable {
	    @Override
	    public void print() {
		System.out.println("Printing document...");
	    }
	}

    Printer printer = new Printer();
    printer.print();  // Output: Printing document...
```

</details>

<details><summary>
	
## [Easy] Can you extend an interface?
</summary>

**Yes.** An interface can extend one or more other interfaces using `extends`, and it inherits all their abstract and default methods. (A class can't *extend* an interface; it *implements* it.)

```java
interface Readable { String read(String key); }
interface Writable { void write(String key, String value); }

interface Store extends Readable, Writable {   // multiple inheritance of interfaces
	void delete(String key);
}

class RedisStore implements Store {             // must implement read, write and delete
	public String read(String key) { return null; }
	public void write(String key, String value) { }
	public void delete(String key) { }
}
```

Real examples: `List extends Collection extends Iterable`, `BlockingQueue extends Queue`.

**Example:**

```java
interface Readable { String read(String key); }
interface Writable { void write(String key, String value); }

interface KeyValueStore extends Readable, Writable {   // an interface can extend many
    void delete(String key);
}

class RedisStore implements KeyValueStore {
    public String read(String k) { return null; }
    public void write(String k, String v) { }
    public void delete(String k) { }
}
```

</details>

<details><summary>
	
## [Easy] Can a class implement multiple interfaces?
</summary>

Yes. A class can extend only one class but can **implement any number of interfaces**, separated by commas. It must implement all their abstract methods (or be abstract).

```java
interface ExampleInterface1 { void method1(); }
interface ExampleInterface2 { void method2(); }

class SampleImpl implements ExampleInterface1, ExampleInterface2 {
	public void method1() { System.out.println("Method1"); }
	public void method2() { System.out.println("Method2"); }
}
```

This is how Java gets multiple inheritance of *type* without the problems of multiple inheritance of *state*.

</details>

<details><summary>
	
## [Easy] What is an Abstract Class?
</summary>

An abstract class in Java is a class that cannot be directly instantiated and serves as a blueprint for other classes. It is declared using the abstract keyword and may contain both abstract and non-abstract methods. Abstract methods are declared without an implementation and must be overridden by subclasses. Abstract classes are meant to be extended by other classes using the extends keyword. They can have constructors and provide common behavior for subclasses. The purpose of an abstract class is to define common characteristics and behaviors that subclasses can inherit and implement.

```java
abstract class Bike{  
	abstract void run();  
}  

class Honda4 extends Bike{  
	void run(){
		System.out.println("running safely");
	}  
	public static void main(String args[]){  
		 Bike obj = new Honda4();  
		 obj.run();  
	}  
}  
```

</details>

<details><summary>
	
## [Easy] When do you use an Abstract Class?
</summary>

An abstract class in Java is used when you want to define a common template or blueprint for a group of related classes. It is typically used in the following situations:

To provide a common set of methods or behavior that multiple subclasses can inherit.
When you have certain methods that need to be implemented by subclasses but have no meaningful implementation in the abstract class itself (abstract methods).
To establish a contract or interface that subclasses must adhere to.
When you want to provide default implementations for some methods while allowing subclasses to override them if needed.
When you want to create a base class that cannot be instantiated on its own but can be extended by subclasses.
The main purpose of an abstract class is to provide a structure and guidelines for subclasses, ensuring consistency and allowing for polymorphic behavior. It promotes code reuse, maintainability, and extensibility in object-oriented programming.

**Example:**

```java
abstract class Notification {
    protected final String recipient;                 // shared state
    Notification(String recipient) { this.recipient = recipient; }

    public final void send() {                        // shared flow (template method)
        validate();
        deliver(format());
        log();
    }

    protected abstract String format();               // subclasses fill in the differences
    protected abstract void deliver(String message);

    private void validate() { if (recipient == null) throw new IllegalStateException(); }
    private void log() { System.out.println("sent to " + recipient); }
}

class EmailNotification extends Notification {
    EmailNotification(String to) { super(to); }
    protected String format() { return "<html>Hi</html>"; }
    protected void deliver(String msg) { /* SMTP */ }
}
```

</details>

<details><summary>
	
## [Easy] How do you define an abstract method?
</summary>

A method declared using the abstract keyword within an abstract class and does not have a definition (implementation) is called an abstract method.

When we need just the method declaration in a super class, it can be achieved by declaring the methods as abstracts.

Abstract method is also called subclass responsibility as it doesn't have the implementation in the super class. Therefore a subclass must override it to provide the method definition.

```java
abstract class Animal {
    abstract void makeSound(); // Abstract method declaration
}

class Dog extends Animal {
    @Override
    void makeSound() {
	System.out.println("Bark!"); // Implementation of the abstract method
    }
}
```

</details>

<details><summary>
	
## [Easy] What is a Constructor?
</summary>

A constructor is a special block that **initialises a new object**. It has the same name as the class, no return type (not even `void`), and runs when you use `new`. Memory is allocated by `new`, then the constructor sets up the object's state.

- If you write **no** constructor, the compiler adds a public **default no-arg constructor**.
- Once you write **any** constructor, the compiler no longer adds the default one.
- Types: no-arg and parameterised. Constructors can be overloaded and can call each other with `this(...)`.
- Constructors are not inherited, but every constructor calls a superclass constructor (`super(...)`, implicitly `super()` if you don't write one).

```java
class Animal {
	String name;
	public Animal(String name) {      // parameterised constructor
		this.name = name;
	}
	public static void main(String[] args) {
		// Animal a = new Animal();   // COMPILER ERROR: no no-arg constructor now
		Animal animal = new Animal("Tommy");
	}
}
```

</details>

<details><summary>
	
## [Easy] What is a Default Constructor?
</summary>

Default Constructor is the constructor that is provided by the compiler. It has no arguments. In the
example below, there are no Constructors defined in the Animal class. Compiler provides us with a
default constructor, which helps us create an instance of animal class.

```java
public class Animal {
	String name;
	public static void main(String[] args) {
	// Compiler provides this class with a default no-argument constructor.
	// This allows us to create an instance of Animal class.
	Animal animal = new Animal();
	}
}
```

</details>

<details><summary>
	
## [Easy] Will this code compile? (no-arg and one-arg constructors)
</summary>	

```java
class Animal {
	String name;
	public Animal() {
		this.name = "Default Name";
	}
	public Animal(String name) {
		this.name = name;
	}
	public static void main(String[] args) {
		Animal animal = new Animal();
	}
}
```

**Yes, it compiles.** The class explicitly defines a no-arg constructor, so `new Animal()` works.

It would **not** compile if only `Animal(String name)` existed: once you write any constructor, the compiler stops adding the default no-arg one.

</details>

<details><summary>
	
## [Easy] How do you call a Super Class Constructor from a Constructor?
</summary>	

Use `super(...)` to call a superclass constructor. It must be the **first statement** in the constructor. If you don't write it, the compiler inserts `super()` (the no-arg version), so the superclass must have one.

```java
class Animal {
	protected String name;
	Animal(String name) { this.name = name; }
}

class Dog extends Animal {
	Dog() {
		super("Default Name");   // must come first
	}
	Dog(String name) {
		super(name);
	}
}
```

You can call either `this(...)` or `super(...)` as the first statement, not both.

</details>

<details><summary>
	
## [Easy] What is the use of this()?
</summary>

There can be a lot of usage of Java this keyword. In Java, this is a reference variable that refers to the current object.

Another constructor in the same class can be invoked from a constructor, using this({parameters})
method call.

```java
public Animal() {
	this("Default Name");
}
public Animal(String name) {
	this.name = name;
}
```

</details>

<details><summary>
	
## [Easy] Can a constructor be called directly from a method?
</summary>

No. You can't invoke a constructor like a normal method (`Animal();` is a compile error). Constructors run only:
- when an object is created with `new`, or
- from another constructor's first line via `this(...)` or `super(...)`.

```java
class Animal {
	String name;
	Animal() { }
	Animal(String name) { this(); this.name = name; }   // OK: constructor chaining

	public void reset() {
		// Animal();               // COMPILER ERROR
		// this();                 // COMPILER ERROR: only allowed in a constructor
		Animal fresh = new Animal();   // allowed: creates a NEW object, doesn't re-run on 'this'
	}
}
```

</details>

<details><summary>

## [Easy] Is a super class constructor called even when there is no explicit call from a sub class constructor?
</summary>

Yes. If a subclass constructor doesn't call `this(...)` or `super(...)`, the compiler inserts `super()` as its first line. So constructors run **from the top of the hierarchy down**. If the superclass has no no-arg constructor, the subclass must call another one explicitly, or it won't compile.

```java
class Animal {
	public Animal() { System.out.println("Animal Constructor"); }
}

class Dog extends Animal {
	public Dog() { System.out.println("Dog Constructor"); }      // super() inserted
}

class Labrador extends Dog {
	public Labrador() { System.out.println("Labrador Constructor"); }
}

new Labrador();
// Animal Constructor
// Dog Constructor
// Labrador Constructor
```

</details>

<details><summary>

## [Medium] What is the use of equals method in Java ?
</summary>

`equals()` checks whether two objects are **logically equal** (same content). The default implementation in `Object` is the same as `==` (same reference), so classes such as `String`, `Integer` and `List` override it.

A correct `equals()` must handle `null` and other types. The version below is safe; a naive `(Client) obj` cast throws `ClassCastException` for other types and `NullPointerException` for `null`.

```java
class Client {
	private final int id;
	Client(int id) { this.id = id; }

	@Override
	public boolean equals(Object obj) {
		if (this == obj) return true;
		if (!(obj instanceof Client other)) return false;   // also false for null
		return id == other.id;
	}

	@Override
	public int hashCode() {           // always override together with equals
		return Integer.hashCode(id);
	}
}

Client client1 = new Client(25);
Client client2 = new Client(25);
Client client3 = client1;

System.out.println(client1.equals(client2)); // true  - same id
System.out.println(client1 == client2);      // false - different objects
System.out.println(client1.equals(client3)); // true  - same object
```

</details>

<details><summary>

## [Medium] What are the important things to consider when implementing equals method?
</summary>

The `equals()` contract:

1. **Reflexive:** `a.equals(a)` is true.
2. **Symmetric:** `a.equals(b)` ⇔ `b.equals(a)`.
3. **Transitive:** `a.equals(b)` and `b.equals(c)` ⇒ `a.equals(c)`.
4. **Consistent:** repeated calls give the same result while the objects don't change.
5. **Non-null:** `a.equals(null)` is false (never throws).

Practical rules:
- Check the type with `instanceof` (or `getClass()` if subclasses must never be equal) before casting.
- **Override `hashCode()` too:** equal objects must have equal hash codes, or `HashMap`/`HashSet` break.
- Compare the same fields in both methods; use `Objects.equals` for fields that may be null.
- Prefer immutable fields; if fields used in `equals` change while the object is in a `HashSet`, it can't be found again.
- Recommended (not required): keep `compareTo()` consistent with `equals()`, otherwise `TreeSet`/`TreeMap` behave differently from `HashSet`.
- Records generate a correct `equals`/`hashCode` for you.

**Example:**

```java
public final class Employee {
    private final long id;
    private final String email;

    public Employee(long id, String email) { this.id = id; this.email = email; }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;                         // reflexive, fast path
        if (!(o instanceof Employee other)) return false;   // handles null and other types
        return id == other.id && Objects.equals(email, other.email);
    }

    @Override
    public int hashCode() {                                  // MUST be consistent with equals
        return Objects.hash(id, email);
    }
}

Set<Employee> set = new HashSet<>();
set.add(new Employee(1, "a@x.com"));
System.out.println(set.contains(new Employee(1, "a@x.com"))); // true only because hashCode is overridden too
```

</details>

<details><summary>

## [Medium] What is the hashCode method used for in Java?
</summary>

`hashCode()` returns an `int` used by hash-based collections (`HashMap`, `HashSet`, `ConcurrentHashMap`) to pick a bucket quickly. It is **not unique**: different objects can have the same hash code (a *collision*); the collection then uses `equals()` to tell them apart.

The contract:
- Equal objects (by `equals`) **must** return the same hash code.
- Unequal objects *may* return the same hash code, but fewer collisions mean better performance.
- The value must stay the same while the fields used in it don't change.

```java
@Override
public int hashCode() {
	return Objects.hash(id, email);   // or 31 * Integer.hashCode(id) + Objects.hashCode(email)
}
```

If you override `equals()` but not `hashCode()`, two equal keys can land in different buckets and `map.get(key)` returns `null`.

</details>

<details><summary>
	
## [Medium] Can you explain a few tricky things about interfaces?
</summary>

1. **Fields are always `public static final`.** They must be initialised and can't be `private` or instance fields.

```java
interface ExampleInterface1 {
	int value1 = 10;                       // implicitly public static final
	public static final int value4 = 25;   // same thing, written out
	// private int value5 = 10;            // COMPILER ERROR
}
```

2. **Abstract methods are implicitly `public abstract`.** They can't be `protected` or `final`.

3. **Method bodies are allowed for `default`, `static` (Java 8) and `private` (Java 9) methods.** A `private` method must have a body; `private abstract` is a compile error.

```java
interface ExampleInterface2 {
	void method1();                         // public abstract
	default void method5() { helper(); }    // Java 8+
	private void helper() { System.out.println("helper"); } // Java 9+
}
```

4. **Diamond problem with defaults:** if a class implements two interfaces with the same default method, it must override it and can pick one with `A.super.method()`.

5. **Static interface methods are not inherited** by implementing classes; call them as `InterfaceName.method()`.

6. An interface can **extend multiple interfaces**, but can't extend a class.

</details>

<details><summary>
	
## [Medium] Compare Abstract Class vs Interface?
</summary>

| | Abstract class | Interface |
|---|---|---|
| Methods | Abstract and concrete | Abstract; plus `default`/`static` (Java 8) and `private` (Java 9) |
| Fields | Any kind (instance, static, final or not) | Only `public static final` constants |
| Constructors | Yes (called via `super()`) | No |
| Inheritance | A class extends **one** class | A class implements **many** interfaces; an interface can extend many interfaces |
| Member access | Any modifier (`private`, `protected`, …) | Members are `public` (except `private` helper methods) |
| State | Can hold shared state | No instance state |
| Keyword | `abstract class`, `extends` | `interface`, `implements` |
| Use it for | A base class sharing code and state among closely related classes | A capability/contract that unrelated classes can implement |

```java
public abstract class Shape {           // shared state + partial implementation
	protected final String name;
	protected Shape(String name) { this.name = name; }
	public abstract double area();
	public String describe() { return name + " with area " + area(); }
}

public interface Drawable {            // capability
	void draw();
}
```

Rule of thumb: start with an interface; add an abstract class when implementations share real code or state.

</details>

<details><summary>
	
## [Medium] Will this code compile? (statement before super())
</summary>

```java
public Animal() {
	this.name = "Default Name";
	super();
}
```

**No** (on Java 21 and earlier, which most projects use): `super()` / `this()` must be the first statement of a constructor.

Java 25 introduced *flexible constructor bodies* (JEP 513), which allow some statements before `super()` as long as they don't use the object being built, for example validating arguments. In interviews, the expected answer is still "super() must come first", and you can mention that newer Java relaxes it.

</details>
