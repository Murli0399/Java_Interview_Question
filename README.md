<details>
	<summary># Why is Java so Popular?</summary>
  
## Why is Java so Popular?
Java is one of the most popular languages because Java has several contributions to its widespread adoption and continued relevance in the software development industry. So Java has some key factors which make it  a popular programming language.

- **Simple:-** Java is easy to learn and its syntax is quite simple, clean, and easy to understand. Apart from this automatic memory management also play a role in the same
- **Object-Oriented**:- Java is ***object-oriented***, it supports all the OOPS characteristics. This makes Java applications easy to develop and maintain, compared to structured programming languages.
- **Platform Independent:-** Java source code is compiled and converted into bytecode. this bytecode can run on multiple platforms i.e. Write Once and Run Anywhere(WORA), we can compile the java code in one Operating System and execute it on another Operating System. The WORA makes java an Architecture Neutral language. Java also standardized all data types that also contributed to making java a platform-independent language.
</details>
  
## What is Platform Independence?
Platform independence, also known as "write once, run anywhere," refers to the ability of a programming language or framework to run on different platforms without requiring extensive modifications. In the context of Java, platform independence is one of the its key features.

Java is one of the most popular platform independent languages. Once we compile a java program and build a jar, we can run the jar (compiledjava program) in any Operating System - where a JVM is installed.Java achieves Platform Independence in a beautiful way. On compiling a java file the output is a class file- which contains an internal java representation called bytecode. 

JVM converts bytecode to executable instructions. The executable instructions are different in different operating systems. So, there aredifferent JVM's for different operating systems. A JVM for windows is different from a JVM for mac.However, both the JVM's understand the bytecode and convert it to the executable code for therespective operating system.

## What is ByteCode?
Bytecode is a low-level representation of code that is executed by a virtual machine (VM) rather than directly by the hardware. It serves as an intermediate step between source code and machine code, enabling platform independence and facilitating efficient execution.

If i talk about Java, when you write a Java program, it is first compiled into bytecode. And the Java compiler (javac) translates the human-readable Java source code into a compact and platform-neutral binary format which is called by bytecode. This bytecode is stored in .class files.

Bytecode is designed to be easily interpreted and executed by the Java Virtual Machine (JVM), which is specific to each platform or operating system. Instead of directly executing machine-specific instructions, the JVM reads the bytecode instructions one by one and dynamically translates them into machine code that can be executed by the underlying hardware.

## Compare JDK vs JVM VS JRE.
JDK (Java Development Kit), JVM (Java Virtual Machine), and JRE (Java Runtime Environment) are key components of the Java platform. Each serves a specific purpose in the Java development and execution process. Here's a comparison of these three components:

### JDK (Java Development Kit):
The JDK is a software development kit that includes the necessary tools and libraries for Java development.
It contains the Java compiler (javac) that translates Java source code into bytecode, which can be executed by the JVM.
The JDK also includes other tools, such as the Java debugger (jdb), documentation generator (javadoc), and various utilities for packaging and deploying Java applications.
Developers use the JDK to write, compile, and package Java applications. It provides all the necessary components to develop and build Java software.

### JVM (Java Virtual Machine):
The JVM is an integral part of the Java platform. It is an abstract machine that executes Java bytecode.
The JVM interprets the bytecode instructions and translates them into machine code that can be understood and executed by the underlying hardware.
It provides several services essential for Java execution, including memory management, garbage collection, security, and exception handling.
The JVM is platform-dependent, meaning that there are different implementations of the JVM for different operating systems and hardware architectures.
It ensures platform independence by providing a standardized runtime environment, allowing Java programs to run consistently across different platforms without requiring recompilation.

### JRE (Java Runtime Environment):
The JRE is a subset of the JDK. It includes the necessary components to run Java applications but does not contain the development tools like the compiler and debugger.
The JRE consists of the JVM, Java class libraries, and other runtime dependencies required for executing Java applications.
It provides the runtime environment for running Java applications on end-user machines or servers.
Users who only need to run Java applications, rather than developing them, can install the JRE. It allows them to execute Java programs without the need for the full JDK.

## What is the role of class loader in java ?
Java ClassLoader is an abstract class. It belongs to a java.lang package. It loads classes from different resources. Java ClassLoader is used to load the classes at run time. In other words, JVM performs the linking process at runtime. Classes are loaded into the JVM according to need. If a loaded class depends on another class, that class is loaded as well. When we request to load a class, it delegates the class to its parent. In this way, uniqueness is maintained in the runtime environment. It is essential to execute a Java program.

