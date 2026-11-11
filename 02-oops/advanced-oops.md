<details><summary>
	
## [Easy] What is Polymorphism?
</summary>

Polymorphism in Java is the ability of an object to take on many forms. It allows a reference variable of a superclass to represent objects of its subclasses. In other words, it enables objects of different classes to be treated as objects of a common superclass during runtime.

There are two types of polymorphism in Java:

### Compile-time Polymorphism (Method Overloading):

Method overloading allows multiple methods in the same class with the same name but different parameter lists.
The appropriate method is chosen at compile time based on the arguments passed to the method.
	
### Runtime Polymorphism (Method Overriding):

Method overriding occurs when a subclass provides its own implementation of a method that is already defined in its superclass.
The method to be executed is determined at runtime based on the actual object being referred to by the reference variable.
Polymorphism is achieved through inheritance, where subclasses inherit the properties and behaviors of their superclass. It allows for code reuse, flexibility, and the ability to write generic code that can operate on objects of different types.

```java
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
```

</details>

<details><summary>
	
## [Easy] What is the use of instanceof Operator in Java?
</summary>

The instanceof operator in Java is used to test if an object is an instance of a particular class or implements a specific interface. It allows you to check the type of an object at runtime.

The instanceof operator has the following syntax:

    object instanceof Class

Here, object is the reference variable whose type is being checked, and Class is the class or interface that is being tested against. The operator returns a boolean value: true if the object is an instance of the specified class or implements the specified interface, and false otherwise.

The instanceof operator is commonly used in scenarios such as:

Type checking: You can use instanceof to determine the actual type of an object before performing certain operations or casting it to a specific type. This helps avoid potential type casting errors at runtime.

Polymorphism and inheritance: instanceof can be used to determine if an object is an instance of a specific subclass or superclass. This allows you to apply different behaviors or logic based on the actual type of the object.

Here's an example that demonstrates the use of the instanceof operator:

```java
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
```

</details>

<details><summary>
	
## [Easy] What is Coupling?
</summary>

Coupling in Java refers to the degree of dependency or interconnectedness between classes or components within a software system. It measures how closely one class or component relies on or interacts with another.

In general, low coupling is desirable as it promotes better software design, modularity, and maintainability. High coupling, on the other hand, can lead to code that is difficult to understand, modify, and reuse.

- **Tight coupling** - When an object creates the object to be used, then it is a tight coupling situation. As the main object creates the object itself, this object can not be changed from outside world easily marked it as tightly coupled objects.

        
```java
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
```


- **Loose coupling** - When an object gets the object to be used from the outside, then it is a loose coupling situation. As the main object is merely using the object, this object can be changed from the outside world easily marked it as loosely coupled objects.

```java
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
```

Reducing coupling is typically achieved through good software design practices, such as following the principles of encapsulation, abstraction, and dependency inversion. Using design patterns, interfaces, and dependency injection can also help to decouple components and promote modular and reusable code.

By minimizing coupling, you can improve code maintainability, reusability, testability, and overall software quality. It allows for easier understanding and modification of individual components without affecting the entire system.
</details>

<details><summary>
	
## [Easy] What is Cohesion?
</summary>

Cohesion in Java is the principle of Object-Oriented programming. Cohesion is closely related to ensuring that the purpose for which a class is getting created in Java is well-focused and single. In other words, the more closely related stuff is grouped in a class, the higher will be the cohesiveness.

**Example Problem** - Example class below is downloading from internet, parsing data and storing data 
to database. Theresponsibilities of this class are not really related. This is 
not cohesive class.

```java
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
```

**Solution** - This is a better way of approaching the problem. Different classes have their 
own responsibilities.

```java
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
```

</details>

<details><summary>
	
## [Easy] What is Encapsulation?
</summary>

Encapsulation in Java is a process of wrapping code and data together into a single unit, for example, a capsule which is mixed of several medicines.

We can create a fully encapsulated class in Java by making all the data members of the class private. Now we can use setter and getter methods to set and get the data in it.

The Java Bean class is the example of a fully encapsulated class.

### Advantage of Encapsulation in Java
- By providing only a setter or getter method, you can make the class read-only or write-only. In other words, you can skip the getter or setter methods.

- It provides you the control over the data. Suppose you want to set the value of id which should be greater than 100 only, you can write the logic inside the setter method. You can write the logic not to store the negative numbers in the setter methods.

- It is a way to achieve data hiding in Java because other class will not be able to access the data through the private data members.

- The encapsulate class is easy to test. So, it is better for unit testing.

- The standard IDE's are providing the facility to generate the getters and setters. So, it is easy and fast to create an encapsulated class in Java.

