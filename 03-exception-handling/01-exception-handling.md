# Exception handling

<details><summary>

## [Easy] Why is Exception Handling important?
</summary>

Exception handling is crucial in Java (and in programming in general) for several reasons:

- **Error management** Exception handling allows you to handle errors and exceptional situations that may occur during the execution of a program. Instead of abruptly terminating the program, you can gracefully handle these errors and take appropriate actions. This helps in maintaining the stability and reliability of the program.

- **Program flow control** With exception handling, you can control the flow of your program when an exceptional situation arises. By catching and handling exceptions, you can decide how your program should proceed in such cases. It provides a mechanism to recover from errors and continue the execution of the program, rather than crashing or terminating unexpectedly.

- **Debugging and troubleshooting** Exception handling aids in debugging and troubleshooting code. When an exception is thrown, it provides valuable information about the cause of the error, including the stack trace, error message, and the line of code where the exception occurred. This information helps developers identify and fix the problem more efficiently.

- **Robustness and stability** By handling exceptions, you can make your code more robust and resilient. Instead of letting errors propagate and potentially causing a system failure, you can catch and handle exceptions at appropriate levels of your code. This allows you to handle errors gracefully and ensure the stability of your program.

- **User-friendly experience** Exception handling enables you to provide meaningful error messages and handle errors in a user-friendly manner. Instead of showing cryptic error messages to users, you can catch exceptions, display custom error messages, and guide users on how to resolve or recover from the error.

- **Code maintainability** Exception handling promotes code maintainability by separating the normal code flow from the error-handling code. By encapsulating error-handling logic in exception handlers, you can keep the main code clean and focused on its primary functionality. This separation enhances code readability and maintainability.

In summary, exception handling is essential in Java because it allows you to manage errors, control program flow, debug code, ensure stability, provide a better user experience, and maintain code quality. It is a fundamental aspect of writing robust and reliable software.

**Example:**

```java
public User loadUser(long id) {
    try {
        return userClient.fetch(id);                       // may fail: network, timeout
    } catch (TimeoutException e) {
        log.warn("User service timed out for id {}", id);  // program keeps running gracefully
        return User.anonymous();                           // sensible fallback
    }
}
```

</details>

<details><summary>

## [Easy] What is the need for finally block?
</summary>

`finally` contains code that must run whether the `try` block completes normally, returns early, or throws.

Typical uses:
- **Releasing resources:** closing files, streams, DB connections, sockets (today, prefer try-with-resources).
- **Unlocking:** `lock.unlock()` after `lock.lock()`.
- **Cleanup and bookkeeping:** clearing `ThreadLocal`/MDC values, decrementing counters, recording metrics.

Things to know:
- `finally` runs even when `try` or `catch` executes `return`, `break` or `continue`.
- It does **not** "propagate" or rethrow a caught exception; the exception continues only if it wasn't caught or the catch rethrows it.
- **Don't `return` from `finally`:** it overrides the `try`'s return value and silently swallows any exception thrown in `try`/`catch`.

```java
static int test() {
	try {
		throw new RuntimeException("lost!");
	} finally {
		return 1;            // BAD: the exception disappears, method returns 1
	}
}
```

**Example:**

```java
Connection conn = null;
try {
    conn = dataSource.getConnection();
    // run queries...
} catch (SQLException e) {
    log.error("Query failed", e);
} finally {
    if (conn != null) {
        try { conn.close(); } catch (SQLException ignored) {}   // always released
    }
}
// Modern code: try-with-resources does this automatically
```

</details>

<details><summary>

## [Easy] In what scenarios is code in finally not executed?
</summary>

The finally block is always get executed unless there is an abnormal program termination either resulting from a JVM crash or from a call to System.exit().

- A finally block is always get executed whether the exception has occurred or not.
- If an exception occurs like closing a file or DB connection, then the finally block is used to clean up the code.
- We cannot say the finally block is always executes because sometimes if any statement like System.exit() or some similar code is written into try block then program will automatically terminate and the finally block will not be executed in this case.
- A finally block will not execute due to other conditions like when JVM runs out of memory when our java process is killed forcefully from task manager or console when our machine shuts down due to power failure and deadlock condition in our try block.

