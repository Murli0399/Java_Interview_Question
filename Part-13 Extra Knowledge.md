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

## What is the stored procedure in JDBC?
</summary>

A stored procedure is a set of SQL statements that are stored together as a single block of code in a database. Stored procedures can be reused multiple times without having to write the queries again. They can provide multiple output values and accept input as well as output parameters.

Stored procedures are executed on the server side and perform a set of actions, before returning the results to the client side. They consist of database access commands (SQL), control statements, and data structures that manipulate the data obtained from the database.

Stored procedures are accessible by all applications that can access relational databases, including Java, Python, and PHP. The procedure code is defined in a Java class method and stored in the database. This is executed using SQL.
</details>
<details><summary>

## What is a connection pool? How is it used to improve performance in database applications?
</summary>

A connection pool is a cache of database connections that can be reused when a database is accessed. Connection pooling is a technique that can improve the performance of database applications.

Connection pooling works by:

- Creating a pool of open connections.
- Passing these connections from database operation to database operation as needed.
- Avoiding the overhead of creating a new database connection every time an application or server object requires access to a database.
- Conserving application resources for future requests.
- Allowing a database to scale effectively as the data stored there and the number of clients accessing it grow.

Connection pooling can be implemented by deploying an intermediary queuing system to manage and recycle database connections. The JDBC Connection Pool Assistant can help you create and deploy a connection pool.
</details>
<details><summary>

## Handling and fixing 'Out of Memory' exceptions?
</summary>

Out of Memory exceptions, or OutOfMemoryError, are runtime errors in Java that occur when the Java Virtual Machine (JVM) cannot allocate an object due to insufficient space in the Java heap. The Java Garbage Collector (GC) cannot free up the space required for a new object.

Here are some ways to fix OutOfMemoryError:
- Increase the size of the Metaspace by adding the -XX:MaxMetaspaceSize flag to the startup parameters of your Java application.
- Increase the heap size of the Perm space by using the JVM option "-XX: MaxPermSize".
- Restructure your code to use less memory. For example, you could stream the output instead of holding the whole thing in memory.
- Give the JVM more memory with the -Xmx option.
- Keep data access to a minimum. Let the database do the hard work for you (querying) and only bring back the data you need to the JVM.

You can look in the atlassian-confluence.log to see which type of OutOfMemory Error you're receiving.
</details>
<details><summary>

## What is the difference between a ClassCastException and a ClassNotFoundException in Java?
</summary>

The main difference between a ClassCastException and a ClassNotFoundException in Java is that a ClassCastException is thrown when an object is not of the expected type, while a ClassNotFoundException is thrown when a class cannot be found.

A ClassCastException is a checked exception, which means that it must be caught or declared in the method signature. It is thrown when an object is cast to a type that it is not compatible with. For example, the following code will throw a ClassCastException:
```
Object o = new Integer(10);
String s = (String) o; // This will throw a ClassCastException
```

In this example, the object o is an Integer, but it is being cast to a String. This is not allowed, because an Integer cannot be converted to a String.

A ClassNotFoundException is an unchecked exception, which means that it does not need to be caught or declared in the method signature. It is thrown when a class cannot be found. For example, the following code will throw a ClassNotFoundException:
```
try {
  Class<?> c = Class.forName("java.lang.String");
} catch (ClassNotFoundException e) {
  // This will be executed if the class cannot be found
}
```

In this example, the class java.lang.String is being looked up, but it cannot be found. This is because the class is not in the classpath.

In general, ClassCastExceptions are more common than ClassNotFoundExceptions. This is because ClassCastExceptions can be caused by a variety of errors, such as misspelling a class name or using an incompatible version of a class. ClassNotFoundExceptions are typically only caused by missing classes.
</details>
<details><summary>

## What is JSON? How is it utilized?
</summary>

JSON (JavaScript Object Notation) is a text-based format for storing and transporting data. It is often used when data is sent from a server to a web page or browser. JSON is a lightweight format that is easy to read and write. It is also easy for software to parse and generate.

JSON is used as an alternative to Extensible Markup Language (XML). It was introduced in the early 2000s as part of JavaScript. Today, 
JSON is the universal standard of data exchange.

JSON is used for:
- Exchanging data between web clients and web servers
- Transmitting data in web applications
- Serializing structured data and exchanging it over a network

JSON is a language-independent data format that supports almost every kind of language, framework, and library.
</details>
<details><summary>

## What is the usage of the PATH variable in an operating system? How is it utilized, when would you like to update it?
</summary>