## What are wrapper classes?
Wrapper classes in Java are a set of classes that encapsulate primitive data types (such as int, float, char, etc.) and provide object-oriented representations for them. They allow primitive types to be used as objects in Java programs by wrapping them within instances of the corresponding wrapper classes.
Here are the wrapper classes for each primitive type:

Boolean: Represents the boolean type.
Byte: Represents the byte type.
Short: Represents the short type.
Integer: Represents the int type.
Long: Represents the long type.
Float: Represents the float type.
Double: Represents the double type.
Character: Represents the char type.

## Why do we need Wrapper Classes in Java?
The Java programming language treats primitive types and objects differently. Primitive types are not considered objects and do not have the capabilities of objects, such as methods and additional functionalities. However, there are situations where we may need to treat primitive types as objects, such as when working with collections, generics, or when using methods that require objects as arguments.
Wrapper classes bridge this gap by providing a way to wrap primitive types and use them as objects. 

## What are the different ways of creating Wrapper Class Instances?
In Java, there are several ways to create instances of wrapper classes, which allow you to wrap primitive values within objects. Here are the different ways of creating wrapper class instances:

### Using Constructors
Each wrapper class provides constructors that accept the corresponding primitive type or a string representation of the value.
Integer myInteger = new Integer(10);       // Using int value
Double myDouble = new Double(3.14);        // Using double value
Character myChar = new Character('A');     // Using char value
Boolean myBoolean = new Boolean(true);     // Using boolean value

Some wrapper classes also provide constructors that take a string as an argument to parse and initialize the value:
Integer myInteger = new Integer("100");     // Using string value
Double myDouble = new Double("3.14");       // Using string value

### Using Static valueOf() Methods
Each wrapper class provides a static valueOf() method that creates an instance of the wrapper class from the specified value. These methods often offer better performance compared to using constructors. 
Integer myInteger = Integer.valueOf(10);         // Using int value
Double myDouble = Double.valueOf(3.14);          // Using double value
Character myChar = Character.valueOf('A');       // Using char value
Boolean myBoolean = Boolean.valueOf(true);       // Using boolean value

The valueOf() methods also accept a string representation of the value:
Integer myInteger = Integer.valueOf("100");      // Using string value
Double myDouble = Double.valueOf("3.14");        // Using string value

### Using Autoboxing
Java provides autoboxing, which automatically converts primitive values to their corresponding wrapper class instances and vice versa. This simplifies the process of creating wrapper class instances.
Integer myInteger = 10;        // Autoboxing int to Integer
Double myDouble = 3.14;        // Autoboxing double to Double
Character myChar = 'A';        // Autoboxing char to Character
Boolean myBoolean = true;      // Autoboxing boolean to Boolean

Autoboxing allows you to assign primitive values directly to wrapper class variables, and the conversion is handled implicitly by the compiler.

### Using Static Constants
Some wrapper classes provide static constants for commonly used values, such as Integer.MAX_VALUE, Double.NaN, or Character.MAX_VALUE. These constants can be directly used to create wrapper class instances.
Integer myInteger = Integer.MAX_VALUE;
Double myDouble = Double.NaN;
Character myChar = Character.MAX_VALUE;

This method is primarily useful when you need to use specific predefined values.

It's important to note that wrapper classes are immutable, meaning their values cannot be changed once created. If you need to perform arithmetic or other operations on the wrapped values, you'll need to create new wrapper instances with the updated values.

In general, using constructors or the valueOf() method are the most common ways to create wrapper class instances, while autoboxing provides a convenient shorthand syntax. The choice depends on your specific requirements and coding style.

## What is Auto Boxing?
### Autoboxing
The automatic conversion of primitive types to the object of their corresponding wrapper classes is known as autoboxing. For example – conversion of int to Integer, long to Long, double to Double, etc. 
int num = 10;
Integer myInteger = num;  // Autoboxing int to Integer

### Unboxing
It is just the reverse process of autoboxing. Automatically converting an object of a wrapper class to its corresponding primitive type is known as unboxing. For example – conversion of Integer to int, Long to long, Double to double, etc. 
Integer myInteger = 20;
int num = myInteger;  // Unboxing Integer to int

