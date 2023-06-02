<details><summary>

## Why is Exception Handling important?
</summary>
Exception handling is crucial in Java (and in programming in general) for several reasons:

- **Error management** Exception handling allows you to handle errors and exceptional situations that may occur during the execution of a program. Instead of abruptly terminating the program, you can gracefully handle these errors and take appropriate actions. This helps in maintaining the stability and reliability of the program.

- **Program flow control** With exception handling, you can control the flow of your program when an exceptional situation arises. By catching and handling exceptions, you can decide how your program should proceed in such cases. It provides a mechanism to recover from errors and continue the execution of the program, rather than crashing or terminating unexpectedly.

- **Debugging and troubleshooting** Exception handling aids in debugging and troubleshooting code. When an exception is thrown, it provides valuable information about the cause of the error, including the stack trace, error message, and the line of code where the exception occurred. This information helps developers identify and fix the problem more efficiently.

- **Robustness and stability** By handling exceptions, you can make your code more robust and resilient. Instead of letting errors propagate and potentially causing a system failure, you can catch and handle exceptions at appropriate levels of your code. This allows you to handle errors gracefully and ensure the stability of your program.

- **User-friendly experience** Exception handling enables you to provide meaningful error messages and handle errors in a user-friendly manner. Instead of showing cryptic error messages to users, you can catch exceptions, display custom error messages, and guide users on how to resolve or recover from the error.

- **Code maintainability** Exception handling promotes code maintainability by separating the normal code flow from the error-handling code. By encapsulating error-handling logic in exception handlers, you can keep the main code clean and focused on its primary functionality. This separation enhances code readability and maintainability.

In summary, exception handling is essential in Java because it allows you to manage errors, control program flow, debug code, ensure stability, provide a better user experience, and maintain code quality. It is a fundamental aspect of writing robust and reliable software.
</details>
<details><summary>

## What design pattern is used to implement Exception handling Features in most languages?
</summary>
In most programming languages, including Java, exception handling is typically implemented using the "Try-Catch" design pattern, which is based on the "Catching-Exceptions" pattern from the Gang of Four (GoF) design patterns.

The Try-Catch pattern allows you to enclose a section of code that might throw an exception within a "try" block. If an exception occurs within the try block, it is caught and handled by one or more "catch" blocks that follow the try block. Each catch block specifies the type of exception it can handle, and if an exception of that type occurs, the corresponding catch block is executed.

The basic structure of the Try-Catch pattern is as follows:

        try {
            // Code that might throw an exception
        } catch (ExceptionType1 exception1) {
            // Exception handling code for ExceptionType1
        } catch (ExceptionType2 exception2) {
            // Exception handling code for ExceptionType2
        } catch (ExceptionType3 exception3) {
            // Exception handling code for ExceptionType3
        } finally {
            // Code that is always executed, regardless of whether an exception occurred or not
        }

In this pattern, the try block contains the code that might throw an exception. The catch blocks handle specific types of exceptions, allowing you to provide appropriate error handling or recovery mechanisms. The finally block, which is optional, is used for code that needs to be executed regardless of whether an exception occurred or not (e.g., cleanup operations).

By using the Try-Catch pattern, you can control the flow of execution when exceptions occur, handle errors gracefully, and ensure that your program remains stable and robust.

It's important to note that while the Try-Catch pattern is widely used for exception handling, there are other patterns and techniques available, depending on the language and programming paradigm. However, the basic principles of encapsulating error-prone code in a try block and handling exceptions in catch blocks remain consistent across different languages.
</details>
<details><summary>

## What is the need for finally block?
</summary>
The "finally" block is an optional component of the Try-Catch-Finally pattern used in exception handling. It provides a mechanism to execute certain code regardless of whether an exception occurred or not. Here are the main reasons for using a "finally" block:

- **Cleanup operations** The "finally" block is often used to perform cleanup operations, such as closing resources (files, database connections, network connections) or releasing acquired locks. These operations are essential to ensure proper resource management and avoid resource leaks. By placing cleanup code in the "finally" block, you guarantee that it will be executed even if an exception is thrown or caught.