The PATH variable is an environment variable that contains a list of directories the operating system checks before running a command. The PATH variable makes it easy to run commonly used programs located in their own folders. Updating the PATH variable allows you to run any executables found in the directories mentioned in PATH from any directory without typing the absolute file path.

The PATH variable is the most frequently used environment variable. It is an important security control. The default systemwide PATH value is specified in the /etc/profile file. Each user normally has a PATH value in the user's $HOME/. profile file.

If used unwisely, the value of the PATH variable can slow down the operating system by searching too many locations, or invalid locations.
</details>
<details><summary>

## What configurations do you need to make in web.xml to deploy a servlet in a web application?
</summary>

To configure a servlet in web.xml, you need to:
- Define the servlet name and class name using the <servlet> element
- Map the servlet to a URL or URL pattern
- Add initializations and security roles for the servlet
- Define mappings between URL paths and the servlets that handle requests with those paths

The web server uses this configuration to identify the servlet to handle a given request. For example, the doGet() method for HTTP GET requests.

The web.xml file is located in the WEB-INF directory. It does not represent the entire configuration that is available for the web application. Other servlets, filters, and listeners can be defined using programmatic configurations, annotations, and web fragments.
</details>
<details><summary>

## Explain how the session is utilized for security implementation. Please explain who creates the session and how is session information exchanged between the browser and server.
</summary>

A session is a unique identifier that identifies a user's session on a website or application. A session is created when a user logs in to a website or app. The server creates a session ID, or session token, which is a randomly generated string. The session ID is attached to the response and is valid for a period of time.

The session management process is as follows:
1. The user enters login credentials and submits.
2. The client sends a request with the login credentials.
3. The server receives the request and checks if the login credentials are valid.
4. If valid, the server creates a session and attaches the session ID to the response.

The session ID is used to identify if the request came from the authenticated user without needing re-authentication.

Session management involves sharing secrets with authenticated users. Secure cryptographic network communications are essential to maintaining session management security.
</details>
<details><summary>

## What is the difference between a database view and a table in a database?
</summary>

A database view is a virtual table that is extracted from a database. A table is an actual table that exists in physical locations. A view is a subset of a database and is based on a query that runs on one or more database tables. A view is used to query certain data present in different tables. A table is an independent data object that stores the data of a database.

Here are some differences between a view and a table:
- A view depends on the table.
- A view is a virtual table, it does not occupy storage space.
- A table is structured with columns and rows.
- A table is an independent data object.
- A table holds the basic user data and instances of defined objects.
- A view is used to query certain data present in different tables.
</details>
<details><summary>

## What is meant by an entity-relationship (E-R) model? Explain the terms Entity, Entity Type, and Entity Set in
</summary>

An entity-relationship (ER) model is a high-level data model that describes how entities relate to each other in a specific domain. The ER model is used to design a database by identifying entities and the relationships between them. The ER model is represented by an ER diagram, which is a blueprint for a database.

The ER model is based on two concepts:
- Entities: Tables that contain specific information
- Relationships: Associations or interactions between entities

The ER model is commonly used in software engineering to represent things a business needs to remember to perform business processes. It can also be used to teach students the basics of database structure.

An entity type in an ER diagram is defined by a name and a set of attributes. For example, a student entity type might have the attributes roll number, student name, age, and mobile number.
</details>
<details><summary>

## What is a database trigger? How is it used to enforce business rules?
</summary>

A database trigger is a set of procedural codes that is automatically executed in response to a specific event in a database. Triggers are used to enforce business rules, maintain data integrity, and automate certain actions within a database.

Triggers can be defined to run instead of or after DML (Data Manipulation Language) actions such as INSERT, UPDATE, and DELETE.

Triggers can also be defined to run after system events such as a login or logout.

Triggers are an important method for enforcing business rules because they automatically perform an action after a change is made to the database.
</details>
<details><summary>

## What all commands in Unix are you aware of? Please explain their usage.
</summary>

Here are some Unix commands and their usage:
- cat: Creates and displays short files
- chmod: Changes permissions
- cd: Changes directory
- cp: Copies files
- date: Displays the system date and time
- ls: Lists the contents of a directory
- man: Gets documentation for any command
- ftp: Connects to a remote machine to download or upload files
- grep: Searches a file

Other Unix commands include:

mv, rm, mkdir, rmdir, ps, kill.

