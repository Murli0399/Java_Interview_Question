<details><summary>
	
# Java Platform 
</summary>
<details><summary>
	
## Why is Java so Popular?
</summary>
Java is one of the most popular languages because Java has several contributions to its widespread adoption and continued relevance in the software development industry. So Java has some key factors which make it  a popular programming language.

- **Simple:-** Java is easy to learn and its syntax is quite simple, clean, and easy to understand. Apart from this automatic memory management also play a role in the same
- **Object-Oriented**:- Java is ***object-oriented***, it supports all the OOPS characteristics. This makes Java applications easy to develop and maintain, compared to structured programming languages.
- **Platform Independent:-** Java source code is compiled and converted into bytecode. this bytecode can run on multiple platforms i.e. Write Once and Run Anywhere(WORA), we can compile the java code in one Operating System and execute it on another Operating System. The WORA makes java an Architecture Neutral language. Java also standardized all data types that also contributed to making java a platform-independent language.
</details>
  
<details><summary>
	
## What is Platform Independence?
</summary>
Platform independence, also known as "write once, run anywhere," refers to the ability of a programming language or framework to run on different platforms without requiring extensive modifications. In the context of Java, platform independence is one of the its key features.

Java is one of the most popular platform independent languages. Once we compile a java program and build a jar, we can run the jar (compiledjava program) in any Operating System - where a JVM is installed.Java achieves Platform Independence in a beautiful way. On compiling a java file the output is a class file- which contains an internal java representation called bytecode. 

JVM converts bytecode to executable instructions. The executable instructions are different in different operating systems. So, there aredifferent JVM's for different operating systems. A JVM for windows is different from a JVM for mac.However, both the JVM's understand the bytecode and convert it to the executable code for therespective operating system.
</details>
  
<details><summary>
	
## What is ByteCode?
</summary>
Bytecode is a low-level representation of code that is executed by a virtual machine (VM) rather than directly by the hardware. It serves as an intermediate step between source code and machine code, enabling platform independence and facilitating efficient execution.

If i talk about Java, when you write a Java program, it is first compiled into bytecode. And the Java compiler (javac) translates the human-readable Java source code into a compact and platform-neutral binary format which is called by bytecode. This bytecode is stored in .class files.

Bytecode is designed to be easily interpreted and executed by the Java Virtual Machine (JVM), which is specific to each platform or operating system. Instead of directly executing machine-specific instructions, the JVM reads the bytecode instructions one by one and dynamically translates them into machine code that can be executed by the underlying hardware.
</details>
  
<details><summary>
	
## Compare JDK vs JVM VS JRE.
</summary>
JDK (Java Development Kit), JVM (Java Virtual Machine), and JRE (Java Runtime Environment) are key components of the Java platform. Each serves a specific purpose in the Java development and execution process. Here's a comparison of these three components:
	
![Diagram](img/java_enviroment.png)
	
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
</details>
  
<details><summary>
	
## What is the role of class loader in java ?
</summary>
Java ClassLoader is an abstract class. It belongs to a java.lang package. It loads classes from different resources. Java ClassLoader is used to load the classes at run time. In other words, JVM performs the linking process at runtime. Classes are loaded into the JVM according to need. If a loaded class depends on another class, that class is loaded as well. When we request to load a class, it delegates the class to its parent. In this way, uniqueness is maintained in the runtime environment. It is essential to execute a Java program.
</details>
</details>
<details><summary>
	
# Wrapper Classes 
</summary>
  
<details><summary>
	
## What are wrapper classes?
</summary>
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
</details>
  
<details><summary>
	
## Why do we need Wrapper Classes in Java?
</summary>
The Java programming language treats primitive types and objects differently. Primitive types are not considered objects and do not have the capabilities of objects, such as methods and additional functionalities. However, there are situations where we may need to treat primitive types as objects, such as when working with collections, generics, or when using methods that require objects as arguments.
Wrapper classes bridge this gap by providing a way to wrap primitive types and use them as objects. 
</details>
  
<details><summary>
	
## What are the different ways of creating Wrapper Class Instances?
</summary>
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
</details>
  
<details><summary>
	
## What is Auto Boxing?
</summary>
### Autoboxing
The automatic conversion of primitive types to the object of their corresponding wrapper classes is known as autoboxing. For example – conversion of int to Integer, long to Long, double to Double, etc. 

	int num = 10;
	Integer myInteger = num;  // Autoboxing int to Integer

