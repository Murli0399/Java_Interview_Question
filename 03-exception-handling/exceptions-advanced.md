# Exceptions (advanced)

<details><summary>

## [Easy] What is the difference between throw and throws?
</summary>

| | `throw` | `throws` |
|---|---|---|
| What | A **statement** that actually throws an exception object | Part of a **method signature** declaring exceptions the method may throw |
| Where | Inside a method body | After the parameter list |
| Followed by | One exception instance | One or more exception class names |
| Needed for | Any exception | Checked exceptions (optional for unchecked) |

```java
public Account find(long id) throws AccountNotFoundException {        // throws: declaration
	return repo.findById(id)
	           .orElseThrow(() -> new AccountNotFoundException(id));   // throw happens inside orElseThrow
}

public void withdraw(Account a, long amount) {
	if (amount <= 0) {
		throw new IllegalArgumentException("Amount must be positive"); // throw: statement
	}
}
```
</details>

<details><summary>

## [Medium] What happens if both try and finally contain a return statement?
</summary>

The **`finally` return wins**. The value from `try` is discarded, and if `try` threw an exception, that exception is **silently swallowed**.

```java
static int value() {
	try {
		return 1;
	} finally {
		return 2;          // overrides
	}
}
System.out.println(value());   // 2

static int hidden() {
	try {
		throw new IllegalStateException("important!");
	} finally {
		return 0;          // exception is lost
	}
}
System.out.println(hidden());  // 0, no exception
```

A related trap: if `try` returns a variable and `finally` changes that variable, the returned value doesn't change (the value was already saved), but if it's an object, changes to its state are visible.

Never `return` (or `throw`) from `finally`; compilers and linters warn about it.
</details>

<details><summary>

## [Medium] What is exception chaining and why does it matter?
</summary>

**Exception chaining** wraps a low-level exception inside a higher-level one, keeping the original as the **cause**. Callers get an exception that makes sense at their level, and the stack trace still shows the root cause ("Caused by: ...").

```java
public Invoice loadInvoice(long id) {
	try {
		return jdbc.queryForObject(SQL, mapper, id);
	} catch (DataAccessException e) {
		throw new InvoiceUnavailableException("Invoice " + id + " could not be loaded", e);  // keep cause
	}
}

class InvoiceUnavailableException extends RuntimeException {
	InvoiceUnavailableException(String message, Throwable cause) { super(message, cause); }
}
```

Always pass the cause. `throw new MyException(e.getMessage())` loses the original stack trace and makes production debugging much harder. Use `getCause()` to navigate the chain.
</details>

<details><summary>

## [Medium] What are the exception rules for method overriding?
</summary>

An overriding method:
- **May throw fewer or narrower checked exceptions** than the overridden method, or none.
- **May not throw new or broader checked exceptions.**
- **May throw any unchecked exceptions** (`RuntimeException`, `Error`).

```java
class Parent {
	void read() throws IOException { }
}

class ChildOk extends Parent {
	@Override void read() throws FileNotFoundException { }   // OK: narrower
}

class ChildAlsoOk extends Parent {
	@Override void read() { }                                // OK: none
}

class ChildBad extends Parent {
	// @Override void read() throws Exception { }            // COMPILE ERROR: broader
}
```

The reason is substitutability: code that calls `parent.read()` and handles `IOException` must still work when given a `Child` (Liskov substitution principle).
</details>

<details><summary>

## [Medium] When would you create a checked vs an unchecked custom exception?
</summary>

- **Checked (`extends Exception`)** – for conditions the **caller can reasonably recover from** and should be forced to think about, e.g. `InsufficientFundsException` in a banking library where the caller must decide what to do.
- **Unchecked (`extends RuntimeException`)** – for **programming errors** (invalid arguments, illegal state) and for application-level errors that are handled centrally, e.g. `ResourceNotFoundException` mapped to a 404 by `@RestControllerAdvice`.

Modern frameworks (Spring, JPA, Kafka clients) mostly use **unchecked** exceptions, because checked exceptions spread through every method signature and don't work inside lambdas. In a Spring Boot service, most custom exceptions are unchecked and handled in one global handler.

```java
public class ResourceNotFoundException extends RuntimeException {
	public ResourceNotFoundException(String resource, Object id) {
		super(resource + " " + id + " not found");
	}
}
```

Remember: `@Transactional` rolls back on unchecked exceptions by default, but **not** on checked ones unless you set `rollbackFor`.
</details>

<details><summary>

## [Medium] What is the difference between ClassNotFoundException and NoClassDefFoundError?
</summary>

| | `ClassNotFoundException` | `NoClassDefFoundError` |
|---|---|---|
| Type | Checked **exception** | **Error** |
| When | Your code loads a class **by name** at runtime and it isn't found | A class that **existed at compile time** is missing or can't be initialised at runtime |
| Thrown by | `Class.forName()`, `ClassLoader.loadClass()` | The JVM when it links/uses the class |
| Typical cause | Wrong class name, missing optional driver JAR | Missing JAR in the deployment, conflicting dependency versions, or a **static initializer that failed earlier** (first attempt throws `ExceptionInInitializerError`, later ones throw `NoClassDefFoundError`) |

Fixes: check the classpath / dependency tree (`mvn dependency:tree`), look for version conflicts, and search logs for the first `ExceptionInInitializerError`.
</details>

<details><summary>

## [Hard] What are suppressed exceptions?
</summary>

When a try-with-resources body throws an exception **and** closing a resource also throws, Java keeps the **body's exception as the primary** one and attaches the close failure to it as a **suppressed exception**, instead of losing either.

```java
class FlakyResource implements AutoCloseable {
	public void close() { throw new IllegalStateException("close failed"); }
}

try (FlakyResource r = new FlakyResource()) {
	throw new RuntimeException("work failed");
} catch (RuntimeException e) {
	System.out.println(e.getMessage());                       // work failed
	System.out.println(e.getSuppressed()[0].getMessage());    // close failed
}
```

You can add your own with `e.addSuppressed(other)`. Before Java 7, a manual `finally { close(); }` that threw would replace the original exception, hiding the real cause.
</details>

<details><summary>

## [Hard] What is ExceptionInInitializerError?
</summary>

It's an `Error` thrown when an exception occurs while a class is being **initialised** – in a `static` block or a static field initialiser. The original exception is available via `getCause()`. After that, the class is unusable: any later attempt to use it throws `NoClassDefFoundError`.

```java
class Config {
	static final int TIMEOUT = Integer.parseInt(System.getenv("TIMEOUT_MS"));  // NumberFormatException if missing or not a number
}

// First use:  ExceptionInInitializerError (cause: NumberFormatException)
// Later uses: NoClassDefFoundError: Could not initialize class Config
```

Avoid risky work in static initialisers; load configuration lazily or validate it at startup with clear error messages.
</details>