## What are the advantages of Auto Boxing?
Auto Boxing helps in saving memory by reusing already created Wrapper objects. 
Auto Boxing uses the static valueOf methods. However wrapper classes created 
using new are not reused.

Two wrapper objects created using new are not same object.
	
	Integer nineA = new Integer(9);
	Integer nineB = new Integer(9);
	System.out.println(nineA == nineB);//false
	System.out.println(nineA.equals(nineB));//true

Two wrapper objects created using boxing are same object.
	
	Integer nineC = 9;
	Integer nineD = 9;
	System.out.println(nineC == nineD);//true
	System.out.println(nineC.equals(nineD));//true

## What is Casting?
Casting is a method or process that converts a data type into another data type in both ways manually and automatically. The automatic conversion is done by the compiler and manual conversion performed by the programmer.
Convert a value from one data type to another data type is known as type casting.

Types of Type Casting
There are two types of type casting:

Widening Type Casting (Implicit Casting)
Narrowing Type Casting (Explicit Casting)

## What is Implicit Casting?
Converting a lower data type into a higher one is called widening type casting. It is also known as implicit conversion or down casting. It is done by compiler or automatically. It is safe because there is no chance to lose data.
Both data types must be compatible with each other.
The target type must be larger than the source type.

byte -> short -> char -> int -> long -> float -> double  
	
	int value = 100;
	long number = value; //Implicit Casting
	float f = 100; //Implicit Casting

## What is Explicit Casting?
Converting a higher data type into a lower one is called narrowing type casting. It is also known as explicit conversion or up casting. It is done manually by the programmer. If we do not perform casting then the compiler reports a compile-time error.

double -> float -> long -> int -> char -> short -> byte  
Storing larger values into smaller variable types;
	
	long number1 = 25678;
	int number2 = (int)number1;//Explicit Casting
	//int x = 35.35;//COMPILER ERROR
	int x = (int)35.35;//Explicit Casting

Explicit casting would cause truncation of value if the value stored is greater 
than the size of the variable.
	
	int bigValue = 280;
	byte small = (byte) bigValue;
	System.out.println(small);//output 24. Only 8 bits remain.

## Are all String’s immutable?
A String is an unavoidable type of variable while writing any application program. String references are used to store various attributes like username, password, etc. In Java, String objects are immutable. Immutable simply means unmodifiable or unchangeable.

Once String object is created its data or state can't be changed but a new String object is created.
As Java uses the concept of String literal. Suppose there are 5 reference variables, all refer to one object "Sachin". If one reference variable changes the value of the object, it will be affected by all the reference variables. That is why String objects are immutable in Java.

## Where are string values stored in memory?
String is a class and strings in java treated as an object, hence the object of String class will be stored in Heap area. But depends on how we are create them. So we have two method for creating String value.

Approach 1
In the below example we are directly referencing a String literal.
	
	String str1 = "value";
This value will be stored in a "String constant pool" – which is inside the 
Heap memory. If compiler finds a String literal, JVM checks the if String constant pool if exists in the pool. it is reused.

Approach 2
However, if new operator is used to create string object, the new object is created on the heap. There will not be any case to reuse of values.

	//String Object - created on the heap
	String str2 = new String("value");

## Why should you be careful about String Concatenation(+) operator in Loops?
Using the string concatenation operator (+) inside loops can be inefficient and lead to performance issues. It is important to be careful when concatenating strings within loops because of the following reasons:

### String immutability
In Java, String objects are immutable, meaning their values cannot be changed once they are created. When you use the + operator to concatenate strings, a new String object is created for each concatenation operation. This can lead to unnecessary memory allocation and object creation inside the loop.

### String memory overhead
Each time a new String object is created through concatenation, the previous String objects are discarded, resulting in additional memory usage. In a loop with a large number of iterations, this can cause unnecessary memory overhead and impact performance.

### Time complexity
The time complexity of string concatenation using the + operator inside a loop is quadratic, meaning it grows exponentially with the number of iterations. For each concatenation operation, the entire concatenated string is copied into a new object, resulting in increasing time complexity. This can lead to significant performance degradation for large loops.

	String s3 = "Value1";
	String s2 = "Value2";

	for (int i = 0; i < 100000; ++i) {
		s3 = s3 + s2;
	}
How many objects are created in memory? More than 100000 Strings are created. 
This will have a huge performance impact.