### Unboxing
It is just the reverse process of autoboxing. Automatically converting an object of a wrapper class to its corresponding primitive type is known as unboxing. For example – conversion of Integer to int, Long to long, Double to double, etc. 
	
	Integer myInteger = 20;
	int num = myInteger;  // Unboxing Integer to int
</details>
  
<details><summary>
	
## What are the advantages of Auto Boxing?
</summary>
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
</details>
  
<details><summary>
	
## What is Casting?
</summary>
Casting is a method or process that converts a data type into another data type in both ways manually and automatically. The automatic conversion is done by the compiler and manual conversion performed by the programmer.
Convert a value from one data type to another data type is known as type casting.

Types of Type Casting
There are two types of type casting:

Widening Type Casting (Implicit Casting)
Narrowing Type Casting (Explicit Casting)
</details>
  
<details><summary>
	
## What is Implicit Casting?
</summary>
Converting a lower data type into a higher one is called widening type casting. It is also known as implicit conversion or down casting. It is done by compiler or automatically. It is safe because there is no chance to lose data.
Both data types must be compatible with each other.
The target type must be larger than the source type.

byte -> short -> char -> int -> long -> float -> double  
	
	int value = 100;
	long number = value; //Implicit Casting
	float f = 100; //Implicit Casting
</details>
  
<details><summary>
	
## What is Explicit Casting?
</summary>
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
</details>
</details>
<details><summary>
	
# Strings
</summary>
  
<details><summary>
	
## Are all String’s immutable?
</summary>
A String is an unavoidable type of variable while writing any application program. String references are used to store various attributes like username, password, etc. In Java, String objects are immutable. Immutable simply means unmodifiable or unchangeable.

Once String object is created its data or state can't be changed but a new String object is created.
As Java uses the concept of String literal. Suppose there are 5 reference variables, all refer to one object "Sachin". If one reference variable changes the value of the object, it will be affected by all the reference variables. That is why String objects are immutable in Java.
</details>
	
<details><summary>
	
## Where are string values stored in memory?
</summary>
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
</details>
  
<details><summary>
	
## Why should you be careful about String Concatenation(+) operator in Loops?
</summary>
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
</details>
  
<details><summary>
	
## How do you solve above problem?
</summary>
To solve the performance problem associated with string concatenation using the + operator inside loops, we can use the StringBuilder class. StringBuilder provides a mutable buffer for efficiently constructing strings by appending individual values. 
	
	StringBuffer s3 = new StringBuffer("Value1");
	String s2 = "Value2";

	for (int i = 0; i < 100000; ++i) {
		s3.append(s2);
	}
</details>
  
<details><summary>
	
## What are differences between String and StringBuffer?
</summary>
String objects are immutable, while StringBuffer objects are mutable.
String concatenation involves creating new String objects, while StringBuffer allows in-place modifications.
String is not thread-safe, while StringBuffer is synchronized and thread-safe.
StringBuffer is more memory-efficient for frequent modifications, while String objects may result in additional memory usage.
Use String when immutability is desired, and StringBuffer when frequent modifications are needed.
</details>
  
<details><summary>
	
## What are differences between StringBuilder and StringBuffer?
</summary>
StringBuilder is not thread-safe, while StringBuffer is thread-safe.
StringBuilder provides better performance due to the absence of synchronization.
Use StringBuilder in single-threaded scenarios or when manual synchronization is applied.
Use StringBuffer in multi-threaded scenarios where thread safety is required.
</details>
  
<details><summary>
	
## Can you give examples of different utility methods in String class?
</summary>
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
</details>
 </details>
<details><summary>
	
# OOP's
</summary>
	
<details><summary>

## What is a Class?
</summary>
In object-oriented programming, a class is a blueprint or template that defines the structure and behavior of objects. It serves as a blueprint for creating instances, also known as objects, which are individual occurrences based on the class.

A class encapsulates data, known as attributes or fields, and defines the operations, known as methods or functions, that can be performed on that data. It provides a way to organize related data and behavior into a cohesive unit.
</details>
  
<details><summary>

## What is an Object?
</summary>
In object-oriented programming, an object is an instance of a class. It represents a specific occurrence or entity based on the structure and behavior defined by its class. An object combines data, known as attributes or properties, with the methods or functions that operate on that data.
</details>
  
<details><summary>

## What is state of an Object?
</summary>
The state of an object refers to the set of values stored in its attributes or instance variables at a given point in time. It represents the current snapshot of the object's data. The state of an object can change over time as its attributes are modified.
</details>
  
