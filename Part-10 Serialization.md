<details><summary>
	
## What is Garbage Collection?
</summary>
Garbage collection in Java is the process by which Java programs perform automatic memory management. Java programs compile to bytecode that can be run on a Java Virtual Machine. When Java programs run on the JVM, objects are created on the heap, which is a portion of memory dedicated to the program. Eventually, some objects will no longer be needed. The garbage collector finds these unused objects and deletes them to free up memory.
</details>
<details><summary>
	
## Can you explain Garbage Collection with an example?
</summary>
Let’s say the below method is called from a function.

      void method(){
          Calendar calendar = new GregorianCalendar(2000,10,30);
          System.out.println(calendar);
      }
      
An object of the class GregorianCalendar is created on the heap by the first line of the function with one
reference variable calendar.

After the function ends execution, the reference variable calendar is no longer valid. Hence, there are no
references to the object created in the method.

JVM recognizes this and removes the object from the heap. This is called Garbage Collection.
</details>
<details><summary>
	
## When is Garbage Collection run?
</summary>
Garbage collection in Java is run automatically by the Java Virtual Machine (JVM) as needed. The JVM determines when to initiate garbage collection based on certain conditions. These conditions can vary depending on the JVM implementation, but some common triggers include:

- **Memory Pressure:** Garbage collection may be triggered when the JVM detects that the available memory is running low or is close to reaching its limit. This helps to reclaim memory occupied by unreferenced objects and make it available for future allocations.

- **Allocation Failure:** If an allocation request cannot be fulfilled due to insufficient memory, the JVM may trigger garbage collection to free up memory and make room for new object allocations.

- **System Idle:** Garbage collection may be initiated during periods of low system activity or when the application is idle. This minimizes the impact on the application's performance.

It's important to note that the JVM manages the garbage collection process internally, and the exact timing and frequency of garbage collection cycles are determined by the JVM implementation. The JVM employs various garbage collection algorithms and techniques to optimize the collection process and minimize its impact on the application's execution.
</details>
<details><summary>
	
## What are best practices on Garbage Collection?
</summary>
Programmatically, we can request (remember it’s just a request - Not an order) JVM to run Garbage
Collection by calling System.gc() method.

JVM might throw an OutOfMemoryException when memory is full and no objects on the heap are eligible
for garbage collection.

finalize() method on the objected is run before the object is removed from the heap from the garbage
collector. We recommend not to write any code in finalize();
</details>
<details><summary>
	
## What are Initialization Blocks?
</summary>
In Java, initialization blocks are code blocks that are used to initialize the state of a class or an instance of a class. There are two types of initialization blocks: instance initialization blocks and static initialization blocks.

**1. Instance Initialization Blocks:** These blocks are executed when an instance of a class is created. They are enclosed in curly braces {} and are not associated with any specific method or constructor. Instance initialization blocks are useful when you need to perform complex initialization logic that cannot be handled by instance variables or constructors alone.
Here's an example of an instance initialization block:

        public class MyClass {
            private int x;
            private int y;

            // Instance initialization block
            {
                x = 5;
                y = 10;
                System.out.println("Instance initialization block executed");
            }

            // Rest of the class...
        }

In the above example, the instance initialization block sets the values of x and y to 5 and 10, respectively. It also prints a message when executed.

**2. Static Initialization Blocks:** These blocks are executed when the class is first loaded into memory, before any instance of the class is created. Static initialization blocks are denoted by the static keyword and are also enclosed in curly braces {}. They are often used to initialize static variables or perform other static initialization tasks.
Here's an example of a static initialization block:

        public class MyClass {
            private static int count;

            // Static initialization block
            static {
                count = 0;
                System.out.println("Static initialization block executed");
            }

            // Rest of the class...
        }

In this example, the static initialization block sets the initial value of the count variable to 0 and prints a message when executed.

Both instance and static initialization blocks are executed in the order they appear in the code. If a class has multiple initialization blocks, they are executed from top to bottom.

Initialization blocks provide a way to perform additional initialization logic beyond what can be achieved with constructors and instance/static variables alone. They are particularly useful when you need to initialize variables based on complex calculations, retrieve values from external sources, or perform other initialization tasks that cannot be expressed in a single line of code.
</details>