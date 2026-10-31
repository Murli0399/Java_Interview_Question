# Advanced Concurrency

<details><summary>

## Describe a few other important methods in threads.
</summary>

| Method | What it does |
|---|---|
| `start()` | Creates a new thread and calls `run()` on it. Calling `run()` directly runs on the current thread. |
| `sleep(ms)` | Pauses the current thread; **keeps** any locks it holds. |
| `join()` | Waits until the other thread finishes. |
| `interrupt()` | Sets the interrupt flag; a sleeping/waiting thread gets `InterruptedException`. |
| `isAlive()` | True between `start()` and the end of `run()`. |
| `setDaemon(true)` | JVM exits without waiting for daemon threads (must be set before `start()`). |
| `currentThread()` | Reference to the running thread. |

```java
Thread worker = new Thread(() -> {
    while (!Thread.currentThread().isInterrupted()) {
        // do work
    }
    System.out.println("stopping cleanly");
});
worker.start();
Thread.sleep(100);
worker.interrupt();   // polite stop request
worker.join();        // wait for it to finish
```
</details>

<details><summary>

## What are the important methods for inter-thread communication?
</summary>

`wait()`, `notify()` and `notifyAll()`, defined in `Object`. They must be called from inside a `synchronized` block on the **same object**, otherwise `IllegalMonitorStateException` is thrown.

- `wait()`: releases the lock and sleeps until notified.
- `notify()`: wakes **one** waiting thread (which one is not specified).
- `notifyAll()`: wakes **all** waiting threads; they compete for the lock.

Always call `wait()` inside a `while` loop that re-checks the condition, because of spurious wakeups and because another thread may have changed the state first.
</details>

<details><summary>

## What is the difference between wait() and sleep()?
</summary>

| | `wait()` | `sleep()` |
|---|---|---|
| Defined in | `Object` | `Thread` |
| Releases lock | Yes | No |
| Must hold lock | Yes (inside `synchronized`) | No |
| Wakes up | `notify`/`notifyAll`, timeout, interrupt | Timeout or interrupt |
| Purpose | Coordination between threads | Simple pause |
</details>

<details><summary>

## Can you write a producer-consumer program with wait and notify?
</summary>

```java
class BoundedBuffer {
    private final Queue<Integer> items = new LinkedList<>();
    private final int capacity;

    BoundedBuffer(int capacity) { this.capacity = capacity; }

    public synchronized void put(int item) throws InterruptedException {
        while (items.size() == capacity) wait();   // buffer full
        items.add(item);
        notifyAll();                               // wake consumers
    }

    public synchronized int take() throws InterruptedException {
        while (items.isEmpty()) wait();            // buffer empty
        int item = items.poll();
        notifyAll();                               // wake producers
        return item;
    }
}

BoundedBuffer buffer = new BoundedBuffer(2);
new Thread(() -> {
    try { for (int i = 1; i <= 5; i++) { buffer.put(i); System.out.println("produced " + i); } }
    catch (InterruptedException e) { Thread.currentThread().interrupt(); }
}).start();
new Thread(() -> {
    try { for (int i = 1; i <= 5; i++) System.out.println("consumed " + buffer.take()); }
    catch (InterruptedException e) { Thread.currentThread().interrupt(); }
}).start();
```

In real code, use `BlockingQueue` instead; it does exactly this for you.
</details>

<details><summary>

## Write a program where two threads print odd and even numbers alternately.
</summary>

```java
class OddEvenPrinter {
    private int number = 1;
    private final int max;

    OddEvenPrinter(int max) { this.max = max; }

    synchronized void print(boolean odd) throws InterruptedException {
        while (number <= max) {
            while (number <= max && (number % 2 == 1) != odd) wait();
            if (number <= max) {
                System.out.println(Thread.currentThread().getName() + ": " + number++);
                notifyAll();
            }
        }
    }
}

OddEvenPrinter p = new OddEvenPrinter(10);
new Thread(() -> { try { p.print(true); } catch (InterruptedException ignored) {} }, "odd").start();
new Thread(() -> { try { p.print(false); } catch (InterruptedException ignored) {} }, "even").start();
// odd: 1, even: 2, odd: 3, ... even: 10
```
</details>

<details><summary>

## What does volatile guarantee, and what doesn't it?
</summary>

`volatile` guarantees **visibility** (a write by one thread is seen by others immediately, not cached in a CPU register) and **ordering** (no reordering around it). It does **not** make compound actions atomic.

```java
class Worker implements Runnable {
    private volatile boolean running = true;   // without volatile the loop may never stop
    public void run() { while (running) { /* work */ } }
    public void stop() { running = false; }
}

private volatile int count;
void increment() { count++; }  // still NOT thread-safe: read + add + write
// use AtomicInteger or synchronized instead
```

Good uses: stop flags, publishing an immutable object, double-checked locking singleton.
</details>

<details><summary>

## What is the Java Memory Model's happens-before relationship?
</summary>

"Happens-before" means the effects of action A are visible to action B. Key rules:

- Unlocking a monitor happens-before every later lock of the same monitor.
- A write to a `volatile` variable happens-before every later read of it.
- `Thread.start()` happens-before any action in the started thread.
- All actions in a thread happen-before another thread returns from `join()` on it.
- Writes to `final` fields in a constructor are visible once the object is published.

Without one of these, a thread may see stale or partially constructed data.
</details>

<details><summary>

## How do you prevent deadlocks?
</summary>

A deadlock needs four conditions at once: mutual exclusion, hold-and-wait, no preemption and circular wait. Break any one:

1. **Lock ordering:** always acquire locks in the same global order.
2. **Timeouts:** `tryLock(timeout)` and back off.
3. **Fewer locks:** keep critical sections small; prefer concurrent collections and immutable objects.
4. **Detect:** thread dumps (`jstack <pid>`) show "Found one Java-level deadlock".

```java
void transfer(Account a, Account b, int amount) {
    Account first = a.id() < b.id() ? a : b;   // consistent order by id
    Account second = a.id() < b.id() ? b : a;
    synchronized (first) {
        synchronized (second) {
            a.debit(amount);
            b.credit(amount);
        }
    }
}
```
</details>

<details><summary>

## What is a ThreadPoolExecutor and how do you size it?
</summary>

`Executors.newFixedThreadPool(n)` is a shortcut for a `ThreadPoolExecutor`. Know its parameters:

```java
ThreadPoolExecutor pool = new ThreadPoolExecutor(
    4,                          // corePoolSize: threads kept alive
    8,                          // maximumPoolSize: used only when the queue is full
    60, TimeUnit.SECONDS,       // keepAliveTime for extra threads
    new ArrayBlockingQueue<>(100),             // bounded queue of pending tasks
    new ThreadPoolExecutor.CallerRunsPolicy()  // when full: caller runs the task (back-pressure)
);
```

Order of growth: core threads → queue → extra threads up to max → rejection policy.

**Sizing:** CPU-bound ≈ number of cores; IO-bound ≈ cores × (1 + wait time / compute time). Avoid `newCachedThreadPool` and unbounded queues in production; they can create unlimited threads or tasks and exhaust memory.
</details>

<details><summary>

## What is CompletableFuture? Give an example.
</summary>

An asynchronous result you can chain without blocking. Useful for calling several services in parallel and combining results.

```java
ExecutorService io = Executors.newFixedThreadPool(8);

CompletableFuture<User> user = CompletableFuture.supplyAsync(() -> userService.find(id), io);
CompletableFuture<List<Order>> orders = CompletableFuture.supplyAsync(() -> orderService.forUser(id), io);

CompletableFuture<Profile> profile = user
    .thenCombine(orders, Profile::new)              // both in parallel
    .orTimeout(2, TimeUnit.SECONDS)
    .exceptionally(ex -> Profile.empty());          // fallback on error/timeout

System.out.println(profile.join());
```

- `thenApply`: transform result (sync)
- `thenCompose`: chain another async call (flatMap)
- `thenCombine`: combine two independent futures
- `allOf` / `anyOf`: wait for many
- Always pass your own executor for IO work; the default common pool is sized for CPU work.
</details>

<details><summary>

## What is ThreadLocal and when can it cause a memory leak?
</summary>

`ThreadLocal` gives each thread its own copy of a variable. Common uses: request IDs/tenant IDs for logging, `SimpleDateFormat` (not thread-safe), transaction context in Spring.

```java
public final class TenantContext {
    private static final ThreadLocal<String> TENANT = new ThreadLocal<>();
    public static void set(String id) { TENANT.set(id); }
    public static String get() { return TENANT.get(); }
    public static void clear() { TENANT.remove(); }
}

// in a servlet filter
try {
    TenantContext.set(request.getHeader("X-Tenant-Id"));
    chain.doFilter(request, response);
} finally {
    TenantContext.clear();   // essential with thread pools
}
```

**Leak:** pool threads live forever, so a value never `remove()`d stays referenced, and the next request on that thread may even see the previous tenant's data.
</details>

<details><summary>

## What are CountDownLatch, CyclicBarrier and Semaphore?
</summary>

- **CountDownLatch:** one or more threads wait until N events happen. Not reusable.
- **CyclicBarrier:** N threads wait for each other at a point, then all proceed. Reusable.
- **Semaphore:** limits how many threads access a resource at once.

```java
CountDownLatch ready = new CountDownLatch(3);
for (int i = 0; i < 3; i++) {
    pool.submit(() -> { loadCache(); ready.countDown(); });
}
ready.await();                    // main waits until all 3 caches load
System.out.println("server ready");

Semaphore dbSlots = new Semaphore(10); // at most 10 concurrent DB calls
dbSlots.acquire();
try { queryDatabase(); } finally { dbSlots.release(); }
```
</details>

<details><summary>

## What is ReadWriteLock?
</summary>

Allows many concurrent readers **or** one writer. Useful for read-heavy shared data such as in-memory config.

```java
class ConfigStore {
    private final Map<String, String> config = new HashMap<>();
    private final ReadWriteLock rw = new ReentrantReadWriteLock();

    String get(String key) {
        rw.readLock().lock();
        try { return config.get(key); } finally { rw.readLock().unlock(); }
    }

    void put(String key, String value) {
        rw.writeLock().lock();
        try { config.put(key, value); } finally { rw.writeLock().unlock(); }
    }
}
```
</details>

<details><summary>

## What are virtual threads (Java 21)?
</summary>

Virtual threads are lightweight threads managed by the JVM, not the OS. Millions can exist; when one blocks on IO, the JVM unmounts it from its carrier (platform) thread so the carrier serves another task.

```java
try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
    for (int i = 0; i < 10_000; i++) {
        executor.submit(() -> callRemoteApi());  // blocking style, scales like async
    }
}
Thread.ofVirtual().start(() -> System.out.println("hello"));
```

- Great for IO-bound request handling (Spring Boot 3.2+: `spring.threads.virtual.enabled=true`).
- No benefit for CPU-bound work.
- Don't pool them; create one per task.
- Long `synchronized` blocks around IO can pin the carrier thread (improved in newer JDKs); `ReentrantLock` avoids it.
</details>