<details><summary>

## What is behavior of an Object?
</summary>
The behavior of an object refers to the actions or operations that an object can perform. It represents the functionality or capabilities associated with an object based on its class definition. The behavior is defined by the methods or functions defined within the class.
</details>
  
<details><summary>

## What is the super class of every class in Java?
</summary>
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
</details>
  
<details><summary>

## Explain about toString method ?
</summary>
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
</details>
  
<details><summary>

## What is the super class of every class in Java?
</summary>
In Java, the superclass of every class is the Object class. The Object class is at the top of the class hierarchy and serves as the root class for all other classes in Java.

The Object class is defined in the java.lang package and provides a set of common methods 
</details>
  
<details><summary>

## What is the use of equals method in Java ?
</summary>
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
</details>
  
<details><summary>

## What are the important things to consider when implementing equals method?
</summary>
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
</details>
  
<details><summary>

## What is the hashCode method used for in Java?
</summary>
The hashCode() method in Java is used to generate a unique integer value, known as the hash code, for an object. It is defined in the Object class and can be overridden by subclasses to provide a custom hash code implementation.

The primary purpose of the hashCode() method is to support efficient storage and retrieval of objects in hash-based data structures such as HashMap, HashSet, and Hashtable. These data structures use hash codes to determine the storage location (bucket) for objects, which allows for fast retrieval and efficient search operations.

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + id;
		return result;
	}
</details>
  
<details><summary>

## Explain inheritance with Examples?
</summary>
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
</details>
  
<details><summary>

## What is Method Overloading?
</summary>
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
</details>
  
<details><summary>

## What is Method Overriding?
</summary>
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
</details>
  
<details><summary>

## Can super class reference variable can hold an object of sub class?
</summary>
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
</details>
  
<details><summary>

## Is Multiple Inheritance allowed in Java?
</summary>
No, multiple inheritance is not allowed for classes in Java. Java supports single inheritance, where a class can inherit from only one superclass. However, multiple inheritance is supported through interfaces, allowing a class to implement multiple interfaces and inherit their abstract method contracts.

	class Dog extends Animal, Pet { //COMPILER ERROR
	}

	However, we can create an Inheritance Chain
	class Pet extends Animal {
	}

	class Dog extends Pet {
	}

</details>
  
<details><summary>

## What is an Interface?
</summary>
An interface in Java is a blueprint of a class. It has static constants and abstract methods.

The interface in Java is a mechanism to achieve abstraction. There can be only abstract methods in the Java interface, not method body. It is used to achieve abstraction and multiple inheritance in Java.

In other words, you can say that interfaces can have abstract methods and variables. It cannot have a method body.

Java Interface also represents the IS-A relationship.
</details>
  
<details><summary>

## How do you define an Interface?
</summary>
An interface is declared by using the interface keyword. It provides total abstraction; means all the methods in an interface are declared with the empty body, and all the fields are public, static and final by default. A class that implements an interface must implement all the methods declared in the interface.

	interface InterfaceName {
	    // Constant declarations (optional)
	    // Method signatures (abstract methods)
	    // Default methods (optional)
	    // Static methods (optional)
	}
</details>
  
<details><summary>

## How do you implement an interface?
</summary>
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
</details>
  
<details><summary>
	
## Can you explain a few tricky things about interfaces?
</summary>
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
</details>
  
<details><summary>
	
## Can you extend an interface?
</summary>
No, we cannot directly extend an interface with another interface in Java using the extends keyword. Interfaces do not support inheritance through the extends keyword. Instead, interfaces can only be implemented by classes or extended indirectly through other interfaces. This means that a class can implement multiple interfaces, effectively inheriting and providing behavior from each interface.

</details>
  
<details><summary>
	
## Can a class extend multiple interfaces?
</summary>
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

</details>
  
<details><summary>
	
## What is an Abstract Class?
</summary>
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
</details>
  
<details><summary>
	
## When do you use an Abstract Class?
</summary>
An abstract class in Java is used when you want to define a common template or blueprint for a group of related classes. It is typically used in the following situations:

To provide a common set of methods or behavior that multiple subclasses can inherit.
When you have certain methods that need to be implemented by subclasses but have no meaningful implementation in the abstract class itself (abstract methods).
To establish a contract or interface that subclasses must adhere to.
When you want to provide default implementations for some methods while allowing subclasses to override them if needed.
When you want to create a base class that cannot be instantiated on its own but can be extended by subclasses.
The main purpose of an abstract class is to provide a structure and guidelines for subclasses, ensuring consistency and allowing for polymorphic behavior. It promotes code reuse, maintainability, and extensibility in object-oriented programming.

