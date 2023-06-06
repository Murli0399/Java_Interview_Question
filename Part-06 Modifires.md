<details><summary>
	
## What is default class modifier?
</summary>
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

</details>
<details><summary>
	
## What is private access modifier?
</summary>
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

</details>
<details><summary>
	
## What is default or package access modifier?
</summary>
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

</details>
<details><summary>
	
## What is protected access modifier?
</summary>
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

</details>
<details><summary>
	
## What is public access modifier?
</summary>
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

</details>
<details><summary>
	
## What access types of variables can be accessed from a Class in Same Package?
</summary>
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

</details>
<details><summary>
	
## What access types of variables can be accessed from a Class in Different Package?
</summary>	
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
	
</details>
<details><summary>
	
## What access types of variables can be accessed from a Sub Class in Same Package?
</summary>	
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

</details>
<details><summary>
	
## What access types of variables can be accessed from a Sub Class in Different Package?
</summary>
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

</details>
<details><summary>
	
## What is the use of a final modifier on a class ?
</summary>
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

</details>
<details><summary>
	
## What is the use of a final modifier on a method ?
</summary>
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

</details>
<details><summary>
	
## What is a Final Variable ?
</summary>
In Java, a final variable is a variable that cannot be reassigned once it has been assigned a value. Once a final variable is assigned a value, its value remains constant throughout the program's execution.  It provides immutability, represents constants, and can contribute to thread safety in concurrent programs.

	public class MyClass {
	    private final int myFinalVariable = 10;

	    public void myMethod() {
		// Cannot reassign value to myFinalVariable
		// myFinalVariable = 20;  // This would cause a compilation error
	    }
	}

</details>
<details><summary>
	
## What is a Final Argument ?
</summary>
In Java, a final argument refers to a method parameter that is declared with the final modifier. When a method parameter is marked as final, it means that its value cannot be changed within the method body. Ensure its immutability and read-only access within the method. It communicates the intent that the parameter should not be modified and provides an extra level of safety in method implementation.

	public void myMethod(final int value) {
	    // Cannot modify the value of the 'value' parameter
	    // value = 10;  // This would cause a compilation error

	    // Read-only access to the 'value' parameter
	    int result = value * 2;
	    System.out.println(result);
	}

</details>
<details><summary>
	
## What happens when a variable is marked as volatile?
</summary>
In Java, when a variable is marked as volatile, it means that the variable's value may be modified by multiple threads, and any changes to the variable should be immediately visible to other threads. The volatile keyword ensures that the variable is always read from and written to the main memory, rather than using a thread's cache.

When a variable is declared as volatile, the following behaviors are guaranteed:

**1. Visibility:** Changes made to a volatile variable by one thread are immediately visible to all other threads. This ensures that the most up-to-date value of the variable is always seen by all threads.

**3. Ordering:** The volatile keyword also provides a guarantee about the ordering of actions performed on the variable. It ensures that the read and write operations on the volatile variable are not reordered with other memory operations.

It's important to note that the volatile keyword only provides guarantees for individual variable accesses. It does not guarantee the atomicity of compound actions, such as incrementing a volatile variable. For atomic operations, you would need to use other mechanisms, such as locks or atomic classes like AtomicInteger, AtomicLong, etc.

The main use case for the volatile keyword is in scenarios where variables are shared among multiple threads, and you want to ensure that the changes made by one thread are immediately visible to others without the need for explicit synchronization mechanisms like locks.
</details>
<details><summary>
	
## What is a Static Variable ?
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