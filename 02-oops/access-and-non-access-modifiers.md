<details><summary>
	
## [Easy] What is default class modifier?
</summary>

In Java, the default class modifier, also known as package-private or default access, is a level of access control that is applied when no explicit access modifier is specified for a class, method, or field. It is denoted by the absence of the public, private, or protected keywords.

When a class member (class, method, or field) is declared with the default modifier, it is accessible only within the same package (i.e., the classes that belong to the same package). It is not accessible outside of the package, including subclasses in other packages.

Example

```java
package com.rithus.classmodifiers.defaultaccess.a;

/* No public before class. So this class has default access*/
class DefaultAccessClass {
//Default access is also called package access
}

Another Class in Same Package: Has access to default class
package com.rithus.classmodifiers.defaultaccess.a;

public class AnotherClassInSamePackage {
		//DefaultAccessClass and AnotherClassInSamePackage
		//are in same package.
		//So, DefaultAccessClass is visible.
		//An instance of the class can be created.
		DefaultAccessClass defaultAccess;
}

Class in Different Package: NO access to default class
package com.rithus.classmodifiers.defaultaccess.b;

public class ClassInDifferentPackage {
		//Class DefaultAccessClass and Class ClassInDifferentPackage
		//are in different packages (*.a and *.b)
		//So, DefaultAccessClass is not visible to ClassInDifferentPackage
		//Below line of code will cause compilation error if uncommented
		//DefaultAccessClass defaultAccess; //COMPILE ERROR!!
}
```

</details>

<details><summary>
	
## [Easy] What is private access modifier?
</summary>

In Java, the private access modifier is one of the four access modifiers used to control the visibility and accessibility of class members, including variables, methods, and nested classes, within a class.

When a class member is declared as private, it is accessible only within the same class where it is defined. It is not visible or accessible from any other class, including subclasses and other classes in the same package.

```java
public class MyClass {
    private int privateField;

    private void privateMethod() {
	System.out.println("This is a private method.");
    }

    public void publicMethod() {
	privateField = 10;   // Accessible within the same class
	privateMethod();     // Accessible within the same class
    }
}
```

</details>

<details><summary>
	
## [Easy] What is default or package access modifier?
</summary>

In Java, the default or package access modifier is a level of access control that is applied when no explicit access modifier is specified for a class, method, or field. It is denoted by the absence of the public, private, or protected keywords.

When a class member (class, method, or field) is declared with the default modifier, it is accessible within the same package (i.e., the classes that belong to the same package). It is not accessible outside of the package, including subclasses in other packages.

```java
package com.example;

class MyClass {
    void myMethod() {
	System.out.println("This method has default access.");
    }
}

public class Main {
    public static void main(String[] args) {
	MyClass myObject = new MyClass();
	myObject.myMethod();  // Accessible within the same package
    }
}
```

</details>

<details><summary>
	
## [Easy] What is public access modifier?
</summary>

In Java, the public access modifier is one of the four access modifiers used to control the visibility and accessibility of class members, including variables, methods, and nested classes.

When a class member is declared as public, it is accessible from any other class, regardless of the package or subclass relationship. It provides the highest level of visibility and allows unrestricted access to the member.

The public access modifier is used when you want a class member to be accessible and visible from any part of the program. It is typically used for creating public APIs, exposing functionality to other classes, and facilitating easy integration with other modules or libraries.

```java
package com.example;

public class MyClass {
    public int publicField;

    public void publicMethod() {
	System.out.println("This is a public method.");
    }
}

public class Main {
    public static void main(String[] args) {
	MyClass myObject = new MyClass();
	myObject.publicField = 10;      // Accessible from any class
	myObject.publicMethod();        // Accessible from any class
    }
}
```

</details>

<details><summary>
	
## [Easy] What access types of variables can be accessed from a Class in Same Package?
</summary>

A class in the **same package** can access **public, protected and default (package-private)** members of another class. Only **private** members are hidden. Being a subclass doesn't matter inside the same package.

```java
package com.rithus.membermodifiers.access;

public class TestClassInSamePackage {
	public static void main(String[] args) {
		ExampleClass example = new ExampleClass();

		example.publicVariable = 5;      // OK
		example.publicMethod();

		example.protectedVariable = 5;   // OK: same package
		example.protectedMethod();

		example.defaultVariable = 5;     // OK: same package
		example.defaultMethod();

		// example.privateVariable = 5;  // COMPILE ERROR
		// example.privateMethod();      // COMPILE ERROR
	}
}
```

</details>

<details><summary>
	
## [Easy] What access types of variables can be accessed from a Class in Different Package?
</summary>

In Java, when a class is in a different package than another class, it has access to the following types of variables in the other class:

1. Public variables: Public variables can be accessed directly from any class, regardless of the package. Therefore, a class in a different package can access public variables in another class.	
	
Look at the code below to understand what can be accessed and what cannot be.