</details>
  
<details><summary>
	
## How do you define an abstract method?
</summary>
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
</details>
  
<details><summary>
	
## Compare Abstract Class vs Interface?
</summary>

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
</details>
  
<details><summary>
	
## What is a Constructor?
</summary>
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
</details>
  
<details><summary>
	
## What is a Default Constructor?
</summary>	
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
</details>
  
<details><summary>
	
## Will this code compile?
</summary>	
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
</details>
  
<details><summary>
	
## How do you call a Super Class Constructor from a Constructor?
</summary>	
A constructor can call the constructor of a super class using the super() method call. Only constraint is
that it should be the first statement i
Both example constructors below can replaces the no argument "public Animal() " constructor in Example


	public Animal() {
		super();
		this.name = "Default Name";
	}
</details>
  
<details><summary>
	
## Will this code Compile?
</summary>
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
</details>
  
<details><summary>
	
## Can a constructor be called directly from a method?
</summary>
No, you cannot call a constructor from a method. The only place from which you can invoke constructors using “this()” or, “super()” is the first line of another constructor. If you try to invoke constructors explicitly elsewhere, a compile time error will be generated.

	class Animal {
		String name;
			public Animal() {
		}
		public method() {
			Animal();// Compiler error
		}
	}

</details>
  
<details><summary>

## Is a super class constructor called even when there is no explicit call from a sub class constructor?
</summary>
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

</details>
	</details>
	
<details><summary>
	
# Advance OOP's
</summary>	
## What is Polymorphism?
Polymorphism in Java is the ability of an object to take on many forms. It allows a reference variable of a superclass to represent objects of its subclasses. In other words, it enables objects of different classes to be treated as objects of a common superclass during runtime.

There are two types of polymorphism in Java:

### Compile-time Polymorphism (Method Overloading):

Method overloading allows multiple methods in the same class with the same name but different parameter lists.
The appropriate method is chosen at compile time based on the arguments passed to the method.
###Runtime Polymorphism (Method Overriding):

Method overriding occurs when a subclass provides its own implementation of a method that is already defined in its superclass.
The method to be executed is determined at runtime based on the actual object being referred to by the reference variable.
Polymorphism is achieved through inheritance, where subclasses inherit the properties and behaviors of their superclass. It allows for code reuse, flexibility, and the ability to write generic code that can operate on objects of different types.

    class Animal {
      public void makeSound() {
          System.out.println("Animal makes a sound");
      }
    }

    class Dog extends Animal {
      @Override
      public void makeSound() {
          System.out.println("Dog barks");
      }
    }

    class Cat extends Animal {
        @Override
        public void makeSound() {
            System.out.println("Cat meows");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Animal animal1 = new Dog(); // Dog object assigned to Animal reference
            Animal animal2 = new Cat(); // Cat object assigned to Animal reference

            animal1.makeSound(); // Output: Dog barks
            animal2.makeSound(); // Output: Cat meows
        }
    }

## What is the use of instanceof Operator in Java?
The instanceof operator in Java is used to test if an object is an instance of a particular class or implements a specific interface. It allows you to check the type of an object at runtime.

The instanceof operator has the following syntax:

    object instanceof Class

Here, object is the reference variable whose type is being checked, and Class is the class or interface that is being tested against. The operator returns a boolean value: true if the object is an instance of the specified class or implements the specified interface, and false otherwise.

The instanceof operator is commonly used in scenarios such as:

Type checking: You can use instanceof to determine the actual type of an object before performing certain operations or casting it to a specific type. This helps avoid potential type casting errors at runtime.

Polymorphism and inheritance: instanceof can be used to determine if an object is an instance of a specific subclass or superclass. This allows you to apply different behaviors or logic based on the actual type of the object.

Here's an example that demonstrates the use of the instanceof operator:

    class Animal { }
    class Dog extends Animal { }
    class Cat extends Animal { }

    public class Main {
        public static void main(String[] args) {
            Animal animal1 = new Dog();
            Animal animal2 = new Cat();
            Animal animal3 = new Animal();

            System.out.println(animal1 instanceof Dog);  // Output: true
            System.out.println(animal2 instanceof Cat);  // Output: true
            System.out.println(animal3 instanceof Animal);  // Output: true
            System.out.println(animal1 instanceof Animal);  // Output: true
            System.out.println(animal2 instanceof Dog);  // Output: false
        }
    }