**Example:**

```java
try {
    System.out.println("in try");
    System.exit(0);          // JVM exits -> finally does NOT run
} finally {
    System.out.println("finally");   // never printed
}
// Also skipped if the JVM crashes, the process is killed (kill -9),
// or the thread runs an infinite loop / deadlocks inside try.
```

</details>

<details><summary>

## [Easy] Will finally be executed in the program below?
</summary>

```java
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
```

In the provided code snippet, the finally block will be executed even when there is a return statement in the try or catch block.

When a return statement is encountered within the try or catch block, the execution flow immediately jumps to the finally block before actually returning from the method. This ensures that the code inside the finally block is executed before the method exits, regardless of whether an exception occurred or not.

In the given code, if an exception occurs within the try block, the catch block will be executed, printing the message "Exception Handled - Method 2". After that, the control flow will reach the finally block, where the connection.close() method will be invoked to perform necessary cleanup operations. Finally, the method will return.

If no exception occurs within the try block, the code inside the finally block will still be executed before the method returns. This allows for proper cleanup of resources (in this case, closing the connection) regardless of the success or failure of the logic inside the try block.

So, in conclusion, the finally block in the provided code snippet will be executed, even if there is a return statement in the try or catch block.
</details>

<details><summary>

## [Easy] Is try without a catch is allowed?
</summary>

Yes, in two forms:

1. **`try` + `finally`** – no catch; the exception propagates after `finally` runs.
2. **try-with-resources** – `try (resource) { }` with neither catch nor finally is legal; resources are closed automatically.

```java
lock.lock();
try {
	updateSharedState();
} finally {
	lock.unlock();            // always runs; exception still propagates to the caller
}

try (BufferedReader r = Files.newBufferedReader(path)) {   // no catch/finally needed
	return r.readLine();
}
```

If the code inside throws a **checked** exception, the method must still declare it with `throws`, because `try`/`finally` doesn't handle it.

</details>

<details><summary>

## [Easy] Is try without catch and finally allowed?
</summary>

No. Below method would give a Compilation Error!! (End of try block)

```java
    private static void method2() {
        Connection connection = new Connection();
        connection.open();
        try {
            // LOGIC
            String str = null;
            str.toString();
        }//COMPILER ERROR!!
    }
```

</details>

<details><summary>

## [Easy] Can you explain the hierarchy of Exception Handling classes?
</summary>

All exceptions and errors extend `java.lang.Throwable`, which has two direct subclasses:

- **`Error`** – serious problems in the JVM or environment that applications normally don't catch: `OutOfMemoryError`, `StackOverflowError`, `NoClassDefFoundError`, `ExceptionInInitializerError`.
- **`Exception`** – conditions an application may want to handle.
  - **Checked exceptions:** `Exception` and its subclasses *except* `RuntimeException` – e.g. `IOException`, `SQLException`, `ClassNotFoundException`, `InterruptedException`. The compiler forces you to catch or declare them.
  - **Unchecked exceptions:** `RuntimeException` and its subclasses – e.g. `NullPointerException`, `IllegalArgumentException`, `IllegalStateException`, `ArithmeticException`, `ClassCastException`, `IndexOutOfBoundsException`.

`Error` and its subclasses are also unchecked.

Catch the most specific types first, because a `catch (Exception e)` placed first would make later, more specific catches unreachable (compile error).

**Example:**

```text
Throwable
├── Error                       (JVM problems - don't catch)
│   ├── OutOfMemoryError
│   └── StackOverflowError
└── Exception
    ├── IOException             (checked)
    ├── SQLException            (checked)
    └── RuntimeException        (unchecked)
        ├── NullPointerException
        ├── IllegalArgumentException
        ├── ArithmeticException
        └── IndexOutOfBoundsException
```

```java
try {
    readFile();
} catch (FileNotFoundException e) {   // most specific first
    ...
} catch (IOException e) {             // then its parent
    ...
}
```

