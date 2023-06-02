<details><summary>
	
## What are wrapper classes?
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