## What is Coupling?
Coupling in Java refers to the degree of dependency or interconnectedness between classes or components within a software system. It measures how closely one class or component relies on or interacts with another.

In general, low coupling is desirable as it promotes better software design, modularity, and maintainability. High coupling, on the other hand, can lead to code that is difficult to understand, modify, and reuse.

- **Tight coupling** - When an object creates the object to be used, then it is a tight coupling situation. As the main object creates the object itself, this object can not be changed from outside world easily marked it as tightly coupled objects.

        
        public class Tester {
            public static void main(String args[]) {
                A a = new A();

                  //a.display() will print A and B
                  //this implementation can not be changed dynamically
                  //being tight coupling
                  a.display();
            }
        }

        class A {
           B b;
           public A() {
              //b is tightly coupled to A
              b = new B();
           }

           public void display() {
              System.out.println("A");
              b.display();
           }
        }

        class B {    
           public B(){}
           public void display() {
              System.out.println("B");
           }
        }


- **Loose coupling** - When an object gets the object to be used from the outside, then it is a loose coupling situation. As the main object is merely using the object, this object can be changed from the outside world easily marked it as loosely coupled objects.

        public class Tester {
           public static void main(String args[]) throws IOException {
              Show b = new B();
              Show c = new C();

              A a = new A(b);          
              //a.display() will print A and B    
              a.display();

              A a1 = new A(c);
              //a.display() will print A and C    
              a1.display();
           }
        }

        interface Show {
           public void display();
        }

        class A {
           Show s;
           public A(Show s) {
              //s is loosely coupled to A
              this.s = s;
           }

           public void display() {
              System.out.println("A");
              s.display();
           }
        }

        class B implements Show {    
           public B(){}
           public void display() {
              System.out.println("B");
           }
        }

        class C implements Show {    
           public C(){}
           public void display() {
              System.out.println("C");
           }
        }

Reducing coupling is typically achieved through good software design practices, such as following the principles of encapsulation, abstraction, and dependency inversion. Using design patterns, interfaces, and dependency injection can also help to decouple components and promote modular and reusable code.

By minimizing coupling, you can improve code maintainability, reusability, testability, and overall software quality. It allows for easier understanding and modification of individual components without affecting the entire system.

## What is Cohesion?
Cohesion in Java is the principle of Object-Oriented programming. Cohesion is closely related to ensuring that the purpose for which a class is getting created in Java is well-focused and single. In other words, the more closely related stuff is grouped in a class, the higher will be the cohesiveness.

**Example Problem** - Example class below is downloading from internet, parsing data and storing data 
to database. Theresponsibilities of this class are not really related. This is 
not cohesive class.

    class DownloadAndStore{
            void downloadFromInternet(){
            }

            void parseData(){
            }

            void storeIntoDatabase(){
            }

            void doEverything(){
                    downloadFromInternet();
                    parseData();
                    storeIntoDatabase();
            }
    }

**Solution** - This is a better way of approaching the problem. Different classes have their 
own responsibilities.

    class InternetDownloader {
            public void downloadFromInternet() {
            }
    }

    class DataParser {
            public void parseData() {
            }
    }

    class DatabaseStorer {
            public void storeIntoDatabase() {
            }
    }

    class DownloadAndStore {
            void doEverything() {
                    new InternetDownloader().downloadFromInternet();
                    new DataParser().parseData();
                    new DatabaseStorer().storeIntoDatabase();
            }
    }

## What is Encapsulation?
Encapsulation in Java is a process of wrapping code and data together into a single unit, for example, a capsule which is mixed of several medicines.

We can create a fully encapsulated class in Java by making all the data members of the class private. Now we can use setter and getter methods to set and get the data in it.

The Java Bean class is the example of a fully encapsulated class.

### Advantage of Encapsulation in Java
- By providing only a setter or getter method, you can make the class read-only or write-only. In other words, you can skip the getter or setter methods.

- It provides you the control over the data. Suppose you want to set the value of id which should be greater than 100 only, you can write the logic inside the setter method. You can write the logic not to store the negative numbers in the setter methods.

- It is a way to achieve data hiding in Java because other class will not be able to access the data through the private data members.

- The encapsulate class is easy to test. So, it is better for unit testing.