</details>

<details><summary>

## [Easy] What is the difference between Error and Exception?
</summary>

| | `Error` | `Exception` |
|---|---|---|
| Meaning | Serious JVM/environment problem | Problem the application can anticipate and handle |
| Examples | `OutOfMemoryError`, `StackOverflowError`, `NoClassDefFoundError` | `IOException`, `SQLException`, `IllegalArgumentException` |
| Checked by compiler? | No (unchecked) | Checked, except `RuntimeException` and subclasses |
| Should you catch it? | Almost never; fix the cause (memory, recursion, classpath) | Yes, where you can do something useful |
| Recovery | Usually not possible | Usually possible (retry, fallback, error response) |

Both extend `Throwable`.

**Example:**

```java
void recurse() { recurse(); }   // StackOverflowError - an Error: fix the code, don't catch it

try {
    int x = Integer.parseInt("abc");
} catch (NumberFormatException e) {   // an Exception: recoverable, handle it
    System.out.println("Invalid number, using default");
}
```

</details>

<details><summary>

## [Easy] What is the difference between Checked Exceptions and Unchecked Exceptions?
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

**Example:**

```java
// Checked: compiler forces you to handle or declare
public String readConfig(Path p) throws IOException {
    return Files.readString(p);
}

// Unchecked: compiler doesn't force handling - usually a bug or invalid input
public int divide(int a, int b) {
    if (b == 0) throw new IllegalArgumentException("Divisor must not be zero");
    return a / b;
}
```

</details>

<details><summary>

## [Easy] How do you throw an exception from a method?
</summary>

In Java, you can throw an exception from a method using the throw keyword followed by an instance of an exception class. Here's how you can throw an exception from a method:

- **Declare the exception in the method signature** If the exception you want to throw is a checked exception, you need to declare it in the method signature using the throws keyword. This notifies the calling code that the method can throw this exception, and the caller must handle or declare it.

```java
    public void someMethod() throws SomeException {
        // code that may throw SomeException
    }
```

- **Create an instance of the exception class** Within the method, when you encounter a condition that warrants an exception, create an instance of the appropriate exception class using the new keyword.

```java
    public void someMethod() throws SomeException {
        if (someCondition) {
            SomeException exception = new SomeException("Exception message");
            throw exception;
        }
    }
```

You can also directly throw an instance of the exception class without assigning it to a variable:

```java
    public void someMethod() throws SomeException {
        if (someCondition) {
            throw new SomeException("Exception message");
        }
    }
```

- **Propagate the exception** Once the throw statement is executed, the exception is thrown out of the method, propagating it to the calling code. The calling code can then catch the exception and handle it or propagate it further.
When throwing an exception, it's important to choose the appropriate exception class that accurately represents the exceptional condition you want to convey. It's also good practice to provide a descriptive message with the exception to aid in troubleshooting and error handling.

Remember, if the exception you are throwing is a checked exception, you need to either handle it within the method using a try-catch block or declare it in the method signature using the throws keyword.
</details>

<details><summary>

## [Easy] What happens when you throw a Checked Exception from a method ?
</summary>

When you throw a checked exception from a method, you are indicating that the method may encounter an exceptional condition that the caller of the method needs to handle. The checked exception must be declared in the method's signature using the throws keyword.

If a method throws a checked exception, the caller of that method is required to either catch the exception using a try-catch block or declare that it can also throw the exception using the throws keyword. This ensures that the caller acknowledges and handles the possibility of an exceptional situation.

```java
        class AmountAdder {
                static Amount addAmounts(Amount amount1, Amount amount2) {
                        if (!amount1.currency.equals(amount2.currency)) {
                                throw new Exception("Currencies don't match");// COMPILER ERROR!
                                // Unhandled exception type Exception
                        }
                        return new Amount(amount1.currency, amount1.amount + amount2.amount);
                }
        }
```

If the caller chooses to catch the checked exception, it can provide appropriate error-handling logic to deal with the exceptional condition. If the caller declares that it can also throw the exception, the responsibility of handling the exception is then passed to the caller's caller.

