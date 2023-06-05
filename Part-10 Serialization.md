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
<details><summary>
	
## What is Serialization?
</summary>
Serialization is the process of converting an object into a format that can be stored or transmitted and later reconstructed to its original form. In the context of Java programming, serialization refers to the mechanism provided by the Java platform to convert objects into a byte stream and vice versa.
</details>
<details><summary>
	
## How do you serialize an object using Serializable interface?
</summary>
To serialize an object in Java using the Serializable interface, you need to follow these steps:

- **Implement the Serializable interface:** Ensure that the class of the object you want to serialize implements the Serializable interface. This is a marker interface with no methods, but its presence indicates that the class can be serialized.

- **Create an output stream:** Create an output stream to which the serialized object will be written. This can be a file output stream, network stream, or any other type of output stream that suits your needs.

- **Create an ObjectOutputStream:** Wrap the output stream with an ObjectOutputStream instance. This class provides the functionality to write objects to the output stream.

- **Call writeObject():** Use the writeObject() method of the ObjectOutputStream to serialize the object. Pass the object you want to serialize as the argument to this method.

- **Close the streams:** Close the ObjectOutputStream and the underlying output stream to ensure proper resource cleanup.

Here's an example that demonstrates the serialization process:

        import java.io.FileOutputStream;
        import java.io.IOException;
        import java.io.ObjectOutputStream;
        import java.io.Serializable;

        public class SerializationExample {
            public static void main(String[] args) {
                // Create an object to serialize
                Student student = new Student("John", 20);

                try {
                    // Create an output stream
                    FileOutputStream fileOut = new FileOutputStream("student.ser");

                    // Create an ObjectOutputStream
                    ObjectOutputStream out = new ObjectOutputStream(fileOut);

                    // Serialize the object
                    out.writeObject(student);

                    // Close the streams
                    out.close();
                    fileOut.close();

                    System.out.println("Object serialized successfully.");
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

        class Student implements Serializable {
            private String name;
            private int age;

            public Student(String name, int age) {
                this.name = name;
                this.age = age;
            }

            // Getters and setters...
        }

In this example, the Student class implements the Serializable interface. An instance of the Student class is created and then serialized using the ObjectOutputStream by calling the writeObject() method. The serialized object is written to a file named "student.ser" using a FileOutputStream.

It's important to note that not all objects can be serialized. Certain types of objects, such as those with non-serializable fields or objects of classes that explicitly prevent serialization, will throw a NotSerializableException at runtime if an attempt is made to serialize them.
</details>
<details><summary>
	
## How do you de-serialize in Java?
</summary>
In Java, deserialization is the process of converting an object from its serialized form (such as a byte stream or a file) back into an object that can be used within the Java program. To deserialize an object, you can follow these steps:

Ensure that the class of the object being deserialized is available in the classpath. The class should have the same structure and field names as when it was serialized.

Create an instance of the ObjectInputStream class, passing an appropriate InputStream as a parameter. This input stream can be a FileInputStream, a ByteArrayInputStream, or any other stream that provides the serialized data.

            FileInputStream fileIn = new FileInputStream("serializedObject.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);

Use the readObject() method of the ObjectInputStream class to read the serialized object. This method returns an Object reference, so you'll need to cast it to the appropriate class.

            MyClass deserializedObject = (MyClass) in.readObject();

Close the ObjectInputStream to release any system resources associated with it.

            in.close();

After these steps, you will have the deserialized object, and you can use it in your Java program as needed.

It's worth noting that deserialization can potentially be unsafe if you are deserializing data from an untrusted source. Malicious objects or code could be injected through a manipulated serialized form. Therefore, it's important to exercise caution when deserializing objects, especially when the serialized data comes from an untrusted or unknown source.
</details>
<details><summary>
	
## What do you do if only parts of the object have to be serialized?
</summary>
If you only want to serialize specific parts of an object in Java, you can make use of the transient keyword. The transient keyword allows you to exclude certain fields from the serialization process.

Here's a short example:

            import java.io.*;

            class MyClass implements Serializable {
                private int serializedField;
                private transient String nonSerializedField;
                
                public MyClass(int serializedField, String nonSerializedField) {
                    this.serializedField = serializedField;
                    this.nonSerializedField = nonSerializedField;
                }
                
                public int getSerializedField() {
                    return serializedField;
                }
                
                public String getNonSerializedField() {
                    return nonSerializedField;
                }
            }

            public class SerializationExample {
                public static void main(String[] args) {
                    MyClass obj = new MyClass(42, "Not serialized");
                    
                    try {
                        FileOutputStream fileOut = new FileOutputStream("serializedObject.ser");
                        ObjectOutputStream out = new ObjectOutputStream(fileOut);
                        out.writeObject(obj);
                        out.close();
                        fileOut.close();
                        System.out.println("Object serialized successfully.");
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }

In this example, the MyClass has two fields: serializedField and nonSerializedField. The serializedField will be serialized because it is not marked as transient, while the nonSerializedField will be excluded from serialization.

When you run the SerializationExample program, it will create a file named "serializedObject.ser" that contains the serialized form of the MyClass object. The file will only include the serialized value of the serializedField, and the nonSerializedField will not be present.

When you deserialize the object, the value of the nonSerializedField will be null because it was not included in the serialization process.
</details>
<details><summary>
	
## How do you serialize a hierarchy of objects?
</summary>
Objects of one class might contain objects of other classes. When serializing and de-serializing, we might
need to serialize and de-serialize entire object chain. All classes that need to be serialized have to
implement the Serializable interface. Otherwise, an exception is thrown. Look at the class below. An
object of class House contains an object of class Wall.

            class House implements Serializable {
                    public House(int number) {
                            super();
                            this.number = number;
                    }
                    Wall wall;
                    int number;
            }

            class Wall{
                    int length;
                    int breadth;
                    int color;
            }

House implements Serializable. However, Wall doesn't implement Serializable. When we try to serialize
an instance of House class, we get the following exception.

Output:
Exception in thread "main" java.io.NotSerializableException:
com.rithus.serialization.Wall
at java.io.ObjectOutputStream.writeObject0(Unknown Source)
at java.io.ObjectOutputStream.defaultWriteFields(Unknown Source)

This is because Wall is not serializable. Two solutions are possible.
1. Make Wall transient. Wall object will not be serialized. This causes the wall object state to be lost.
2. Make Wall implement Serializable. Wall object will also be serialized and the state of wall object
along with the house will be stored.

            class House implements Serializable {
                    public House(int number) {
                            super();
                            this.number = number;
                    }

                    transient Wall wall;
                    int number;
            }

            class Wall implements Serializable {
                    int length;
                    int breadth;
                    int color;
            }

With both these programs, earlier main method would run without throwing an exception.

If you try de-serializing, In Example2, state of wall object is retained whereas in Example1, state of wall
object is lost.
</details>
<details><summary>
	
## Are the values of static variables stored when an object is serialized?
</summary>
No, the values of static variables are not stored when an object is serialized in Java.

Static variables belong to the class itself rather than individual instances of the class. They are not considered part of the state of an object and are not serialized along with the object.

During the serialization process, only the instance variables (non-static fields) are serialized to preserve the state of the object. When the object is deserialized, the static variables will be initialized according to their default values or any explicit initialization in the class definition.

It's important to note that static variables are associated with the class and are shared among all instances of the class, so it wouldn't make sense to store their values on a per-object basis during serialization.
</details>