- The standard IDE's are providing the facility to generate the getters and setters. So, it is easy and fast to create an encapsulated class in Java.

        Approach 1
        In this approach we create a public variable score. The main method directly 
        accesses the score variable, updates it.

        public class CricketScorer {
                public int score;
        }

        Let’s use the CricketScorer class.
        public static void main(String[] args) {
                CricketScorer scorer = new CricketScorer();
                scorer.score = scorer.score + 4;
        }

        Approach 2
        In this approach, we make score as private and access value through get and set 
        methods. However, the logic of adding 4 to the score is performed in the main 
        method.

        public class CricketScorer {
                private int score;

                public int getScore() {
                        return score;
                }

                public void setScore(int score) {
                        this.score = score;
                }
        }

        Let’s use the CricketScorer class.

        public static void main(String[] args) {
                CricketScorer scorer = new CricketScorer();
                int score = scorer.getScore();
                scorer.setScore(score + 4);
        }


        Approach 3
        In this approach - For better encapsulation, the logic of doing the four 
        operation also is moved to the CricketScorer class.

        public class CricketScorer {
                private int score;
                        public void four() {
                                score += 4;
                        }
        }

        Let’s use the CricketScorer class.
        public static void main(String[] args) {
                CricketScorer scorer = new CricketScorer();
                scorer.four();
        }

**Description** - In terms of encapsulation Approach 3 > Approach 2 > Approach 1. In Approach 3, 
the user of scorer class does not even know that there is a variable called 
score. Implementation of Scorer can change without changing other classes using 
Scorer.

## What is an Inner Class?
Java inner class or nested class is a class that is declared inside the class or interface.

We use inner classes to logically group classes and interfaces in one place to be more readable and maintainable.

Additionally, it can access all the members of the outer class, including private data members and methods.

### Advantage of Java inner classes

- Nested classes represent a particular type of relationship that is it can access all the members (data members and methods) of the outer class, including private.
- Nested classes are used to develop more readable and maintainable code because it logically group classes and interfaces in one place only.
- Code Optimization: It requires less code to write.

        class OuterClass {
            public class InnerClass {
            }
        }

## What is a Static Inner Class?
A static class is a class that is created inside a class, is called a static nested class in Java. It cannot access non-static data members and methods. It can be accessed by outer class name.

It can access static data members of the outer class, including private.
The static nested class cannot access non-static (instance) data members or

Inner Classes are classes which are declared inside other classes. Consider the following example:

    class OuterClass {
         public static class StaticNestedClass {
         }
    }

## Can you create an inner class inside a method?
we can write a class within a method and this will be a local type. Like local variables, the scope of the inner class is restricted within the method.

A method-local inner class can be instantiated only within the method where the inner class is defined. 

    class OuterClass {
		public void exampleMethod() {
			class MethodLocalInnerClass {
				
			};
		}
    }

## What is an Anonymous Class?
Java anonymous inner class is an inner class without a name and for which only a single object is created. An anonymous inner class can be useful when making an instance of an object with certain "extras" such as overloading methods of a class or interface, without having to actually subclass a class.

In simple words, a class that has no name is known as an anonymous inner class in Java. It should be used if you have to override a method of class or interface. Java Anonymous inner class can be created in two ways:

1. Class (may be abstract or concrete).
2. Interface

Below examples shows various ways to create Anonymous classes.

	class Animal {
		void bark() {
			System.out .println("Animal Bark");
		}
	};

	public class AnonymousClass {
		private static String[] reverseSort(String[] array) {
			Comparator<String> reverseComparator = new Comparator<String>() {	
				/* Anonymous Class */
				@Override
				public int compare(String string1, String string2) {
					return string2.compareTo(string1);
				}
			};
		Arrays.sort(array, reverseComparator);
		return array;
	}

	public static void main(String[] args) {
		String[] array = { "Apple", "Cat", "Boy" };
		System.out .println(Arrays.toString(reverseSort(array)));//[Cat, Boy, Apple]
		
		/* Second Anonymous Class - SubClass of Animal*/
		Animal animal = new Animal() {
			oid bark() {
				System.out .println("Subclass bark");
			}
		};
		animal.bark();//Subclass bark
		}
	}



</details>	
	
<details><summary>
	
# Modifires
</summary>	
## What is default class modifier?
In Java, the default class modifier, also known as package-private or default access, is a level of access control that is applied when no explicit access modifier is specified for a class, method, or field. It is denoted by the absence of the public, private, or protected keywords.

When a class member (class, method, or field) is declared with the default modifier, it is accessible only within the same package (i.e., the classes that belong to the same package). It is not accessible outside of the package, including subclasses in other packages.

Example

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