```java
package com.rithus.membermodifiers.access.different;

import com.rithus.membermodifiers.access.ExampleClass;

public class TestClassInDifferentPackage {
		public static void main(String[] args) {
				ExampleClass example = new ExampleClass();

				example.publicVariable = 5;
				example.publicMethod();

				//privateVariable,privateMethod are not visible
				//Below Lines, uncommented, would give compiler error
				//example.privateVariable=5; //COMPILE ERROR
				//example.privateMethod();//COMPILE ERROR

				//protectedVariable,protectedMethod are not visible
				//Below Lines, uncommented, would give compiler error
				//example.protectedVariable = 5; //COMPILE ERROR
				//example.protectedMethod();//COMPILE ERROR

				//defaultVariable,defaultMethod are not visible
				//Below Lines, uncommented, would give compiler error
				//example.defaultVariable = 5;//COMPILE ERROR
				//example.defaultMethod();//COMPILE ERROR
		}
}	
```
	
</details>

<details><summary>
	
## [Easy] What is the use of a final modifier on a class ?
</summary>

A `final` class **cannot be extended**. Use it when:
- The class's behaviour must not be changed by subclasses (security, correctness). `String`, `Integer` and the other wrapper classes are final, so nobody can create a "fake" mutable `String`.
- You are building an **immutable class**: marking it `final` stops a subclass from adding mutable state or overriding methods.
- The class wasn't designed for inheritance ("design for inheritance or prohibit it").

```java
public final class Money {
	private final long amountPaise;
	private final String currency;
	public Money(long amountPaise, String currency) { this.amountPaise = amountPaise; this.currency = currency; }
}

// class DiscountedMoney extends Money { }   // COMPILER ERROR: cannot inherit from final Money
```

Performance is *not* a real reason today: the JIT already inlines non-overridden methods. For controlled extension (only some subclasses allowed), use **sealed classes** (Java 17).

</details>

<details><summary>
	
## [Easy] What is the use of a final modifier on a method ?
</summary>

A `final` method **cannot be overridden** by subclasses (it can still be inherited and overloaded). Use it to protect behaviour that subclasses must not change, for example the steps of a template method or a security check.

```java
public class PaymentProcessor {
	public final void process(Payment p) {   // fixed algorithm
		validate(p);
		charge(p);
		audit(p);
	}
	protected void charge(Payment p) { }     // subclasses customise only this step
	private void validate(Payment p) { }
	private void audit(Payment p) { }
}

class UpiProcessor extends PaymentProcessor {
	@Override protected void charge(Payment p) { /* UPI call */ }
	// public void process(Payment p) { }    // COMPILER ERROR: process is final
}
```

`private` and `static` methods are effectively non-overridable already. Modern JVMs don't need `final` for speed; use it for design intent.

</details>

<details><summary>
	
## [Easy] What is a Final Variable ?
</summary>

A `final` variable can be **assigned only once**.

- **Final local variable / parameter:** can't be reassigned after initialisation.
- **Final instance field:** must be assigned exactly once, either at declaration or in every constructor (a "blank final").
- **`static final`:** a constant shared by the class (`static final int MAX_RETRIES = 3;`).

```java
public class Order {
	private final long id;                       // blank final: set in constructor
	private final List<String> items = new ArrayList<>();

	public Order(long id) { this.id = id; }

	void update() {
		// id = 5;                  // COMPILER ERROR
		items.add("pen");           // allowed! the reference is final, the list is not
	}
}
```

Important: `final` makes the **reference** constant, not the object. For a truly immutable field, also use an immutable object (`List.copyOf(...)`, `String`, records). `final` fields also get a memory-model guarantee: other threads see their constructed values once the object is safely published.

</details>

<details><summary>
	
## [Easy] What is a Final Argument ?
</summary>

In Java, a final argument refers to a method parameter that is declared with the final modifier. When a method parameter is marked as final, it means that its value cannot be changed within the method body. Ensure its immutability and read-only access within the method. It communicates the intent that the parameter should not be modified and provides an extra level of safety in method implementation.

```java
public void myMethod(final int value) {
    // Cannot modify the value of the 'value' parameter
    // value = 10;  // This would cause a compilation error

    // Read-only access to the 'value' parameter
    int result = value * 2;
    System.out.println(result);
}
```

</details>

<details><summary>
	
## [Easy] What is a Static Variable ?
</summary>

In Java, a static variable, also known as a class variable, is a variable that belongs to the class itself rather than to any particular instance of the class. This means that all instances of the class share the same copy of the static variable. Here are some key points about static variables:

1. Shared by all instances: Static variables are shared by all instances of a class. Any modification to the static variable is reflected across all instances of the class.

2. Memory allocation: Static variables are allocated memory once, when the class is loaded into memory. They exist throughout the entire execution of the program, regardless of the number of instances created.

3. Accessed using the class name: Since static variables belong to the class itself, they are accessed using the class name followed by the variable name, rather than through an instance of the class.

4. Initialization: Static variables can be initialized at the time of declaration or within a static block, which is a block of code that runs when the class is loaded.

5. Usage: Static variables are commonly used to store values that are shared among all instances of a class, such as constants, configuration settings, or counters.

Static Variable/Method – Example
count variable in Cricketer class is static. The method to get the count value 
getCount() is also a static method.