- **Guarantee execution** The "finally" block ensures that specific code is always executed, regardless of whether an exception occurred or not. This is useful in situations where certain actions must be performed, regardless of the success or failure of preceding code. For example, if you have allocated some resources in a try block, the "finally" block can be used to release those resources, ensuring they are not left in an inconsistent state.

- **Exception propagation** The "finally" block allows exceptions to be propagated after executing cleanup operations. If an exception is caught in a catch block and not re-thrown, the "finally" block can ensure that the exception is propagated further up the call stack. This is important when you need to handle exceptions at different levels of your code hierarchy while still ensuring that cleanup operations are performed.

- **Consistency and code readability** By placing code that must be executed in all circumstances in a "finally" block, you make your code more readable and maintainable. It clearly indicates the intention that certain operations are meant to be executed regardless of exceptions. This helps in writing robust and error-tolerant code.

To summarize, the "finally" block is used to execute code that should always run, regardless of exceptions. It is primarily used for cleanup operations, guaranteeing execution, propagating exceptions, and enhancing code readability. It plays a crucial role in ensuring the proper handling of resources and maintaining code consistency.
</details>
<details><summary>

## In what scenarios is code in finally not executed?
</summary>
The finally block is always get executed unless there is an abnormal program termination either resulting from a JVM crash or from a call to System.exit().

- A finally block is always get executed whether the exception has occurred or not.
- If an exception occurs like closing a file or DB connection, then the finally block is used to clean up the code.
- We cannot say the finally block is always executes because sometimes if any statement like System.exit() or some similar code is written into try block then program will automatically terminate and the finally block will not be executed in this case.
- A finally block will not execute due to other conditions like when JVM runs out of memory when our java process is killed forcefully from task manager or console when our machine shuts down due to power failure and deadlock condition in our try block.
</details>
<details><summary>

## Will finally be executed in the program below?
</summary>

        private static void method2() {
              Connection connection = new Connection();
              connection.open();
              try {
                  // LOGIC
                  String str = null;
                  str.toString();
                  return;
              } catch (Exception e) {
                  // NOT PRINTING EXCEPTION TRACE - BAD PRACTICE
                  System.out.println("Exception Handled - Method 2");
                  return;
              } finally {
                  connection.close();
              }
        }

In the provided code snippet, the finally block will be executed even when there is a return statement in the try or catch block.

When a return statement is encountered within the try or catch block, the execution flow immediately jumps to the finally block before actually returning from the method. This ensures that the code inside the finally block is executed before the method exits, regardless of whether an exception occurred or not.

In the given code, if an exception occurs within the try block, the catch block will be executed, printing the message "Exception Handled - Method 2". After that, the control flow will reach the finally block, where the connection.close() method will be invoked to perform necessary cleanup operations. Finally, the method will return.

If no exception occurs within the try block, the code inside the finally block will still be executed before the method returns. This allows for proper cleanup of resources (in this case, closing the connection) regardless of the success or failure of the logic inside the try block.

So, in conclusion, the finally block in the provided code snippet will be executed, even if there is a return statement in the try or catch block.
</details>
<details><summary>

## Is try without a catch is allowed?
</summary>
Yes, it is allowed to have a try block without a corresponding catch block. In such cases, it is required to have a finally block to handle the exception or perform necessary cleanup operations.

In some cases, you may have code that needs to be executed within a try block, but you don't need to catch or handle any specific exceptions. In such situations, you can use a finally block without any catch blocks. The code within the finally block will execute regardless of whether an exception occurred or not.

      try {
          // Code that doesn't throw a specific exception
      } finally {
          // Code that is always executed, regardless of whether an exception occurred or not
      }

Using a try block without a corresponding catch block can be useful in situations where you only need to ensure that certain code is executed, such as releasing resources or cleaning up operations. The finally block allows you to accomplish this even if an exception occurs within the try block.
</details>
<details><summary>

## Is try without catch and finally allowed?
</summary>
No. Below method would give a Compilation Error!! (End of try block)

        private static void method2() {
            Connection connection = new Connection();
            connection.open();
            try {
                // LOGIC
                String str = null;
                str.toString();
            }//COMPILER ERROR!!
        }

</details>
<details><summary>