## How do you solve above problem?
To solve the performance problem associated with string concatenation using the + operator inside loops, we can use the StringBuilder class. StringBuilder provides a mutable buffer for efficiently constructing strings by appending individual values. 
	
	StringBuffer s3 = new StringBuffer("Value1");
	String s2 = "Value2";

	for (int i = 0; i < 100000; ++i) {
		s3.append(s2);
	}

## What are differences between String and StringBuffer?
String objects are immutable, while StringBuffer objects are mutable.
String concatenation involves creating new String objects, while StringBuffer allows in-place modifications.
String is not thread-safe, while StringBuffer is synchronized and thread-safe.
StringBuffer is more memory-efficient for frequent modifications, while String objects may result in additional memory usage.
Use String when immutability is desired, and StringBuffer when frequent modifications are needed.

## What are differences between StringBuilder and StringBuffer?
StringBuilder is not thread-safe, while StringBuffer is thread-safe.
StringBuilder provides better performance due to the absence of synchronization.
Use StringBuilder in single-threaded scenarios or when manual synchronization is applied.
Use StringBuffer in multi-threaded scenarios where thread safety is required.

## Can you give examples of different utility methods in String class?
Certainly! The String class in Java provides a wide range of utility methods to perform various operations on strings. Here are some examples of commonly used utility methods in the String class:

	1. Length:
	int length(): Returns the length of the string.

	2.Concatenation:
	String concat(String str): Concatenates the specified string to the end of the current string.
	static String join(CharSequence delimiter, CharSequence... elements): Joins multiple strings using the specified delimiter.

	3. Substring:
	String substring(int beginIndex); //Returns a new string that is a substring of the current string, starting from the specified index.
	String substring(int beginIndex, int endIndex); //Returns a new string that is a substring of the current string, starting from the specified begin index and ending at the specified end index (exclusive).

	4. Case conversion:
	String toLowerCase(): //Converts the string to lowercase.
	String toUpperCase(): //Converts the string to uppercase.

	5. Character extraction:
	char charAt(int index): //Returns the character at the specified index in the string.
	int codePointAt(int index): //Returns the Unicode code point value of the character at the specified index.

	6. Comparison:
	boolean equals(Object obj): //Checks if the current string is equal to the specified object.
	boolean equalsIgnoreCase(String anotherString): //Checks if the current string is equal to the specified string, ignoring case.

## What is a Class?
In object-oriented programming, a class is a blueprint or template that defines the structure and behavior of objects. It serves as a blueprint for creating instances, also known as objects, which are individual occurrences based on the class.

A class encapsulates data, known as attributes or fields, and defines the operations, known as methods or functions, that can be performed on that data. It provides a way to organize related data and behavior into a cohesive unit.

## What is an Object?
In object-oriented programming, an object is an instance of a class. It represents a specific occurrence or entity based on the structure and behavior defined by its class. An object combines data, known as attributes or properties, with the methods or functions that operate on that data.

## What is state of an Object?
The state of an object refers to the set of values stored in its attributes or instance variables at a given point in time. It represents the current snapshot of the object's data. The state of an object can change over time as its attributes are modified.

## What is behavior of an Object?
The behavior of an object refers to the actions or operations that an object can perform. It represents the functionality or capabilities associated with an object based on its class definition. The behavior is defined by the methods or functions defined within the class.

## What is the super class of every class in Java?
In Java, the superclass of every class is the Object class. The Object class is at the top of the class hierarchy and serves as the root class for all other classes in Java.

The Object class is defined in the java.lang package and provides a set of common methods and behaviors that are inherited by all classes. These methods include toString(), equals(), hashCode(), getClass(), and more.

Since every class in Java implicitly or explicitly extends the Object class, all objects in Java inherit the methods and behavior defined in Object. This allows for certain fundamental operations and provides a common interface for all objects in Java.

It's important to note that even if a class doesn't explicitly extend any other class, it still inherits from Object by default. This inheritance relationship establishes a foundation for the object-oriented features and functionality in Java.
	
	Let’s look at a simple example:

	String str = "Testing";
	System.out.println(str.toString());
	System.out.println(str.hashCode());
	System.out.println(str.clone());

	if(str instanceof Object){
		System.out.println("I extend Object");//Will be printed
	}

In the above example, toString, hashCode and clone methods for String class are 
inherited from Object class and overridden.