In summary, throwing a checked exception from a method alerts the caller about a potential exceptional situation and enforces the handling or propagation of the exception through the calling chain.
</details>

<details><summary>

## [Easy] How do you create a Custom Exception?
</summary>

To create a custom exception in Java, you need to create a new class that extends either the Exception class or one of its subclasses, such as RuntimeException. Here are the steps to create a custom exception:

1. Create a new class that extends Exception or one of its subclasses. For example:

```java
        public class CustomException extends Exception {
            // Custom exception code...
        }
```

2. Optionally, you can add constructors to your custom exception class to provide additional functionality or customization. For example:

```java
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
```

3. In your code, when an exceptional situation occurs that warrants throwing your custom exception, you can create an instance of your custom exception class and throw it using the throw keyword. For example:

```java
        public class Example {
            public static void main(String[] args) {
                try {
                    throw new CustomException("Something went wrong.");
                } catch (CustomException e) {
                    System.out.println("Custom Exception caught: " + e.getMessage());
                }
            }
        }
```

In this example, we create an instance of the CustomException class with a specific message, and then we throw it using the throw keyword. The catch block catches the custom exception and handles it accordingly.

By creating a custom exception, you can define and throw exceptions that are specific to your application's domain or requirements, allowing you to provide more meaningful error information and separate different types of exceptional situations.
</details>

<details><summary>

## [Easy] How do you handle multiple exception types with same exception handling block?
</summary>

Use a **multi-catch** (Java 7): list the types separated by `|`.

```java
try {
	parseAndSave(file);
} catch (IOException | ParseException e) {        // one block for both
	log.error("Import failed", e);
}
```

Rules:
- The types in a multi-catch can't be subclasses of each other (`catch (IOException | FileNotFoundException e)` is a compile error, because `FileNotFoundException` is already an `IOException`).
- The variable `e` is implicitly `final`.

Alternatives:
- **Catch a common superclass** (`catch (IOException e)`) if all types share one and you want to handle them all.
- **Separate catch blocks** (most specific first) when each type needs different handling.

</details>

<details><summary>

## [Medium] What design pattern is used to implement Exception handling Features in most languages?
</summary>

The classic answer is the **Chain of Responsibility** pattern.

When an exception is thrown, the current method gets the first chance to handle it. If it has no matching `catch`, the exception is passed to its caller, then the caller's caller, and so on up the call stack, until some method handles it. If none does, the thread's default handler prints the stack trace and the thread ends. Each method in the call stack is a "handler" in the chain.

```java
void controller() {
	try {
		service();                         // handler 3: catches it
	} catch (IllegalStateException e) {
		System.out.println("Handled: " + e.getMessage());
	}
}
void service() { repository(); }           // handler 2: doesn't catch, passes it on
void repository() {                        // handler 1: throws
	throw new IllegalStateException("DB down");
}
```

`try`/`catch`/`finally` is the language syntax for taking part in that chain; it is not itself a GoF pattern.

</details>

<details><summary>

## [Medium] What are the options you have to eliminate compilation errors when handling checked exceptions?
</summary>

When code calls a method that throws a checked exception, you must do one of these:

1. **Catch and handle it** with `try`/`catch` (log, retry, fallback, return a default).
2. **Declare it** with `throws` in your method signature so the caller decides.
3. **Wrap it** in an unchecked exception (keeping the cause) when the caller can't do anything useful, e.g. `throw new UncheckedIOException(e)` or a custom `RuntimeException`. Common in service layers and inside lambdas, because functional interfaces like `Function` can't throw checked exceptions.
4. **Catch it and rethrow** a more meaningful checked or unchecked exception for your layer (exception translation, as Spring does with `DataAccessException`).

A `try`/`finally` without `catch` does **not** remove the compile error, and `Optional` doesn't handle exceptions; neither is an option here.

**Example:**

