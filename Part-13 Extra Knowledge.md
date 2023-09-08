<details><summary>

## Difference between API and REST API?
</summary>
An API (Application Programming Interface) is a set of rules that define how applications or devices can connect to and communicate with each other. A REST API is a specific type of API that adheres to the constraints of the REST architectural style. REST stands for Representational State Transfer. REST is a style of web architecture that governs the behavior of clients and servers. REST APIs use HTTP requests to interact with data. Traditional APIs can use a variety of protocols.
REST APIs are also known as RESTful APIs. When a client requests a resource using a REST API, the server transfers back the current state of the resource in a standardized representation.
</details>
<details><summary>

## What is domain vs. endpoint in API?
</summary>
A domain is a library of common components, such as parameters, responses, and data models, that are used across multiple API definitions. An endpoint is a component of an API. It's a specific location within an API that accepts requests and sends back responses.
Endpoints are the locations of the resources, and the API uses endpoint URLs to retrieve the requested resources. For example, assuming the base URL of https://api.example.com/v1, the /users endpoint refers to https://api.example.com/v1/users.
APIs work by sending requests for information from a web application or web server and receiving a response.
</details>
<details><summary>

## Difference between Http and Https?
</summary>

HTTP (Hypertext Transfer Protocol) is the primary protocol for transmitting information across the internet. HTTPS (Hypertext Transfer Protocol Secure) is a more secure version of HTTP. The main difference between the two is that HTTPS uses encryption to protect information as it is sent between clients and servers. HTTPS encrypts data entered into a user's device and data going from the website to the browser. This makes it difficult for anyone to intercept information like passwords or credit card numbers.

Here are some other differences between HTTP and HTTPS:
- HTTP sends data over port 80, while HTTPS uses port 443.
- HTTP operates at the application layer, while HTTPS operates at the transport layer.
- HTTP transfers data in plain text, while HTTPS transfers data in cipher text.
- HTTP is faster than HTTPS because HTTPS consumes computation power to encrypt the communication channel.

HTTPS requires an SSL certificate and a CA signature, while HTTP does not require SSL certificates.
</details>
<details><summary>

## What is reflection API in Java?
</summary>
The Java Reflection API is a set of classes and interfaces that allows Java code to examine or modify the runtime behavior of a class at run time. The java.lang.Class class provides many methods that can be used to get metadata, and examine and change the run time behavior of a class. The java.lang and java.lang.reflect packages provide classes for Java reflection.

The Reflection API is mainly used in:
- IDE (Integrated Development Environment) e.g., Eclipse, MyEclipse, NetBeans, etc.
- Debugger
- Test Tools etc.

Here are some examples of how the Reflection API can be used:
- To get information about the fields, methods, and constructors of a class.
- To create instances of classes at runtime.
- To invoke methods at runtime.
- To get and set the values of fields at runtime.
- To override the access control restrictions on classes and members.

The Reflection API is a powerful tool that can be used to do things that would not be possible without it. However, it is important to use it carefully, as it can also be used to do things that could have unintended consequences.
</details>
<details><summary>

## Where is the Java Reflection API used in the Spring Framework?
</summary>
The Java Reflection API is used in the Spring Framework in a number of places, including:

- To create Spring beans at runtime.
- To inject dependencies into Spring Beans.
- To resolve the type of a Spring bean at runtime.
- To invoke methods on Spring beans.
- To get and set the values of fields on Spring beans.
- To override the access control restrictions on Spring beans.


The use of the Java Reflection API in the Spring Framework allows for a greater degree of flexibility and extensibility than would be possible without it. For example, it allows Spring beans to be created at runtime, even if the classes for those beans are not known at compile time. This can be useful in situations where the Spring beans are dynamically generated or loaded from a database.


The use of the Java Reflection API in the Spring Framework also makes it possible to inject dependencies into Spring beans that are not known at compile time. This can be useful in situations where the dependencies are provided by a third-party library or are dynamically generated.


Overall, the use of the Java Reflection API in the Spring Framework makes it a more powerful and flexible framework than would be possible without it.
</details>
<details><summary>

## What is the difference between authentication and authorization in api?
</summary>

Authentication and authorization are two different security functions. Authentication verifies a user's identity, while authorization determines what resources a user can access.

Authentication is the process of verifying a user's identity before granting access to an API. Authorization is the process of determining what resources a user can access.

For example, when you go through security at an airport, you show your ID to authenticate your identity. Authorization is like an airline determining which people can come on board.

Authentication and authorization are often used interchangeably, but they are two separate functions.
</details>
<details><summary>

## Difference between Abstract class vs. interface?
</summary>

Abstract classes and interfaces are both used for abstraction in object-oriented programming. The main difference between the two is that abstract classes can have state, while interfaces cannot. Abstract classes are used to define default behavior for subclasses. Interfaces are used to define behavior that can be implemented by multiple unrelated classes.

Here are some other differences between abstract classes and interfaces:

- Abstract classes can have abstract and non-abstract methods, while interfaces can only have abstract, static, and default methods.
- Abstract classes can extend one abstract class and implement multiple interfaces, while interfaces can only extend other interfaces.
- Abstract classes have no restrictions on field and method modifiers, while in an interface, all are public by default.
- Abstract classes can have instance and static initialization blocks, while interfaces cannot.
- Abstract classes can be used to provide a base for a hierarchy of classes or provide a common implementation. Interfaces can be used to define a contract behavior.
</details>
<details><summary>

## Difference between heap and stack memory?
</summary>

In Java, heap and stack are two different types of memory that are used to store data. The heap is used to store objects, while the stack is used to store local variables and method call information.

The heap is a large, unstructured area of memory that can be used to store any type of object. Objects are created on the heap by the new keyword. The garbage collector is responsible for managing the heap and removing objects that are no longer needed.

The stack is a small, fixed-size area of memory that is used to store local variables and method call information. Local variables are variables that are declared within a method. Method call information is used to keep track of the current method call and the methods that have been called before it.

The stack is used in a last-in, first-out (LIFO) manner. This means that the last variable that was declared is the first variable that is removed. The stack is also used to store the return address of a method call. The return address is the location of the code that will be executed after the method call returns.

The heap and stack are two important parts of the Java memory model. They work together to provide a safe and efficient way to store data.
</details>
<details><summary>

## 
</summary>


</details>