## Explain about toString method ?
The toString() method is a method defined in the Object class in Java. It is inherited by all classes in Java, as every class is a subclass of Object. The toString() method is used to obtain a string representation of an object.

By default, the toString() method in the Object class returns a string that consists of the class name, followed by an "at" symbol (@), and the hash code of the object in hexadecimal format. For example, ClassName@6e1408c6.

However, it is common practice to override the toString() method in custom classes to provide a more meaningful and human-readable representation of the object's state. By overriding the toString() method, you can define the format and content of the string representation according to your requirements.

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

	Run this piece of code:

	Animal animal = new Animal("Tommy","Dog");
	System.out.println(animal);//Animal [name=Tommy, type=Dog]

## What is the super class of every class in Java?
In Java, the superclass of every class is the Object class. The Object class is at the top of the class hierarchy and serves as the root class for all other classes in Java.

The Object class is defined in the java.lang package and provides a set of common methods 

## What is the use of equals method in Java ?
The equals() method in Java is used to compare the equality of two objects. It is defined in the Object class and can be overridden by subclasses to provide custom comparison logic.

The primary purpose of the equals() method is to determine if two objects have the same logical equivalence, rather than just checking if they are the same object in terms of memory reference (which is done by using the == operator). By default, the equals() method in the Object class performs the same reference comparison as the == operator, but it can be overridden to provide a more meaningful comparison based on the content or attributes of the objects.

	class Client {
		private int id;
		public Client(int id) {
				this.id = id;
		}
		@Override
		public boolean equals(Object obj) {
			Client other = (Client) obj;
			if (id != other.id)
				return false;
			return true;
		}
	}

Consider running the code below:
	
	Client client1 = new Client(25);
	Client client2 = new Client(25);
	Client client3 = client1;

	//both id's are 25
	System.out.println(client1.equals(client2));//true

	//both id's are 25
	System.out.println(client1.equals(client3));//true

Above code compares the values (id's) of the objects.

## What are the important things to consider when implementing equals method?
When implementing the equals() method in Java, there are several important considerations to keep in mind to ensure correctness and consistency. Here are the key points to consider:

1. Reflexivity: Object should be equal to itself.
2. Symmetry: If a.equals(b) is true, then b.equals(a) should also be true.
3. Transitivity: If a.equals(b) and b.equals(c) are true, then a.equals(c) should also be true.
4. Consistency: Multiple invocations of equals() should return the same result if object state hasn't changed.
5. Handling null: equals() should handle null references properly and return false.
6. Type checking: Properly check and handle different object types to avoid ClassCastException.
7. Override hashCode(): If equals() is overridden, hashCode() should be overridden to maintain consistency.
8. Comparable attributes: If implementing Comparable, attributes used in equals() should match those used in compareTo().
Considering these points ensures correct and reliable behavior when comparing objects for equality.

## What is the hashCode method used for in Java?
The hashCode() method in Java is used to generate a unique integer value, known as the hash code, for an object. It is defined in the Object class and can be overridden by subclasses to provide a custom hash code implementation.

The primary purpose of the hashCode() method is to support efficient storage and retrieval of objects in hash-based data structures such as HashMap, HashSet, and Hashtable. These data structures use hash codes to determine the storage location (bucket) for objects, which allows for fast retrieval and efficient search operations.

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + id;
		return result;
	}

## Explain inheritance with Examples?
Inheritance in Java is a mechanism in which one object acquires all the properties and behaviors of a parent object. It is an important part of OOPs (Object Oriented programming system).

The idea behind inheritance in Java is that you can create new classes that are built upon existing classes. When you inherit from an existing class, you can reuse methods and fields of the parent class. Moreover, you can add new methods and fields in your current class also.

Inheritance represents the IS-A relationship which is also known as a parent-child relationship.

	public class Actor {
		public void act(){
			System.out.println("Act");
		};
	}

We can extend this class by using the keyword extends. Hero class extends Actor.

	//IS-A relationship. Hero is-a Actor
	public class Hero extends Actor {
		public void fight(){
			System.out.println("fight");
		};
	}

We can now create an instance of Hero class. Since Hero extends Animal, the 
methods defined in Animal are also available through an instance of Hero class. 
In the example below, we invoke the act method on hero object.

	Hero hero = new Hero();
	//act method inherited from Actor
	hero.act();//Act
	hero.fight();//fight

