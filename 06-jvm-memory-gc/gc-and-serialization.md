<details><summary>
	
## [Easy] What is a Garbage Collection?
</summary>

Garbage collection in Java is the process by which Java programs perform automatic memory management. Java programs compile to bytecode that can be run on a Java Virtual Machine. When Java programs run on the JVM, objects are created on the heap, which is a portion of memory dedicated to the program. Eventually, some objects will no longer be needed. The garbage collector finds these unused objects and deletes them to free up memory.

**Example:**

```java
void process() {
    User temp = new User("Asha");   // object created on the heap
    temp = null;                    // no references left -> eligible for GC
}
// More detail: jvm-memory-and-performance.md
```

</details>

<details><summary>
	
## [Easy] Can you explain the Garbage Collection with an example?
</summary>

```java
void method() {
	Calendar calendar = new GregorianCalendar(2000, 10, 30);
	System.out.println(calendar);
}
```

The `GregorianCalendar` object is created on the **heap**; the reference `calendar` lives in the method's **stack frame**. When the method returns, the frame is popped and no reference to the object remains, so the object becomes **unreachable** and therefore **eligible** for garbage collection.

It is not removed at that exact moment: the GC reclaims it at some later point when it runs (often during the next young-generation collection, since most short-lived objects die young). An object is eligible once it can't be reached from any GC root (thread stacks, static fields, JNI references).

</details>

<details><summary>
	
## [Easy] What is Serialization?
</summary>

Serialization is the process of converting an object into a format that can be stored or transmitted and later reconstructed to its original form. In the context of Java programming, serialization refers to the mechanism provided by the Java platform to convert objects into a byte stream and vice versa.

**Example:**

```java
public class Session implements Serializable {
    private static final long serialVersionUID = 1L;   // version control for the class
    private String userId;
    private transient String password;                  // skipped during serialization
}

try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("session.ser"))) {
    out.writeObject(new Session());
}
// In modern services, JSON (Jackson) or Protobuf is preferred over Java serialization,
// which is slow and a known security risk when deserializing untrusted data.
```

</details>

<details><summary>
	
## [Easy] How do you serialize an object using Serializable interface?
</summary>

1. Make the class implement **`java.io.Serializable`** (a marker interface with no methods). Every field must itself be serializable, or be marked `transient`.
2. Declare a **`serialVersionUID`** so changes to the class don't silently break deserialization of old data.
3. Write the object with **`ObjectOutputStream.writeObject()`**, using try-with-resources so streams are closed.

```java
class Student implements Serializable {
	private static final long serialVersionUID = 1L;
	private String name;
	private int age;
	private transient String password;     // not written

	Student(String name, int age) { this.name = name; this.age = age; }
}

try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("student.ser"))) {
	out.writeObject(new Student("John", 20));
}
```

If any non-transient field's class isn't `Serializable`, you get `NotSerializableException` at runtime.

In modern backend services, prefer **JSON (Jackson) or Protobuf/Avro** for data you store or send over the network. Java's built-in serialization is slow, tightly coupled to class structure, and deserializing untrusted data is a known security risk.

</details>

<details><summary>
	
## [Easy] How do you de-serialize in Java?
</summary>

Read the bytes back with `ObjectInputStream.readObject()` and cast the result. The class must be on the classpath, and its `serialVersionUID` must match the one that was serialized (otherwise `InvalidClassException`).

```java
try (ObjectInputStream in = new ObjectInputStream(new FileInputStream("student.ser"))) {
	Student s = (Student) in.readObject();     // may throw ClassNotFoundException
}
```

What happens during deserialization:
- The object is created **without calling its constructor**; fields are filled from the stream.
- `transient` fields get default values (`null`, `0`, `false`).
- Static fields are not restored; they keep whatever value the class has in the current JVM.

**Security:** never deserialize data from untrusted sources with Java serialization (it has led to remote code execution vulnerabilities). If you must, use an `ObjectInputFilter` (Java 9+) to allow only expected classes.

</details>

<details><summary>
	