When writing Unix commands, you can follow these general rules:
- Enter commands in lowercase
- Options are often single letters prefixed with a dash (-)
- Options are set off by any number of spaces or tabs
</details>
<details><summary>

## What is shell scripting? What purpose is it used for?
</summary>

Shell scripting is a computer program that is used to automate repetitive tasks. It is often used by system administrators to save time and increase accuracy. Shell scripts can be used for tasks such as:
- Backing up files
- Monitoring system resources
- Managing user accounts
- Creating command tools
- Manipulating files
- Running programs
- Linking programs together
- Completing batches

Shell scripts are written as a sequence of commands in a file. The file is made up of ASCII text, also called plain text. You can use a text editor to create shell scripts. Some good command line text editors include vim, emacs, and nano.

Shell scripts are easier to write and debug than other programming languages like C or C++. You can transfer the shell script to other UNIX and similar operating systems and execute it.
</details>
<details><summary>

## How does your computer know what path to take to reach the external server
</summary>

When a computer tries to reach a server, it uses a Domain Name System (DNS) server to translate the URL into an IP address. This process is called DNS resolution. The DNS server then provides the IP address to reach the server.

The router uses a forwarding table to determine the best path to reach the destination device. The router consults the routing table to find the IP address of the destination device. The router then uses the forwarding table to pick the next path based on the destination IP address.

You can use Traceroute to trace the path between your computer and a target destination.
</details>
<details><summary>

## Explain how you can read fields sent in a request from the browser using a servlet.
</summary>

Servlets are classes in a Java web application that handle requests and responses from client browsers. When a form is submitted, the servlet's doPost() method is invoked. The field values are submitted to the servlet as parameters in the HTTP request. You can use the following methods on the request object to get the parameter values: getParameter(, getParameterValues(, getParameterNames(.

The getParameter() method returns the value of a request parameter as a string. If there is no parameter, it returns null. You can use this method when the parameter has a single value.

The getParameterValues() method is used if the parameter appears more than once and returns multiple values. For example, a checkbox.

The getParameterNames() method is used if you want a complete list of all parameters in the current request.
</details>
<details><summary>

## What objects are implicitly available in JSP? Explain their usage
</summary>

JSP implicit objects are created automatically by the container during the translation of a JSP page to a servlet. These objects can be used directly in scriptlets without initializing or declaring them.

Here are some of the implicit objects in JSP:
- page: A synonym for "this", used to call methods defined by the translated servlet class
- pageContext: The context for the JSP page, which provides access to other objects
- servletContext: The context for the JSP page's servlet and any web components in the same application
- Exception: Allows the designated JSP to access exception data

Other implicit objects include: out, request, response, session, and application.

You can use these objects to get, set, and remove attributes in four scopes: page, request, session, and application.
</details>
<details><summary>

## Difference between hashmap and hashtable?
</summary>

HashMap and Hashtable are both data structures in Java that store key-value pairs. The main difference between them is that HashMap is not thread-safe, while Hashtable is thread-safe. This means that HashMap is faster for single-threaded tasks, but Hashtable is thread-safe and can be shared with many threads.

Here are some other differences between HashMap and Hashtable:
- HashMap allows one null key and several null values, while Hashtable doesn't allow any null keys or values.
- HashMap is non-synchronized, making it faster for single-threaded tasks, while Hashtable is inherently synchronized.
- HashMap uses Iterator to iterate over values, whereas Hashtable has Enumerator for the same.
</details>
<details><summary>

## What is constructor chaining?
</summary>

Constructor chaining is the process of calling one constructor from another constructor in the same class. It is used to initialize the object with some default values. Constructor chaining can be done in two ways:

- Using the this() keyword to call the constructor in the same class.
- Using the super() keyword to call the constructor in the parent class.

The following is an example of constructor chaining using the this() keyword:
```
public class Person {

    private String name;
    private int age;

    public Person(String name) {
        this.name = name;
    }

    public Person(String name, int age) {
        this(name); // Chaining to the constructor with one parameter
        this.age = age;
    }

}
```
The following is an example of constructor chaining using the super() keyword:
```
public class Car extends Vehicle {

    private String make;
    private String model;

    public Car(String make, String model) {
        super(make, model); // Chaining to the constructor in the parent class
        this.make = make;
        this.model = model;
    }

}
```
Constructor chaining is a powerful feature that can help to make your code more concise and efficient.
</details>
<details><summary>

## 
</summary>


</details>
<details><summary>

## 
</summary>


</details>
<details><summary>

## 
</summary>


</details>

