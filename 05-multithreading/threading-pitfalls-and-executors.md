<details><summary>

## [Easy] What is a daemon thread?
</summary>

A **daemon thread** is a background thread that **doesn't keep the JVM alive**: the JVM exits when only daemon threads are left, without waiting for them to finish. Examples: the GC and JIT compiler threads.

```java
Thread heartbeat = new Thread(() -> {
	while (true) { sendHeartbeat(); sleepQuietly(5000); }
});
heartbeat.setDaemon(true);      // must be set before start()
heartbeat.start();
```

- `setDaemon(true)` after `start()` throws `IllegalThreadStateException`.
- Threads inherit daemon status from the thread that created them.
- Daemon threads can be stopped abruptly at exit (no `finally` blocks run), so don't use them for work that must complete, such as writing files or committing transactions.

Executors created with `Executors.newFixedThreadPool` use **non-daemon** threads by default, which is why forgetting `shutdown()` can stop a program from exiting.
</details>

<details><summary>

## [Easy] What is the difference between Runnable and Callable?
</summary>

| | `Runnable` | `Callable<V>` |
|---|---|---|
| Method | `void run()` | `V call() throws Exception` |
| Returns a value | No | Yes |
| Checked exceptions | Can't throw | Can throw |
| Used with | `Thread`, `executor.execute()`, `submit()` | `executor.submit()`, `invokeAll`, `invokeAny` |
| Since | Java 1.0 | Java 5 |

```java
Runnable log = () -> System.out.println("fire and forget");
Callable<Integer> compute = () -> 6 * 7;

ExecutorService pool = Executors.newSingleThreadExecutor();
pool.execute(log);
Future<Integer> answer = pool.submit(compute);
System.out.println(answer.get());   // 42
pool.shutdown();
```

`submit(Runnable)` also returns a `Future<?>`, whose `get()` returns `null` on success. Exceptions thrown by a task given to `execute()` go to the thread's uncaught exception handler; with `submit()` they're captured in the `Future` and only seen when you call `get()`.
</details>

<details><summary>

## [Medium] What is a race condition? How do you fix it?
</summary>

A **race condition** happens when the result depends on the timing of threads that access shared mutable data without proper synchronization. The classic case is a **read-modify-write** like `count++`, which is really three steps (read, add, write), so two threads can both read the same old value and one update is lost.

```java
class UnsafeCounter {
	private int count;
	void increment() { count++; }          // race: lost updates under concurrency
}

class SafeCounter {
	private final AtomicInteger count = new AtomicInteger();
	void increment() { count.incrementAndGet(); }   // atomic
}
```

Another common form is **check-then-act**: `if (!map.containsKey(k)) map.put(k, v);` – two threads can both pass the check. Fix it with an atomic operation (`map.putIfAbsent`, `computeIfAbsent` on a `ConcurrentHashMap`).

Fixes in general: use atomic classes, `synchronized` or locks around the whole compound action, concurrent collections with atomic methods, or avoid shared mutable state (immutability, thread confinement). In databases, the same problem is solved with transactions, unique constraints and optimistic locking.
</details>

<details><summary>

## [Medium] What makes a class thread-safe?
</summary>

A class is **thread-safe** if it behaves correctly when used by multiple threads at the same time, without the callers having to add their own synchronization.

Ways to achieve it, best first:
1. **No shared state:** stateless objects (most Spring services) are thread-safe by default.
2. **Immutability:** all fields `final`, no setters, defensive copies.
3. **Thread confinement:** each thread has its own copy (local variables, `ThreadLocal`).
4. **Thread-safe building blocks:** `AtomicInteger`, `ConcurrentHashMap`, `BlockingQueue`.
5. **Locking:** `synchronized` or `ReentrantLock` around every access to shared mutable state, using the same lock for related data.

Visibility matters as much as atomicity: without synchronization or `volatile`, one thread may never see another thread's writes.
</details>

<details><summary>

## [Medium] What are deadlock, livelock and starvation?
</summary>

