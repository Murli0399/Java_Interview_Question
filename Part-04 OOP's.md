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