## What is private access modifier?
In Java, the private access modifier is one of the four access modifiers used to control the visibility and accessibility of class members, including variables, methods, and nested classes, within a class.

When a class member is declared as private, it is accessible only within the same class where it is defined. It is not visible or accessible from any other class, including subclasses and other classes in the same package.

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

## What is default or package access modifier?
In Java, the default or package access modifier is a level of access control that is applied when no explicit access modifier is specified for a class, method, or field. It is denoted by the absence of the public, private, or protected keywords.

When a class member (class, method, or field) is declared with the default modifier, it is accessible within the same package (i.e., the classes that belong to the same package). It is not accessible outside of the package, including subclasses in other packages.

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

## What is protected access modifier?
In Java, the protected access modifier is one of the four access modifiers used to control the visibility and accessibility of class members, including variables, methods, and nested classes.

When a class member is declared as protected, it is accessible within the same package and can also be accessed by subclasses (whether they are in the same package or not) and non-subclasses outside the package.

	package com.example;

	public class Superclass {
	    protected int protectedField;

	    protected void protectedMethod() {
		System.out.println("This is a protected method.");
	    }
	}

	public class Subclass extends Superclass {
	    public void accessProtectedMember() {
		protectedField = 10;      // Accessible in subclass
		protectedMethod();        // Accessible in subclass
	    }
	}

	public class Main {
	    public static void main(String[] args) {
		Subclass subclassObject = new Subclass();
		subclassObject.accessProtectedMember();  // Accessible in subclass
	    }
	}
	
## What is public access modifier?
In Java, the public access modifier is one of the four access modifiers used to control the visibility and accessibility of class members, including variables, methods, and nested classes.

When a class member is declared as public, it is accessible from any other class, regardless of the package or subclass relationship. It provides the highest level of visibility and allows unrestricted access to the member.

The public access modifier is used when you want a class member to be accessible and visible from any part of the program. It is typically used for creating public APIs, exposing functionality to other classes, and facilitating easy integration with other modules or libraries.

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

## What access types of variables can be accessed from a Class in Same Package?
In Java, when a class is in the same package as another class, it has access to the following types of variables in the other class:

1. Public variables: Public variables can be accessed directly from any class, regardless of the package. Thus, a class in the same package can access public variables in another class.

2. Default (package-private) variables: Default variables are accessible within the same package but not outside of it. Therefore, a class in the same package can access the default variables in another class.

3. Protected variables: Protected variables are accessible within the same package as well as by subclasses, even if they are in a different package. However, if the class in the same package is not a subclass, it cannot access protected variables.

Look at the code below to understand what can be accessed and what cannot be.

	package com.rithus.membermodifiers.access;

	public class TestClassInSamePackage {
		public static void main(String[] args) {
				ExampleClass example = new ExampleClass();

				example.publicVariable = 5;
				example.publicMethod();

				//privateVariable is not visible
				//Below Line, uncommented, would give compiler error
				//example.privateVariable=5; //COMPILE ERROR
				//example.privateMethod();

				example.protectedVariable = 5;
				example.protectedMethod();

				example.defaultVariable = 5;
				example.defaultMethod();
		}
	}
	
## What access types of variables can be accessed from a Class in Different Package?	
In Java, when a class is in a different package than another class, it has access to the following types of variables in the other class:

1. Public variables: Public variables can be accessed directly from any class, regardless of the package. Therefore, a class in a different package can access public variables in another class.	
	
Look at the code below to understand what can be accessed and what cannot be.

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
	
## What access types of variables can be accessed from a Sub Class in Same Package?	
In Java, when a subclass is in the same package as its superclass, it has access to the following types of variables in the superclass:

1. Public variables: Public variables can be accessed directly from any class, including subclasses. Therefore, a subclass in the same package can access public variables in its superclass.

2. Protected variables: Protected variables are accessible within the same package as well as by subclasses, even if they are in a different package. Therefore, a subclass in the same package can access protected variables in its superclass.

3. Default (package-private) variables: Default variables are accessible within the same package but not outside of it. Therefore, a subclass in the same package can access the default variables in its superclass.
	
Look at the code below to understand what can be accessed and what cannot be.

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
	
## What access types of variables can be accessed from a Sub Class in Different Package?	
In Java, when a subclass is in a different package than its superclass, it has access to the following types of variables in the superclass:

1. Public variables: Public variables can be accessed directly from any class, including subclasses. Therefore, a subclass in a different package can access public variables in its superclass.