| Problem | What happens | Example | Fix |
|---|---|---|---|
| **Deadlock** | Threads wait forever for each other's locks; nobody progresses | T1 holds A, wants B; T2 holds B, wants A | Global lock order, `tryLock` with timeout |
| **Livelock** | Threads keep reacting to each other and changing state, but nobody progresses | Two threads repeatedly back off and retry at exactly the same time | Add randomised backoff (jitter) |
| **Starvation** | A thread never gets the CPU or lock it needs because others keep winning | Low-priority threads, or a non-fair lock always grabbed by busy threads | Fair locks (`new ReentrantLock(true)`), bounded work, avoid priorities |

Detect deadlocks with a thread dump (`jstack <pid>` or `jcmd <pid> Thread.print`), which reports "Found one Java-level deadlock" with the threads and locks involved.
</details>

<details><summary>

## [Medium] What is the difference between shutdown() and shutdownNow()?
</summary>

| | `shutdown()` | `shutdownNow()` |
|---|---|---|
| New tasks | Rejected | Rejected |
| Queued tasks | **Still executed** | **Not executed** – returned as a `List<Runnable>` |
| Running tasks | Allowed to finish | **Interrupted** (`Thread.interrupt()`); they stop only if they respond to interruption |
| Blocks the caller? | No | No |

Neither waits. Combine them with `awaitTermination` for a graceful stop:

```java
void stop(ExecutorService pool) throws InterruptedException {
	pool.shutdown();                                         // stop accepting work
	if (!pool.awaitTermination(30, TimeUnit.SECONDS)) {      // let running/queued work finish
		List<Runnable> dropped = pool.shutdownNow();         // then force it
		log.warn("{} tasks were not run", dropped.size());
	}
}
```

Since Java 19, `ExecutorService` implements `AutoCloseable`; `close()` does a graceful shutdown and waits.
</details>

<details><summary>

## [Medium] What do invokeAll() and invokeAny() do?
</summary>

- **`invokeAll(tasks)`** – submits all `Callable`s and **blocks until every one completes**, returning a list of `Future`s in the same order. Use it for fan-out work where you need all results (e.g. call three services in parallel and combine them).
- **`invokeAny(tasks)`** – returns the result of the **first task that completes successfully** and cancels the rest. Use it for redundant calls (query two replicas, take the fastest).

Both have overloads with timeouts.

```java
ExecutorService pool = Executors.newFixedThreadPool(3);
List<Callable<Integer>> tasks = List.of(() -> 1, () -> 2, () -> 3);

int sum = 0;
for (Future<Integer> f : pool.invokeAll(tasks)) sum += f.get();   // 6

String fastest = pool.invokeAny(List.of(
	() -> { Thread.sleep(300); return "replica-1"; },
	() -> { Thread.sleep(50);  return "replica-2"; }));          // replica-2
pool.shutdown();
```

For non-blocking composition, `CompletableFuture.allOf` / `anyOf` do the same thing asynchronously.
</details>

<details><summary>

## [Hard] What is the Fork/Join framework and work stealing?
</summary>

The **Fork/Join framework** (Java 7) is for **CPU-bound divide-and-conquer** work: split a big task into subtasks (`fork`), compute them in parallel, then combine results (`join`). It runs on a **`ForkJoinPool`**.

**Work stealing:** each worker thread has its own deque of tasks. Idle workers **steal** tasks from the tail of busy workers' deques, which keeps all cores busy with little contention.

```java
class SumTask extends RecursiveTask<Long> {
	private final int[] arr; private final int lo, hi;
	SumTask(int[] arr, int lo, int hi) { this.arr = arr; this.lo = lo; this.hi = hi; }

	@Override
	protected Long compute() {
		if (hi - lo <= 10_000) {                       // small enough: compute directly
			long s = 0;
			for (int i = lo; i < hi; i++) s += arr[i];
			return s;
		}
		int mid = (lo + hi) >>> 1;
		SumTask left = new SumTask(arr, lo, mid);
		left.fork();                                   // run asynchronously
		long right = new SumTask(arr, mid, hi).compute();
		return left.join() + right;
	}
}

long total = ForkJoinPool.commonPool().invoke(new SumTask(data, 0, data.length));
```

**Parallel streams** and the default `CompletableFuture` async methods use `ForkJoinPool.commonPool()`. That's why you shouldn't run blocking IO there – it starves every other user of the common pool.
</details>