```java
// Option 1: handle it
void load() {
    try { Files.readString(Path.of("a.txt")); }
    catch (IOException e) { log.error("Read failed", e); }
}

// Option 2: declare it and let the caller decide
void load2() throws IOException {
    Files.readString(Path.of("a.txt"));
}

// Option 3: wrap in an unchecked exception (common in lambdas and service layers)
void load3() {
    try { Files.readString(Path.of("a.txt")); }
    catch (IOException e) { throw new UncheckedIOException(e); }
}
```

</details>

<details><summary>

## [Medium] Can you explain about try with resources?
</summary>

**Try-with-resources** (Java 7) closes resources automatically. Any object that implements `AutoCloseable` (or its subinterface `Closeable`) can be declared in the parentheses after `try`. Its `close()` is called when the block ends, normally or by exception, so you don't need a `finally` for cleanup.

```java
try (BufferedReader reader = Files.newBufferedReader(Path.of("file.txt"))) {
	System.out.println(reader.readLine());
} catch (IOException e) {
	log.error("Could not read file", e);   // the reader is ALREADY closed here
}
```

- Resources are closed **before** any `catch` or `finally` block runs.
- Since Java 9 you can use an existing **effectively final** variable: `try (reader) { ... }`.
- If both the body and `close()` throw, the body's exception is thrown and the `close()` exception is attached as a **suppressed** exception (`e.getSuppressed()`), so nothing is lost.

</details>

<details><summary>

## [Medium] How does try with resources work?
</summary>

1. Each resource in the parentheses is initialised in order. It must implement `AutoCloseable` and is implicitly `final`.
2. The `try` body runs.
3. When the body finishes (normally or with an exception), the resources are **closed in reverse order** of declaration.
4. **Then** a matching `catch` block runs (if an exception occurred), and **then** `finally`.
5. If `close()` throws while an exception is already in flight, that close exception is added as a **suppressed** exception to the primary one.

```java
try (FileInputStream in = new FileInputStream("file.txt");
     InputStreamReader reader = new InputStreamReader(in)) {
	// use reader
} catch (IOException e) {
	// reader.close() then in.close() have already run
	for (Throwable s : e.getSuppressed()) log.warn("close failed", s);
}
```

The compiler turns this into nested `try`/`finally` blocks with null checks and `addSuppressed` calls, which is far less error-prone than writing it by hand.

</details>

<details><summary>

## [Medium] Can you explain a few Exception Handling Best Practices?
</summary>

1. **Catch specific exceptions,** not `Exception` or `Throwable`, unless you're at a top-level boundary (controller advice, message listener) that must log and convert everything.
2. **Order catch blocks** from most specific to most general.
3. **Never swallow exceptions.** An empty `catch` hides bugs; at least log with context.
4. **Keep the cause** when wrapping: `throw new OrderFailedException("Order " + id, e)`.
5. **Log once,** where the exception is handled, not at every layer (avoids duplicate stack traces).
6. **Use try-with-resources** for anything `AutoCloseable`.
7. **Don't use exceptions for normal control flow** (e.g. to detect a missing map key).
8. **Prefer unchecked exceptions for programming errors** and invalid input; don't catch generic `RuntimeException` just to hide bugs, but do catch specific ones you can handle (e.g. `DuplicateKeyException` → 409).
9. **Restore the interrupt flag** when catching `InterruptedException`: `Thread.currentThread().interrupt();`.
10. **Don't expose internals** (stack traces, SQL) to API clients; return a clean error response and log the details.
11. **Create custom exceptions** for meaningful domain errors (`InsufficientBalanceException`) instead of generic ones.

**Example:**

```java
// Bad: swallowed, generic, loses the cause
try { process(); } catch (Exception e) { }

// Good
try {
    process(order);
} catch (PaymentDeclinedException e) {                 // catch specific exceptions
    throw new OrderFailedException("Order " + order.id() + " declined", e); // keep the cause
} finally {
    metrics.increment("orders.processed");
}

// Use try-with-resources, don't use exceptions for normal flow control,
// log once (where handled), and never expose stack traces to API clients.
```

</details>