Let’s look at another class extending Actor class - Comedian.

	//IS-A relationship. Comedian is-a Actor
	public class Comedian extends Actor {
		public void performComedy(){
			System.out.println("Comedy");
		};
	}

We can now reuse Actor methods from an instance of Comedian class as well.

	Comedian comedian = new Comedian();
	//act method inherited from Actor
	comedian.act();//Act
	comedian.performComedy();//Comedy

## What is Method Overloading?
If a class has multiple methods having same name but different in parameters, it is known as Method Overloading.

If we have to perform only one operation, having same name of the methods increases the readability of the program.

Suppose you have to perform addition of the given numbers but there can be any number of arguments, if you write the method such as a(int,int) for two parameters, and b(int,int,int) for three parameters then it may be difficult for you as well as other programmers to understand the behavior of the method because its name differs.

So, we perform method overloading to figure out the program quickly.

Example 1
doIt method is overloaded in the below example:

	class Foo{
		public void doIt(int number){

		}
		public void doIt(String string){

		}
	}

Example 2
Overloading can also be done from a sub class.

	class Bar extends Foo{
		public void doIt(float number){

		}
	}

## What is Method Overriding?
If subclass (child class) has the same method as declared in the parent class, it is known as method overriding in Java.

In other words, If a subclass provides the specific implementation of the method that has been declared by one of its parent class, it is known as method overriding.

Usage of Java Method Overriding
1. Method overriding is used to provide the specific implementation of a method which is already provided by its superclass.
2. Method overriding is used for runtime polymorphism
Rules for Java Method Overriding
1. The method must have the same name as in the parent class
2. The method must have the same parameter as in the parent class.
3. There must be an IS-A relationship (inheritance).

Let’s define an Animal class with a method shout.

	public class Animal {
		public String bark() {
			return "Don't Know!";
		}
	}

Let’s create a sub class of Animal – Cat - overriding the existing shout method 
in Animal.

	class Cat extends Animal {
		public String bark() {
			return "Meow Meow";
		}
	}

bark method in Cat class is overriding the bark method in Animal class.

## Can super class reference variable can hold an object of sub class?
Yes, the super class reference variable can hold the sub class object actually, it is widening in case of objects (Conversion of lower datatype to a higher datatype).

But, using this reference you can access the members of super class only, if you try to access the sub class members a compile time error will be generated.

	class Vehicle {
	    public void drive() {
		System.out.println("Driving a vehicle.");
	    }
	}

	class Car extends Vehicle {
	    public void drive() {
		System.out.println("Driving a car.");
	    }

	    public void accelerate() {
		System.out.println("Accelerating the car.");
	    }
	}

        Vehicle vehicle1 = new Vehicle();
        Vehicle vehicle2 = new Car();
        Car car = new Car();

        vehicle1.drive();  // Output: Driving a vehicle.
        vehicle2.drive();  // Output: Driving a car.
        car.drive();       // Output: Driving a car.

        // vehicle2.accelerate();  // Error: The reference type is Vehicle which doesn't have the accelerate() method.
        ((Car) vehicle2).accelerate();  // Casting vehicle2 to Car type to access the accelerate() method.
        car.accelerate();               // Output: Accelerating the car.

## Is Multiple Inheritance allowed in Java?
No, multiple inheritance is not allowed for classes in Java. Java supports single inheritance, where a class can inherit from only one superclass. However, multiple inheritance is supported through interfaces, allowing a class to implement multiple interfaces and inherit their abstract method contracts.

	class Dog extends Animal, Pet { //COMPILER ERROR
	}

	However, we can create an Inheritance Chain
	class Pet extends Animal {
	}

	class Dog extends Pet {
	}


## What is an Interface?
An interface in Java is a blueprint of a class. It has static constants and abstract methods.

The interface in Java is a mechanism to achieve abstraction. There can be only abstract methods in the Java interface, not method body. It is used to achieve abstraction and multiple inheritance in Java.

In other words, you can say that interfaces can have abstract methods and variables. It cannot have a method body.

Java Interface also represents the IS-A relationship.

## How do you define an Interface?
An interface is declared by using the interface keyword. It provides total abstraction; means all the methods in an interface are declared with the empty body, and all the fields are public, static and final by default. A class that implements an interface must implement all the methods declared in the interface.

	interface InterfaceName {
	    // Constant declarations (optional)
	    // Method signatures (abstract methods)
	    // Default methods (optional)
	    // Static methods (optional)
	}