```java
    Approach 1
    // In this approach we create a public variable score. The main method directly
    accesses the score variable, updates it.

    public class CricketScorer {
            public int score;
    }

    // Let’s use the CricketScorer class.
    public static void main(String[] args) {
            CricketScorer scorer = new CricketScorer();
            scorer.score = scorer.score + 4;
    }

    Approach 2
    // In this approach, we make score as private and access value through get and set
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

    // Let’s use the CricketScorer class.

    public static void main(String[] args) {
            CricketScorer scorer = new CricketScorer();
            int score = scorer.getScore();
            scorer.setScore(score + 4);
    }


    Approach 3
    // In this approach - For better encapsulation, the logic of doing the four
    operation also is moved to the CricketScorer class.

    public class CricketScorer {
            private int score;
                    public void four() {
                            score += 4;
                    }
    }

    // Let’s use the CricketScorer class.
    public static void main(String[] args) {
            CricketScorer scorer = new CricketScorer();
            scorer.four();
    }
```

**Description** - In terms of encapsulation Approach 3 > Approach 2 > Approach 1. In Approach 3, 
the user of scorer class does not even know that there is a variable called 
score. Implementation of Scorer can change without changing other classes using 
Scorer.
</details>

<details><summary>
	
## [Medium] What is an Inner Class?
</summary>

An **inner class** is a non-static class declared inside another class. Each inner-class object is tied to an instance of the outer class and can access all of its members, including private fields and methods.

Types of nested classes in Java:
1. **Inner (member) class:** non-static, needs an outer instance.
2. **Static nested class:** no outer instance needed.
3. **Local class:** declared inside a method.
4. **Anonymous class:** declared and instantiated in one expression.

```java
class OuterClass {
	private String secret = "outer-data";

	public class InnerClass {
		void print() { System.out.println(secret); }   // can read outer's private field
	}
}

OuterClass outer = new OuterClass();
OuterClass.InnerClass inner = outer.new InnerClass();  // needs an outer instance
inner.print();
```

Benefits: logical grouping of classes used in one place, better encapsulation, and access to the outer object's state.

</details>

<details><summary>
	
## [Medium] What is a Static Inner Class?
</summary>

A **static nested class** is a class declared `static` inside another class. It behaves like a top-level class that is namespaced inside the outer class:

- It does **not** need an instance of the outer class: `new Outer.Nested()`.
- It can access the outer class's **static** members (even private ones), but **not instance** members directly.
- Common uses: builders (`HttpRequest.Builder`), helper types tightly tied to one class (`Map.Entry`), and avoiding a hidden reference to the outer object.

```java
class OuterClass {
	private static int counter = 0;
	private int instanceValue = 5;

	public static class StaticNestedClass {
		void show() {
			System.out.println(counter);          // OK: static member
			// System.out.println(instanceValue); // COMPILER ERROR: needs an OuterClass instance
		}
	}
}

OuterClass.StaticNestedClass nested = new OuterClass.StaticNestedClass();
```

Prefer static nested classes over inner classes unless you need access to the outer instance; a non-static inner class holds a reference to its outer object, which can cause memory leaks.

</details>

<details><summary>
	
## [Medium] Can you create an inner class inside a method?
</summary>

we can write a class within a method and this will be a local type. Like local variables, the scope of the inner class is restricted within the method.

A method-local inner class can be instantiated only within the method where the inner class is defined. 

```java
class OuterClass {
	public void exampleMethod() {
		class MethodLocalInnerClass {
			
		};
	}
}
```

</details>

<details><summary>
	
## [Medium] What is an Anonymous Class?
</summary>

An anonymous class is a class **without a name**, declared and instantiated in a single expression. It either extends a class or implements an interface, and is used once, typically to **override** a method on the spot.

```java
class Animal {
	void bark() { System.out.println("Animal Bark"); }
}

// 1. Implementing an interface
Comparator<String> reverse = new Comparator<String>() {
	@Override
	public int compare(String a, String b) { return b.compareTo(a); }
};
String[] array = { "Apple", "Cat", "Boy" };
Arrays.sort(array, reverse);
System.out.println(Arrays.toString(array));   // [Cat, Boy, Apple]

// 2. Extending a class
Animal animal = new Animal() {
	@Override
	void bark() { System.out.println("Subclass bark"); }
};
animal.bark();                                // Subclass bark
```

Since Java 8, a **lambda** replaces an anonymous class when the target is a functional interface: `Comparator<String> reverse = (a, b) -> b.compareTo(a);`. Anonymous classes are still needed to extend a class, implement an interface with several methods, or hold state.

</details>