2. Protected variables: Protected variables are accessible within the same package as well as by subclasses, even if they are in a different package. Therefore, a subclass in a different package can access protected variables in its superclass if it is a subclass of the superclass.	
	
Look at the code below to understand what can be accessed and what cannot be.

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
	
## What is the use of a final modifier on a class ?
In Java, the final modifier can be used to restrict the behavior of a class. When a class is declared as final, it means that it cannot be subclassed or extended by other classes. Here are the main uses of the final modifier on a class:

1. Preventing inheritance: When a class is declared as final, it cannot be subclassed or extended by other classes. This ensures that the class's implementation and behavior cannot be modified or overridden, providing a level of control and stability.

2. Performance optimizations: Declaring a class as final allows the compiler and runtime environment to perform certain optimizations. Since a final class cannot be subclassed, method calls can be resolved at compile-time instead of runtime, leading to potential performance improvements.
	
		Final Class examples : String, Integer, Double and other wrapper classes

		final public class FinalClass {
		}

		Below class will not compile if uncommented. FinalClass cannot be extended.

		/*
		class ExtendingFinalClass extends FinalClass{ //COMPILER ERROR

		}
		*/	
	
## What is the use of a final modifier on a method ?
In Java, the final modifier can be applied to a method to indicate that the method cannot be overridden by subclasses. Here are the main uses of the final modifier on a method:

1. Preventing method overriding: When a method is declared as final, it cannot be overridden by subclasses. This ensures that the behavior of the method remains unchanged and consistent throughout the class hierarchy.

2. Efficiency and performance: Marking a method as final allows the compiler to perform certain optimizations. Since the method cannot be overridden, the compiler can make direct invocations of the method without the need for dynamic dispatch, which can result in improved performance.
	
		public class FinalMemberModifiersExample {
			final void finalMethod(){
			}
		}

		Any SubClass extending above class cannot override the finalMethod().

		class SubClass extends FinalMemberModifiersExample {
			//final method cannot be over-riddent
			//Below method, uncommented, causes compilation Error
			/*
			final void finalMethod(){

			}
			*/
		}	
	
## What is a Final Variable ?
In Java, a final variable is a variable that cannot be reassigned once it has been assigned a value. Once a final variable is assigned a value, its value remains constant throughout the program's execution.  It provides immutability, represents constants, and can contribute to thread safety in concurrent programs.

	public class MyClass {
	    private final int myFinalVariable = 10;

	    public void myMethod() {
		// Cannot reassign value to myFinalVariable
		// myFinalVariable = 20;  // This would cause a compilation error
	    }
	}

## What is a Final Argument ?
In Java, a final argument refers to a method parameter that is declared with the final modifier. When a method parameter is marked as final, it means that its value cannot be changed within the method body. Ensure its immutability and read-only access within the method. It communicates the intent that the parameter should not be modified and provides an extra level of safety in method implementation.

	public void myMethod(final int value) {
	    // Cannot modify the value of the 'value' parameter
	    // value = 10;  // This would cause a compilation error

	    // Read-only access to the 'value' parameter
	    int result = value * 2;
	    System.out.println(result);
	}

## What is a Static Variable ?
In Java, a static variable, also known as a class variable, is a variable that belongs to the class itself rather than to any particular instance of the class. This means that all instances of the class share the same copy of the static variable. Here are some key points about static variables:

1. Shared by all instances: Static variables are shared by all instances of a class. Any modification to the static variable is reflected across all instances of the class.

2. Memory allocation: Static variables are allocated memory once, when the class is loaded into memory. They exist throughout the entire execution of the program, regardless of the number of instances created.

3. Accessed using the class name: Since static variables belong to the class itself, they are accessed using the class name followed by the variable name, rather than through an instance of the class.

4. Initialization: Static variables can be initialized at the time of declaration or within a static block, which is a block of code that runs when the class is loaded.

5. Usage: Static variables are commonly used to store values that are shared among all instances of a class, such as constants, configuration settings, or counters.

Static Variable/Method – Example
count variable in Cricketer class is static. The method to get the count value 
getCount() is also a static method.

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

4 instances of the Cricketer class are created. Variable count is incremented 
with every instance createdin the constructor.
</details>	
	
<details><summary>
	
# Collections
</summary>	
	
</details>	
	
<details><summary>
	
# Exception Handling
</summary>	
	
</details>	
	
<details><summary>
	
# Multi Threading
</summary>	
	
</details>	
	
<details><summary>
	
# Serialization
</summary>	
	
</details>