## Can you explain the hierarchy of Exception Handling classes?
</summary>
Yes, I can explain the hierarchy of exception handling classes in Java.

In Java, the exception handling classes are organized in a hierarchy, with the root class being Throwable. The Throwable class serves as the base class for all exceptions and errors in Java. It has two main subclasses: Exception and Error.

Exception class: It represents exceptional conditions that can be caught and handled by the program. The Exception class is further subclassed into many specific exception types, such as RuntimeException, IOException, SQLException, etc. Exceptions in this hierarchy are meant to be caught and handled by the application code. They are typically caused by conditions that can be anticipated and recovered from.

Error class: It represents severe errors that are typically beyond the control of the application. Error objects are not usually caught or handled by application code. Examples of Error subclasses include OutOfMemoryError, StackOverflowError, VirtualMachineError, etc. These errors generally indicate critical problems that may not be recoverable, and they are usually not caught or handled explicitly in the application code.

Here's a simplified visual representation of the exception hierarchy:


                ┌───────────────┐
                │   Throwable   │
                └───────┬───────┘
                        │
             ┌──────────┴────────────┐
             │                       │
         ┌───┴───┐               ┌───┴─────┐
         │ Error │               │Exception│
         └───────┘               └─────────┘

The Exception class itself has many subclasses that provide more specific types of exceptions. For example, RuntimeException and its subclasses represent exceptions that are unchecked (do not need to be declared in the method signature or caught explicitly). IOException and its subclasses represent exceptions related to input/output operations. Similarly, other subclasses of Exception cover different categories of exceptional conditions.

It's important to understand this hierarchy when handling exceptions in Java. Catching and handling exceptions at appropriate levels in the hierarchy allows for more precise exception handling and error recovery in your code.
</details>
<details><summary>

## What is the difference between Error and Exception?
</summary>

- Error represents severe and typically unrecoverable conditions beyond the control of the application. They are usually unchecked exceptions and often lead to abnormal termination of the program.

- Exception represents exceptional conditions that can be caught and handled by the application code. They can be checked or unchecked exceptions. Checked exceptions must be declared or caught, while unchecked exceptions (subclasses of RuntimeException) do not require explicit handling.

Overall, Error indicates critical problems, while Exception is used for anticipated exceptional conditions that can be handled by the application code.
</details>
<details><summary>

## What is the difference between Checked Exceptions and Unchecked Exceptions?
</summary>
The main difference between checked exceptions and unchecked exceptions in Java lies in how they are handled and enforced by the compiler. Here are the key distinctions between these two types of exceptions:

### Checked Exceptions:

- Checked exceptions are exceptions that must be declared in the method signature or handled explicitly using try-catch blocks.
- They are typically used for exceptional conditions that can be reasonably anticipated and recovered from.
- Examples of checked exceptions in Java include IOException, SQLException, and ClassNotFoundException.
- Checked exceptions are enforced by the compiler, meaning that if a method throws a checked exception, the calling code must handle or declare that exception.
- This encourages developers to explicitly deal with potential exceptional situations, ensuring that they are aware of and address potential errors or exceptional conditions.

### Unchecked Exceptions:

- Unchecked exceptions are exceptions that do not need to be declared in the method signature or caught explicitly.
- They are typically caused by programming errors, such as null pointer access, arithmetic exceptions, or index out of bounds.
- Examples of unchecked exceptions in Java include NullPointerException, ArithmeticException, and ArrayIndexOutOfBoundsException.
- Unchecked exceptions are subclasses of RuntimeException or its subclasses.
- Unchecked exceptions are not enforced by the compiler, meaning that the calling code is not required to handle or declare these exceptions.
- This provides flexibility to developers, but it also places the responsibility on them to ensure proper error handling and validation within their code.

In summary, checked exceptions are checked by the compiler and must be declared or caught, while unchecked exceptions do not require explicit handling or declaration. Checked exceptions are typically used for anticipated exceptional conditions that can be recovered from, while unchecked exceptions are usually caused by programming errors and may require fixing the code itself.
</details>
<details><summary>

## How do you throw an exception from a method?
</summary>
In Java, you can throw an exception from a method using the throw keyword followed by an instance of an exception class. Here's how you can throw an exception from a method:

