# SOLID Principles and Design Patterns

<details><summary>

## Explain the SOLID principles with examples.
</summary>

**S – Single Responsibility:** a class has one reason to change.

```java
// Bad: InvoiceService calculates, saves AND emails
// Good: split responsibilities
class InvoiceCalculator { Money total(Invoice i) { /* ... */ return null; } }
class InvoiceRepository { void save(Invoice i) { /* ... */ } }
class InvoiceMailer { void send(Invoice i) { /* ... */ } }
```

**O – Open/Closed:** open for extension, closed for modification. Add a class instead of editing a growing `if/else`.

```java
interface DiscountPolicy { double apply(double amount); }
class FestiveDiscount implements DiscountPolicy { public double apply(double a) { return a * 0.9; } }
class NoDiscount implements DiscountPolicy { public double apply(double a) { return a; } }
// new discount = new class; checkout code doesn't change
```

**L – Liskov Substitution:** a subclass must be usable wherever its parent is. Classic violation: `Square extends Rectangle` breaks `setWidth` expectations. Another: a `ReadOnlyList` subclass that throws on `add()`.

**I – Interface Segregation:** many small interfaces beat one fat one.

```java
interface Readable { byte[] read(String key); }
interface Writable { void write(String key, byte[] data); }
class ReadOnlyStore implements Readable { public byte[] read(String k) { return new byte[0]; } }
```

**D – Dependency Inversion:** depend on abstractions, not concrete classes; inject them.

```java
class NotificationService {
    private final MessageSender sender;          // interface
    NotificationService(MessageSender sender) {  // Spring injects Email/SMS/WhatsApp impl
        this.sender = sender;
    }
}
```
</details>

<details><summary>

## Write a thread-safe Singleton. Which approach is best?
</summary>

```java
// 1. Double-checked locking (volatile is essential)
public final class Config {
    private static volatile Config instance;
    private Config() {}
    public static Config getInstance() {
        if (instance == null) {
            synchronized (Config.class) {
                if (instance == null) instance = new Config();
            }
        }
        return instance;
    }
}

// 2. Holder idiom: lazy and thread-safe via class-loading guarantees
public final class Registry {
    private Registry() {}
    private static class Holder { static final Registry INSTANCE = new Registry(); }
    public static Registry getInstance() { return Holder.INSTANCE; }
}

// 3. Enum: also safe against reflection and serialization attacks
public enum IdGenerator {
    INSTANCE;
    private final AtomicLong next = new AtomicLong();
    public long nextId() { return next.incrementAndGet(); }
}
```

Without `volatile`, another thread could see a non-null reference to a partially constructed object (instruction reordering). In Spring apps you rarely write this: beans are singletons by default.
</details>

<details><summary>

## What is the Factory pattern? Give a real example.
</summary>

A factory hides which concrete class gets created.

```java
interface SpeechToText { String transcribe(byte[] audio); }
class ConformerModel implements SpeechToText { public String transcribe(byte[] a) { return "..."; } }
class WhisperModel implements SpeechToText { public String transcribe(byte[] a) { return "..."; } }

class SpeechModelFactory {
    static SpeechToText forLanguage(String lang) {
        return switch (lang) {
            case "en", "hi" -> new ConformerModel();
            default -> new WhisperModel();       // fallback for other languages
        };
    }
}
```

In Spring, a cleaner version injects all implementations as `Map<String, SpeechToText>` (bean name → bean) and picks by key.
</details>

<details><summary>

## What is the Builder pattern?
</summary>

Builds objects with many optional fields readably and keeps them immutable.

```java
public final class HttpRequestSpec {
    private final String url; private final String method; private final int timeoutMs;

    private HttpRequestSpec(Builder b) { url = b.url; method = b.method; timeoutMs = b.timeoutMs; }
    public static Builder builder(String url) { return new Builder(url); }

    public static final class Builder {
        private final String url; private String method = "GET"; private int timeoutMs = 3000;
        private Builder(String url) { this.url = url; }
        public Builder method(String m) { this.method = m; return this; }
        public Builder timeoutMs(int t) { this.timeoutMs = t; return this; }
        public HttpRequestSpec build() { return new HttpRequestSpec(this); }
    }
}

HttpRequestSpec req = HttpRequestSpec.builder("https://api.x.com").method("POST").timeoutMs(500).build();
```

Lombok's `@Builder` generates this.
</details>

<details><summary>

## What is the Strategy pattern?
</summary>

Encapsulate interchangeable algorithms behind one interface and choose at runtime.

```java
interface LlmClient { String summarize(String transcript); }
class GeminiClient implements LlmClient { public String summarize(String t) { return "..."; } }
class AzureOpenAiClient implements LlmClient { public String summarize(String t) { return "..."; } }

class SummaryService {
    private final Map<String, LlmClient> clients;   // injected by Spring
    SummaryService(Map<String, LlmClient> clients) { this.clients = clients; }
    String summarize(String provider, String transcript) {
        return clients.get(provider).summarize(transcript);
    }
}
```

Other examples: `Comparator`, pricing rules, retry/backoff policies.
</details>

<details><summary>

## What is the Observer pattern?
</summary>

Subjects notify registered observers when something happens, without knowing who they are.

```java
interface OrderListener { void onOrderPlaced(Order o); }

class OrderService {
    private final List<OrderListener> listeners = new CopyOnWriteArrayList<>();
    void register(OrderListener l) { listeners.add(l); }
    void place(Order o) {
        // save order...
        listeners.forEach(l -> l.onOrderPlaced(o));
    }
}
```

Spring equivalents: `ApplicationEventPublisher` + `@EventListener`. At system scale, Kafka topics with consumer groups apply the same idea across services.
</details>

<details><summary>

## What are Adapter, Decorator, Proxy and Template Method?
</summary>

- **Adapter:** converts one interface into another (wrapping a third-party SMS SDK behind your `MessageSender`).
- **Decorator:** adds behaviour by wrapping (`BufferedInputStream(new FileInputStream(...))`, adding caching/metrics around a repository).
- **Proxy:** stands in for an object to control access. Spring AOP creates proxies for `@Transactional`, `@Cacheable`, `@Async`.
- **Template Method:** base class defines the steps, subclasses fill in some. `JdbcTemplate`, `RestTemplate`, `AbstractController`.

```java
abstract class ReportJob {
    final void run() { var data = fetch(); var out = transform(data); publish(out); } // template
    protected abstract List<String> fetch();
    protected List<String> transform(List<String> d) { return d; }  // optional override
    protected abstract void publish(List<String> out);
}
```
</details>

<details><summary>

## Composition vs inheritance: which should you prefer?
</summary>

Prefer **composition** ("has-a"): it's flexible at runtime, keeps classes loosely coupled and avoids fragile base classes. Use inheritance only for a genuine "is-a" relationship where the subclass honours the parent's contract (Liskov).

```java
// Inheritance misuse: a Stack that IS-A ArrayList exposes add(index), remove(index)...
// Composition: expose only what a stack should do
class Stack<T> {
    private final Deque<T> items = new ArrayDeque<>();
    void push(T t) { items.push(t); }
    T pop() { return items.pop(); }
}
```
</details>