## How do you implement an interface?
To implement an interface in Java:

1. Create a class that will implement the interface.
2. Use the implements keyword followed by the name of the interface(s) you want to implement.
3. Implement all the methods declared in the interface by providing their implementations in the class.
4. Use the @Override annotation to indicate that the methods are overriding the ones in the interface.
5. Instantiate the class and use its implemented methods.


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

## Can you explain a few tricky things about interfaces?
Variables in an interface are always public, static, final. Variables in an 
interface cannot be declared private.

	interface ExampleInterface1 {
		//By default - public static final. No other modifier allowed
		//value1,value2,value3,value4 all are - public static final
		int value1 = 10;
		public int value2 = 15;
		public static int value3 = 20;
		public static final int value4 = 25;
		//private int value5 = 10;//COMPILER ERROR
	}

Interface methods are by default public and abstract. Before Java 8, A concrete 
method (fully defined method) cannot be created in an interface. Consider the 
example below:

	interface ExampleInterface1 {
		//By default - public abstract. No other modifier allowed
		void method1();//method1 is public and abstract
		//private void method6();//COMPILER ERROR!

		//This method, uncommented, would have given COMPILER ERROR!

		//in Java 7. Allowed from Java 8.
		default void method5() {
				System.out .println("Method5");
		}
	}

## Can you extend an interface?
No, we cannot directly extend an interface with another interface in Java using the extends keyword. Interfaces do not support inheritance through the extends keyword. Instead, interfaces can only be implemented by classes or extended indirectly through other interfaces. This means that a class can implement multiple interfaces, effectively inheriting and providing behavior from each interface.


## Can a class extend multiple interfaces?
Yes, in Java, a class can implement multiple interfaces. This allows the class to inherit and provide behavior from multiple sources. To implement multiple interfaces, the class declaration uses the implements keyword followed by the names of the interfaces, separated by commas.

	interface ExampleInterface2 {
		void method2();
	}

	class SampleImpl implements ExampleInterface1,ExampleInterface2{
		/* A class should implement all the methods in an interface.
		If either of method1 or method2 is commented, it would
		result in compilation error.
		*/
		public void method2() {
				System.out.println("Sample Implementation for Method2");
		}
		public void method1() {
				System.out.println("Sample Implementation for Method1");
		}
	}


## What is an Abstract Class?
An abstract class in Java is a class that cannot be directly instantiated and serves as a blueprint for other classes. It is declared using the abstract keyword and may contain both abstract and non-abstract methods. Abstract methods are declared without an implementation and must be overridden by subclasses. Abstract classes are meant to be extended by other classes using the extends keyword. They can have constructors and provide common behavior for subclasses. The purpose of an abstract class is to define common characteristics and behaviors that subclasses can inherit and implement.

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

## When do you use an Abstract Class?
An abstract class in Java is used when you want to define a common template or blueprint for a group of related classes. It is typically used in the following situations:

To provide a common set of methods or behavior that multiple subclasses can inherit.
When you have certain methods that need to be implemented by subclasses but have no meaningful implementation in the abstract class itself (abstract methods).
To establish a contract or interface that subclasses must adhere to.
When you want to provide default implementations for some methods while allowing subclasses to override them if needed.
When you want to create a base class that cannot be instantiated on its own but can be extended by subclasses.
The main purpose of an abstract class is to provide a structure and guidelines for subclasses, ensuring consistency and allowing for polymorphic behavior. It promotes code reuse, maintainability, and extensibility in object-oriented programming.


## How do you define an abstract method?
A method declared using the abstract keyword within an abstract class and does not have a definition (implementation) is called an abstract method.

When we need just the method declaration in a super class, it can be achieved by declaring the methods as abstracts.

Abstract method is also called subclass responsibility as it doesn't have the implementation in the super class. Therefore a subclass must override it to provide the method definition.

	abstract class Animal {
	    abstract void makeSound(); // Abstract method declaration
	}

	class Dog extends Animal {
	    @Override
	    void makeSound() {
		System.out.println("Bark!"); // Implementation of the abstract method
	    }
	}

## Compare Abstract Class vs Interface?