- **Declare the exception in the method signature** If the exception you want to throw is a checked exception, you need to declare it in the method signature using the throws keyword. This notifies the calling code that the method can throw this exception, and the caller must handle or declare it.

        public void someMethod() throws SomeException {
            // code that may throw SomeException
        }

- **Create an instance of the exception class** Within the method, when you encounter a condition that warrants an exception, create an instance of the appropriate exception class using the new keyword.

        public void someMethod() throws SomeException {
            if (someCondition) {
                SomeException exception = new SomeException("Exception message");
                throw exception;
            }
        }

You can also directly throw an instance of the exception class without assigning it to a variable:

        public void someMethod() throws SomeException {
            if (someCondition) {
                throw new SomeException("Exception message");
            }
        }

- **Propagate the exception** Once the throw statement is executed, the exception is thrown out of the method, propagating it to the calling code. The calling code can then catch the exception and handle it or propagate it further.
When throwing an exception, it's important to choose the appropriate exception class that accurately represents the exceptional condition you want to convey. It's also good practice to provide a descriptive message with the exception to aid in troubleshooting and error handling.

Remember, if the exception you are throwing is a checked exception, you need to either handle it within the method using a try-catch block or declare it in the method signature using the throws keyword.
</details>
<details><summary>

## What happens when you throw a Checked Exception from a method ?
</summary>
When you throw a checked exception from a method, you are indicating that the method may encounter an exceptional condition that the caller of the method needs to handle. The checked exception must be declared in the method's signature using the throws keyword.

If a method throws a checked exception, the caller of that method is required to either catch the exception using a try-catch block or declare that it can also throw the exception using the throws keyword. This ensures that the caller acknowledges and handles the possibility of an exceptional situation.

            class AmountAdder {
                    static Amount addAmounts(Amount amount1, Amount amount2) {
                            if (!amount1.currency.equals(amount2.currency)) {
                                    throw new Exception("Currencies don't match");// COMPILER ERROR!
                                    // Unhandled exception type Exception
                            }
                            return new Amount(amount1.currency, amount1.amount + amount2.amount);
                    }
            }

If the caller chooses to catch the checked exception, it can provide appropriate error-handling logic to deal with the exceptional condition. If the caller declares that it can also throw the exception, the responsibility of handling the exception is then passed to the caller's caller.

In summary, throwing a checked exception from a method alerts the caller about a potential exceptional situation and enforces the handling or propagation of the exception through the calling chain.
</details>
<details><summary>

## What are the options you have to eliminate compilation errors when handling checked exceptions?
</summary>
When handling checked exceptions in Java, you have several options to eliminate compilation errors:

1. **Catch and Handle the Exception** You can surround the code that may throw the checked exception with a try-catch block. Inside the catch block, you provide the necessary error-handling logic to handle the exception gracefully.

2. **Declare the Exception** If you don't want to handle the checked exception at the current level, you can declare the exception using the throws keyword in the method signature. This passes the responsibility of handling the exception to the method's caller.

3. **Wrap the Exception** If the checked exception is not compatible with the current method's signature, you can wrap it inside a different exception that is compatible. This involves catching the checked exception, creating a new exception object, and throwing the wrapped exception instead.

4. **Handle with Finally** If you are unable to handle the checked exception within the current method, you can use a try-finally block. The finally block will execute regardless of whether an exception is thrown or not, allowing you to perform necessary cleanup or resource release operations.

5. **Rethrow the Exception** If you catch a checked exception but cannot handle it properly, you can rethrow the exception using the throw keyword. This propagates the exception to the caller without handling it within the current method.

6. **Handle with Optional** If you are using Java 8 or later, you can use the Optional class to handle checked exceptions in a more functional style. You can wrap the potentially exception-throwing code in a lambda expression and use Optional to handle the exception elegantly.

It's important to note that the appropriate choice depends on the specific scenario and requirements of your application. Consider the nature of the exception, the level at which it can be effectively handled, and the design principles of your code when selecting the appropriate approach.
</details>
<details><summary>

## How do you create a Custom Exception?
</summary>
To create a custom exception in Java, you need to create a new class that extends either the Exception class or one of its subclasses, such as RuntimeException. Here are the steps to create a custom exception:

1. Create a new class that extends Exception or one of its subclasses. For example:

            public class CustomException extends Exception {
                // Custom exception code...
            }

2. Optionally, you can add constructors to your custom exception class to provide additional functionality or customization. For example:

            public class CustomException extends Exception {
                public CustomException() {
                    super();
                }
                
                public CustomException(String message) {
                    super(message);
                }
                
                public CustomException(String message, Throwable cause) {
                    super(message, cause);
                }
                
                // Additional constructors or custom code...
            }

3. In your code, when an exceptional situation occurs that warrants throwing your custom exception, you can create an instance of your custom exception class and throw it using the throw keyword. For example:

            public class Example {
                public static void main(String[] args) {
                    try {
                        throw new CustomException("Something went wrong.");
                    } catch (CustomException e) {
                        System.out.println("Custom Exception caught: " + e.getMessage());
                    }
                }
            }

In this example, we create an instance of the CustomException class with a specific message, and then we throw it using the throw keyword. The catch block catches the custom exception and handles it accordingly.

By creating a custom exception, you can define and throw exceptions that are specific to your application's domain or requirements, allowing you to provide more meaningful error information and separate different types of exceptional situations.
</details>
<details><summary>

## How do you handle multiple exception types with same exception handling block?
</summary>
In Java, you can handle multiple exception types using a single exception handling block by either specifying multiple catch blocks or by catching a common superclass of the exception types. Here's how you can handle multiple exception types in the same exception handling block:

**Option 1:** Multiple Catch Blocks

            try {
                // Code that may throw exceptions
            } catch (ExceptionType1 e) {
                // Handling logic for ExceptionType1
            } catch (ExceptionType2 e) {
                // Handling logic for ExceptionType2
            } catch (ExceptionType3 e) {
                // Handling logic for ExceptionType3
            }

In this approach, each catch block handles a specific exception type. When an exception occurs, the catch blocks are evaluated in order, and the first catch block that matches the exception type is executed.

**Option 2:** Catching a Common Superclass

            try {
                // Code that may throw exceptions
            } catch (ExceptionType1 | ExceptionType2 | ExceptionType3 e) {
                // Common handling logic for ExceptionType1, ExceptionType2, and ExceptionType3
            }

In this approach, a single catch block handles multiple exception types by using the pipe symbol (|) to specify multiple exception types separated by it. The catch block will execute if any of the specified exception types are thrown.

It's important to note that when catching multiple exception types, the exception variable (e in the above examples) is implicitly final, meaning you cannot modify its value within the catch block.

By handling multiple exception types in the same exception handling block, you can provide a unified error-handling mechanism for different types of exceptions, reducing code duplication and improving code readability.
</details>
<details><summary>

## Can you explain about try with resources?
</summary>
Certainly! "Try with resources" is a feature introduced in Java 7 that simplifies resource management and ensures proper handling of resources that need to be closed, such as file streams, database connections, or network sockets. It eliminates the need for explicit finally blocks to close resources.

Here's how the "try with resources" statement works:

1. The try block is used to enclose the code that uses the resources. It is followed by a set of parentheses () where you declare and initialize the resources.

2. The resources declared in the parentheses must implement the AutoCloseable interface or its subinterface Closeable. These interfaces provide the close() method that is used to release the allocated resources.

3. After the try block, you don't need to explicitly close the resources. The Java runtime automatically takes care of closing the resources for you, even if an exception occurs.

Here's an example that demonstrates the usage of "try with resources" with a file stream:

            try (FileInputStream fileInputStream = new FileInputStream("file.txt")) {
                // Code that uses the fileInputStream
                // ...
            } catch (IOException e) {
                // Exception handling code
            }

In this example, the FileInputStream is declared and initialized within the parentheses after the try keyword. The resource, in this case, the file stream, will be automatically closed at the end of the try block, whether an exception occurs or not.

If an exception occurs within the try block, the catch block will handle the exception as usual. After the catch block is executed, the file stream will be closed automatically.