## [Easy] What do you do if only parts of the object have to be serialized?
</summary>

If you only want to serialize specific parts of an object in Java, you can make use of the transient keyword. The transient keyword allows you to exclude certain fields from the serialization process.

Here's a short example:

```java
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
```

In this example, the MyClass has two fields: serializedField and nonSerializedField. The serializedField will be serialized because it is not marked as transient, while the nonSerializedField will be excluded from serialization.

When you run the SerializationExample program, it will create a file named "serializedObject.ser" that contains the serialized form of the MyClass object. The file will only include the serialized value of the serializedField, and the nonSerializedField will not be present.

When you deserialize the object, the value of the nonSerializedField will be null because it was not included in the serialization process.
</details>

<details><summary>
	
## [Medium] When is the Garbage Collection run?
</summary>

The JVM decides; you can't schedule it precisely. Common triggers in HotSpot:

- **Allocation failure in the young generation:** Eden is full when a new object needs space, so a minor (young) GC runs. This is by far the most common trigger.
- **Old generation filling up:** collectors start concurrent or mixed collections when occupancy crosses a threshold (G1's *Initiating Heap Occupancy Percent*, 45% by default).
- **Humongous / large allocations** that don't fit (G1).
- **Metaspace** reaching its threshold (class metadata).
- **Explicit `System.gc()`** – only a request; it can be disabled with `-XX:+DisableExplicitGC`.
- **Periodic GC** if configured (e.g. `-XX:G1PeriodicGCInterval`) to return memory when the app is idle.

Watch GC behaviour with `-Xlog:gc*` or JVM metrics (Micrometer/Prometheus) rather than guessing.

**Example:**

```java
System.gc();   // only a hint - the JVM may ignore it; don't rely on it in production

// See when GC actually runs:
// java -Xlog:gc -jar app.jar
// [0.512s][info][gc] GC(0) Pause Young (Normal) (G1 Evacuation Pause) 24M->4M(256M) 3.1ms
```

</details>

<details><summary>
	
## [Medium] What are the best practices for Garbage Collection?
</summary>

- **Don't call `System.gc()`** in application code; it's only a hint and can cause unnecessary full collections.
- **Don't use `finalize()`.** It was deprecated in Java 9 and marked for removal in Java 18; it runs unpredictably (or never) and slows GC. Use try-with-resources, or `java.lang.ref.Cleaner` for native resources.
- When memory is full and nothing can be freed, the JVM throws **`OutOfMemoryError`** (an Error, not an "OutOfMemoryException").
- **Reduce allocation pressure:** avoid needless temporary objects in hot paths, use primitives instead of wrappers in large loops, reuse buffers carefully.
- **Avoid memory leaks:** bound caches, remove `ThreadLocal` values, unregister listeners, close resources.
- **Size the heap for the environment:** `-Xms`/`-Xmx`, or `-XX:MaxRAMPercentage=75` in containers.
- **Choose the collector for your goal:** G1 (default, balanced), ZGC for very low pauses, Parallel for throughput.
- **Measure** with GC logs, JFR and heap dumps before tuning flags.

**Example:**

```java
// 1. Don't create unnecessary objects in hot loops
StringBuilder sb = new StringBuilder();
for (String s : items) sb.append(s);          // instead of s1 + s2 + ... in a loop

// 2. Bound caches so they don't grow forever
Map<String, Data> cache = new LinkedHashMap<>(16, 0.75f, true) {
    protected boolean removeEldestEntry(Map.Entry<String, Data> e) { return size() > 10_000; }
};

// 3. Close resources (try-with-resources), remove ThreadLocals, unregister listeners
// 4. Size the heap for containers: -XX:MaxRAMPercentage=75
```

</details>

<details><summary>
	
## [Medium] What are Initialization Blocks?
</summary>

Initialization blocks are unnamed blocks of code in a class body.

**Static initialization block** – `static { ... }` – runs **once**, when the class is **initialised** (on its first active use: first instance created, static method called, or static field accessed – not merely when it's loaded). Used to set up static state.

**Instance initialization block** – `{ ... }` – runs **every time an object is created**, after the superclass constructor (`super()`) completes and **before the rest of the constructor body**. The compiler effectively copies it into every constructor. Useful for logic shared by all constructors.

```java
public class MyClass {
	private static final Map<String, Integer> CODES;
	private final List<String> items;

	static {                                   // once per class
		CODES = Map.of("A", 1, "B", 2);
		System.out.println("static block");
	}

	{                                          // once per object, before constructor body
		items = new ArrayList<>();
		System.out.println("instance block");
	}

	public MyClass() { System.out.println("constructor"); }
}

new MyClass(); new MyClass();
// static block
// instance block
// constructor
// instance block
// constructor
```

Multiple blocks of the same kind run top to bottom, interleaved with field initialisers in source order. Order on first creation: static fields/blocks (parent then child) → for each object: parent constructor chain → instance fields/blocks → constructor body.

</details>

<details><summary>
	
## [Medium] How do you serialize a hierarchy of objects?
</summary>

Objects of one class might contain objects of other classes. When serializing and de-serializing, we might
need to serialize and de-serialize entire object chain. All classes that need to be serialized have to
implement the Serializable interface. Otherwise, an exception is thrown. Look at the class below. An
object of class House contains an object of class Wall.

```java
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
```

House implements Serializable. However, Wall doesn't implement Serializable. When we try to serialize
an instance of House class, we get the following exception.

Output:
Exception in thread "main" java.io.NotSerializableException:
com.rithus.serialization.Wall
at java.io.ObjectOutputStream.writeObject0(Unknown Source)
at java.io.ObjectOutputStream.defaultWriteFields(Unknown Source)

This is because Wall is not serializable. Two solutions are possible.
1. Make Wall transient. Wall objects will not be serialized. This causes the wall object state to be lost.
2. Make Wall implement Serializable. The wall object will also be serialized and the state of the wall object
along with the house will be stored.

```java
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
```

With both these programs, the earlier main method would run without throwing an exception.

If you try de-serializing, In Example 2, the state of the wall object is retained whereas in Example 1, the state of the wall
object is lost.
</details>

<details><summary>
	
## [Medium] Are the values of static variables stored when an object is serialized?
</summary>

No. Serialization saves the state of an **object**, and static variables belong to the **class**, so they are not written to the stream.

After deserialization, the object sees whatever value the static variable **currently has in that JVM** (from class initialisation and any later changes). It is not reset to a default value by deserialization, and it isn't restored to the value it had when the object was saved.

`transient` instance fields are also skipped, but those do come back with default values (`null`/`0`/`false`).

**Example:**

```java
class Config implements Serializable {
    static String env = "dev";       // belongs to the class, NOT serialized
    String name = "app";
}
// serialize a Config while env = "dev", then set Config.env = "prod" and deserialize:
// the object sees env = "prod" (current class value), name = "app" (restored)
```

</details>

<details><summary>

## [Hard] Are the constructors in an object invoked when it is de-serialized?
</summary>

For a normal `Serializable` class: **its own constructor is not called**, and neither are the constructors of any serializable superclasses. The JVM allocates the object and fills fields from the stream.

But the **no-arg constructor of the first non-serializable superclass** *is* called (often just `Object()`), to initialise that superclass's fields. If that superclass has no accessible no-arg constructor, deserialization fails with `InvalidClassException`.

For **`Externalizable`** classes it's different: the class's **public no-arg constructor is called first**, and then `readExternal()` fills in the fields. That's why `Externalizable` classes must have a public no-arg constructor.

Instance initialisers and field initialisers of the serializable class also don't run, so `transient` fields end up with default values unless you restore them in a `readObject()` method.

**Example:**

```java
class Parent { Parent() { System.out.println("Parent()"); } }          // not Serializable
class Child extends Parent implements Serializable {
    Child() { System.out.println("Child()"); }
}
// On deserializing a Child:
//   Child() is NOT called (fields restored from the stream)
//   Parent() IS called, because Parent is not Serializable
```

</details>