Abstract class	Interface
1) Abstract class can have abstract and non-abstract methods.	Interface can have only abstract methods. Since Java 8, it can have default and static methods also.
2) Abstract class doesn't support multiple inheritance.	Interface supports multiple inheritance.
3) Abstract class can have final, non-final, static and non-static variables.	Interface has only static and final variables.
4) Abstract class can provide the implementation of interface.	Interface can't provide the implementation of abstract class.
5) The abstract keyword is used to declare abstract class.	The interface keyword is used to declare interface.
6) An abstract class can extend another Java class and implement multiple Java interfaces.	An interface can extend another Java interface only.
7) An abstract class can be extended using keyword "extends".	An interface can be implemented using keyword "implements".
8) A Java abstract class can have class members like private, protected, etc.	Members of a Java interface are public by default.

	Example:
	
		public abstract class Shape{
			public abstract void draw();
		}
	Example:
	
		public interface Drawable{
			void draw();
		}

## What is a Constructor?
In Java, a constructor is a block of codes similar to the method. It is called when an instance of the class is created. At the time of calling constructor, memory for the object is allocated in the memory.

It is a special type of method which is used to initialize the object.

Every time an object is created using the new() keyword, at least one constructor is called.

It calls a default constructor if there is no constructor available in the class. In such case, Java compiler provides a default constructor by default.

There are two types of constructors in Java: no-arg constructor, and parameterized constructor.

Note: It is called constructor because it constructs the values at the time of object creation. It is not necessary to write a constructor for a class. It is because java compiler creates a default constructor if your class doesn't have any.

	class Animal {
		String name;
		// This is called a one argument constructor.
		public Animal(String name) {
			this.name = name;
		}
		public static void main(String[] args) {
		// Since we provided a constructor, compiler does not
		// provide a default constructor.
		// Animal animal = new Animal();//COMPILER ERROR!
		// The only way we can create Animal1 object is by using
			Animal animal = new Animal("Tommy");
		}
	}
	
## What is a Default Constructor?
Default Constructor is the constructor that is provided by the compiler. It has no arguments. In the
example below, there are no Constructors defined in the Animal class. Compiler provides us with a
default constructor, which helps us create an instance of animal class.

	public class Animal {
		String name;
		public static void main(String[] args) {
		// Compiler provides this class with a default no-argument constructor.
		// This allows us to create an instance of Animal class.
		Animal animal = new Animal();
		}
	}
	
## Will this code compile?
	class Animal {
		String name;
		public Animal() {
			this.name = "Default Name";
		}
	// This is called a one argument constructor.
		public Animal(String name) {
			this.name = name;
		}
		public static void main(String[] args) {
			Animal animal = new Animal();
		}
	}
Answer is no. Since we provided a constructor, compiler does not provide a default constructor

## How do you call a Super Class Constructor from a Constructor?
A constructor can call the constructor of a super class using the super() method call. Only constraint is
that it should be the first statement i
Both example constructors below can replaces the no argument "public Animal() " constructor in Example


	public Animal() {
		super();
		this.name = "Default Name";
	}

## Will this code Compile?
	public Animal() {
		this.name = "Default Name";
		super();
	}
Answer is NO. super should be always called on the first line of the constructor.

## What is the use of this()?
There can be a lot of usage of Java this keyword. In Java, this is a reference variable that refers to the current object.

Another constructor in the same class can be invoked from a constructor, using this({parameters})
method call.

	public Animal() {
		this("Default Name");
	}
	public Animal(String name) {
		this.name = name;
	}

## Can a constructor be called directly from a method?
No, you cannot call a constructor from a method. The only place from which you can invoke constructors using “this()” or, “super()” is the first line of another constructor. If you try to invoke constructors explicitly elsewhere, a compile time error will be generated.

	class Animal {
		String name;
			public Animal() {
		}
		public method() {
			Animal();// Compiler error
		}
	}


## Is a super class constructor called even when there is no explicit call from a sub class constructor ?
If a super class constructor is not explicitly called from a sub class constructor, super class (no argument)
constructor is automatically invoked (as first line) from a sub class constructor.
Consider the example below:

	class Animal {
		public Animal() {
			System.out.println("Animal Constructor");
		}
	}
	
	class Dog extends Animal {
		public Dog() {
			System.out.println("Dog Constructor");
		}
	}
	
	class Labrador extends Dog {
		public Labrador() {
			System.out.println("Labrador Constructor");
		}
	}
	
	public class ConstructorExamples {
		public static void main(String[] args) {
			Labrador labrador = new Labrador();
		}
	}
	Program Output
	Animal Constructor
	Dog Constructor
	Labrador Constructor