The "try with resources" statement ensures that resources are properly closed, even in scenarios where exceptions are thrown. It simplifies resource management, reduces the boilerplate code required for closing resources, and improves the overall reliability of your code.
</details>
<details><summary>

## How does try with resources work?
</summary>
When you use the "try with resources" statement in Java, it ensures that resources are automatically closed at the end of the block, regardless of whether an exception occurs or not. Here's how it works:

1. When the "try with resources" statement is encountered, the resources are declared and initialized within the parentheses after the try keyword. Each resource must implement the AutoCloseable interface or its subinterface Closeable.

2. The resources declared in the parentheses are implicitly final, meaning you cannot reassign them within the block.

3. After the resources are initialized, the try block is executed, which contains the code that uses the resources.

4. At the end of the try block, the resources are automatically closed in reverse order of their declaration. The close() method of each resource is called. This happens regardless of whether an exception occurs within the try block or not.

5. If an exception occurs within the try block, the exception is caught and handled by the appropriate catch block, if present. After the catch block is executed, the resources are still automatically closed in the reverse order of their declaration.

6. If no exception occurs, the catch block is skipped, and the resources are still closed automatically.

Here's an example to illustrate how "try with resources" works:

            try (FileInputStream fileInputStream = new FileInputStream("file.txt");
                InputStreamReader inputStreamReader = new InputStreamReader(fileInputStream)) {
                // Code that uses fileInputStream and inputStreamReader
                // ...
            } catch (IOException e) {
                // Exception handling code
            }

In this example, we have two resources declared and initialized within the parentheses after the try keyword: fileInputStream and inputStreamReader. These resources will be automatically closed in the reverse order of their declaration, meaning inputStreamReader will be closed first, followed by fileInputStream.

By using the "try with resources" statement, you don't need to explicitly close the resources using a finally block. The Java runtime ensures that the resources are properly closed, even in the presence of exceptions, making your code cleaner and more reliable.
</details>
<details><summary>

## Can you explain a few Exception Handling Best Practices?
</summary>
Here are a few exception handling best practices in Java:

**1. Use specific exception types -** Catch and handle exceptions at an appropriate level of granularity. Use specific exception types to catch and handle specific exceptional situations. This helps in providing meaningful error messages and allows for more targeted exception handling.

**2. Catch the most specific exception first -** When using multiple catch blocks, order them from the most specific exception type to the more general ones. This ensures that exceptions are caught and handled at the appropriate level, preventing more generic catch blocks from intercepting specific exceptions.

**3. Handle exceptions at the appropriate level -** Catch and handle exceptions at the appropriate level in your application. Consider whether it makes sense to handle the exception locally or propagate it to a higher level where it can be handled more effectively.

**4. Provide meaningful error messages -** When catching and handling exceptions, provide meaningful error messages or log the relevant details. This helps in diagnosing and troubleshooting issues during development and production.

**5. Avoid empty catch blocks -** Avoid using empty catch blocks as they silently ignore exceptions and make it difficult to diagnose and debug issues. If you decide not to handle an exception, provide a comment explaining the rationale.

**6. Use finally blocks for cleanup -** Use finally blocks to ensure that necessary cleanup operations are performed, such as closing resources (e.g., file streams, database connections) or releasing acquired locks. finally blocks are executed regardless of whether an exception occurs or not.

**7. Avoid catching RuntimeExceptions -** RuntimeExceptions and their subclasses (unchecked exceptions) usually indicate programming errors or unexpected conditions. It's generally better to let these exceptions propagate and be caught at higher levels or allow them to be handled by default exception handling mechanisms.

**8. Don't catch and ignore exceptions unnecessarily -** Avoid catching and ignoring exceptions unless you have a valid reason to do so. Ignoring exceptions can lead to silent failures and make it harder to identify and fix issues.

**9. Avoid excessive nesting of try-catch blocks -** Excessive nesting of try-catch blocks can make the code more complex and harder to read. Refactor the code to simplify the nesting and improve its readability.

**10. Use try-with-resources -** Utilize the "try with resources" statement when working with resources that need to be closed, such as file streams or database connections. This ensures proper resource management and eliminates the need for explicit finally blocks.

By following these exception handling best practices, you can improve the robustness, maintainability, and reliability of your Java code.
</details>