```java
public class Cricketer {
	private static int count;

	public Cricketer() {
			count++;
	}

	static int getCount() {
			return count;
	}

	public static void main(String[] args) {
			Cricketer cricketer1 = new Cricketer();
			Cricketer cricketer2 = new Cricketer();
			Cricketer cricketer3 = new Cricketer();
			Cricketer cricketer4 = new Cricketer();
			System.out.println(Cricketer.getCount());//4
	}
}
```

4 instances of the Cricketer class are created. Variable count is incremented 
with every instance createdin the constructor.
</details>

<details><summary>
	
## [Medium] What is protected access modifier?
</summary>

A `protected` member is accessible:
1. from **any class in the same package** (subclass or not), and
2. from **subclasses in other packages**, but only through inheritance (via `this`/the subclass type), not through an arbitrary superclass reference.

It is **not** accessible to unrelated classes in other packages.

```java
package com.example.base;
public class Superclass {
	protected int protectedField;
	protected void protectedMethod() { System.out.println("protected"); }
}

package com.example.other;
import com.example.base.Superclass;

public class Subclass extends Superclass {
	void use(Superclass someOther) {
		protectedField = 10;          // OK: inherited member
		protectedMethod();            // OK
		// someOther.protectedMethod(); // COMPILER ERROR: not via another Superclass reference
	}
}

class Unrelated {                       // different package, not a subclass
	// new Superclass().protectedMethod(); // COMPILER ERROR
}
```

| Modifier | Same class | Same package | Subclass (other package) | Anywhere |
|---|---|---|---|---|
| `private` | ✅ | ❌ | ❌ | ❌ |
| default (none) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ (through inheritance) | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

</details>

<details><summary>
	
## [Medium] What access types of variables can be accessed from a Sub Class in Same Package?
</summary>

In Java, when a subclass is in the same package as its superclass, it has access to the following types of variables in the superclass:

1. Public variables: Public variables can be accessed directly from any class, including subclasses. Therefore, a subclass in the same package can access public variables in its superclass.

2. Protected variables: Protected variables are accessible within the same package as well as by subclasses, even if they are in a different package. Therefore, a subclass in the same package can access protected variables in its superclass.

3. Default (package-private) variables: Default variables are accessible within the same package but not outside of it. Therefore, a subclass in the same package can access the default variables in its superclass.
	
Look at the code below to understand what can be accessed and what cannot be.

```java
package com.rithus.membermodifiers.access;

public class SubClassInSamePackage extends ExampleClass {

	void subClassMethod(){
			publicVariable = 5;
			publicMethod();

			//privateVariable is not visible to SubClass
			//Below Line, uncommented, would give compiler error
			//privateVariable=5; //COMPILE ERROR
			//privateMethod();

			protectedVariable = 5;
			protectedMethod();

			defaultVariable = 5;
			defaultMethod();
	}
}	
```

</details>

<details><summary>
	
## [Medium] What access types of variables can be accessed from a Sub Class in Different Package?
</summary>

In Java, when a subclass is in a different package than its superclass, it has access to the following types of variables in the superclass:

1. Public variables: Public variables can be accessed directly from any class, including subclasses. Therefore, a subclass in a different package can access public variables in its superclass.

2. Protected variables: Protected variables are accessible within the same package as well as by subclasses, even if they are in a different package. Therefore, a subclass in a different package can access protected variables in its superclass if it is a subclass of the superclass.	
	
Look at the code below to understand what can be accessed and what cannot be.

```java
package com.rithus.membermodifiers.access.different;

import com.rithus.membermodifiers.access.ExampleClass;

public class SubClassInDifferentPackage extends ExampleClass {

	void subClassMethod(){
		publicVariable = 5;
		publicMethod();

		//privateVariable is not visible to SubClass
		//Below Line, uncommented, would give compiler error
		//privateVariable=5; //COMPILE ERROR
		//privateMethod();

		protectedVariable = 5;
		protectedMethod();

		//privateVariable is not visible to SubClass
		//Below Line, uncommented, would give compiler error
		//defaultVariable = 5; //COMPILE ERROR
		//defaultMethod();
	}
}	
```

</details>

<details><summary>
	
## [Hard] What happens when a variable is marked as volatile?
</summary>

`volatile` tells the JVM that a field is shared between threads:

1. **Visibility:** a write by one thread is visible to all other threads immediately; threads don't keep a stale cached copy.
2. **Ordering:** reads/writes of a volatile field aren't reordered with the memory operations around them (a *happens-before* relationship), so everything a thread wrote before writing the volatile is visible to a thread that reads it.

What it does **not** do: make compound actions atomic. `count++` (read, add, write) on a volatile field is still a race; use `AtomicInteger`, `LongAdder` or a lock.

Good uses: stop/status flags, publishing a reference to an immutable object, the instance field in double-checked-locking singletons.

**Example:**

```java
class Task implements Runnable {
    private volatile boolean running = true;  // without volatile, run() may loop forever

    public void run() {
        while (running) { /* work */ }
        System.out.println("stopped");
    }

    public void stop() { running = false; }   // visible to the worker thread immediately
}

// volatile does NOT make this safe: count++ is read + add + write
private volatile int count;
void increment() { count++; }   // use AtomicInteger instead
```

</details>