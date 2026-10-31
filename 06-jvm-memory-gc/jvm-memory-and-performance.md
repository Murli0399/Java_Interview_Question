# JVM Memory, Class Loading and Performance

<details><summary>

## What are the memory areas of the JVM?
</summary>

| Area | Shared? | Holds |
|---|---|---|
| **Heap** | All threads | Objects and arrays; managed by GC |
| **Stack** | One per thread | Method frames: local primitives, object references, return addresses |
| **Metaspace** (Java 8+, replaced PermGen) | All threads | Class metadata, method bytecode; uses native memory |
| **PC register** | Per thread | Current instruction address |
| **Native method stack** | Per thread | Frames for native (JNI) code |

```java
void process() {
    int count = 5;                 // stack
    User u = new User("Asha");     // reference 'u' on stack, User object on heap
    String s = "hello";            // literal in the String pool (part of the heap)
}
```

Errors: deep recursion → `StackOverflowError`; too many live objects → `OutOfMemoryError: Java heap space`; too many loaded classes → `OutOfMemoryError: Metaspace`.
</details>

<details><summary>

## How does generational garbage collection work?
</summary>

Most objects die young, so the heap is split:

- **Young generation:** Eden + two Survivor spaces. New objects go to Eden. A **minor GC** copies live objects to a Survivor space; objects surviving several cycles (age threshold) are promoted.
- **Old generation:** long-lived objects; collected by a **major/mixed GC**, which is more expensive.

An object is eligible for GC when it is **unreachable from GC roots** (thread stacks, static fields, JNI references). Circular references between unreachable objects are still collected.
</details>

<details><summary>

## Which garbage collectors are available, and which would you choose?
</summary>

| Collector | Flag | Best for |
|---|---|---|
| Serial | `-XX:+UseSerialGC` | Small heaps, single CPU, containers with tiny limits |
| Parallel | `-XX:+UseParallelGC` | Maximum throughput, batch jobs, pauses acceptable |
| **G1** (default since Java 9) | `-XX:+UseG1GC` | General-purpose services; balances throughput and pause time (`-XX:MaxGCPauseMillis=200`) |
| ZGC | `-XX:+UseZGC` | Very large heaps, sub-millisecond pauses (Java 15+ production ready; generational in 21) |
| Shenandoah | `-XX:+UseShenandoahGC` | Low pause, concurrent compaction |

For a typical Spring Boot microservice, G1 with tuned heap size is the usual choice; ZGC when latency SLAs are strict.
</details>

<details><summary>

## Can a Java application have a memory leak? Give examples.
</summary>

Yes: objects stay **reachable** although they are no longer needed.

```java
public class Cache {
    private static final Map<String, byte[]> CACHE = new HashMap<>(); // grows forever
    public static void put(String k, byte[] v) { CACHE.put(k, v); }
}
```

Common causes:
- Static collections or caches without eviction (use Caffeine/TTL, or a bounded `LinkedHashMap`).
- `ThreadLocal` values not removed in thread pools.
- Listeners/callbacks registered but never unregistered.
- Unclosed resources (streams, connections) – use try-with-resources.
- Mutable `HashMap` keys whose `hashCode` changes.
</details>

<details><summary>

## How do you troubleshoot an OutOfMemoryError or high memory in production?
</summary>

1. **Confirm the type** from the message: heap space, Metaspace, "GC overhead limit exceeded", "unable to create native thread".
2. **Capture a heap dump:** run with `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/dumps`, or `jcmd <pid> GC.heap_dump file.hprof`.
3. **Analyse** with Eclipse MAT or VisualVM: look at the dominator tree / biggest retained sizes and the path to GC roots.
4. **Check GC behaviour:** GC logs (`-Xlog:gc*`), or JVM metrics in Prometheus/Grafana (heap used after GC rising steadily = leak).
5. **In Kubernetes:** set `-XX:MaxRAMPercentage=75` so the heap respects the container limit; a pod `OOMKilled` with a healthy heap points to native memory or too-large heap settings.
6. Fix the root cause (bounded caches, streaming large results, pagination) rather than just raising `-Xmx`.
</details>

<details><summary>

## How do you diagnose high CPU or a hung Java service?
</summary>

1. `top -H -p <pid>` to find the hottest thread id; convert it to hex.
2. `jstack <pid>` (or `jcmd <pid> Thread.print`) and find that hex `nid` to see its stack.
3. Take 3 thread dumps a few seconds apart: the same stack every time = hot loop or stuck call.
4. Look for `BLOCKED` threads waiting on the same lock (contention) or "Found one Java-level deadlock".
5. Use a profiler (async-profiler, JFR: `jcmd <pid> JFR.start duration=60s filename=rec.jfr`) for CPU flame graphs.

Typical culprits: infinite loops, regex backtracking, excessive GC (check GC time), synchronized hot paths, thread-pool exhaustion waiting on a slow downstream.
</details>

<details><summary>

## Explain class loading and the delegation model.
</summary>

Class loaders form a hierarchy:

1. **Bootstrap** loader: core classes (`java.lang.*`) from the JDK.
2. **Platform** (formerly Extension) loader: other JDK modules.
3. **Application (System)** loader: your classpath.

**Parent delegation:** a loader first asks its parent; it loads the class itself only if the parent can't. This stops anyone replacing `java.lang.String` with a fake one.

Phases: **Loading** → **Linking** (verify, prepare static fields with defaults, resolve) → **Initialization** (run static initializers, on first active use).

```java
System.out.println(String.class.getClassLoader());        // null (bootstrap)
System.out.println(MyService.class.getClassLoader());     // app class loader
```

`ClassNotFoundException`: class not found when loaded by name at runtime (`Class.forName`). `NoClassDefFoundError`: class was present at compile time but missing (or failed static init) at runtime.
</details>

<details><summary>

## What is the difference between strong, soft, weak and phantom references?
</summary>

- **Strong:** normal reference; never collected while reachable.
- **Soft** (`SoftReference`): collected only when memory is low. Used for memory-sensitive caches.
- **Weak** (`WeakReference`): collected at the next GC if no strong refs exist. `WeakHashMap` keys are weak.
- **Phantom** (`PhantomReference`): `get()` always returns null; used with a `ReferenceQueue` for cleanup after collection (`Cleaner`).

```java
Map<Object, String> meta = new WeakHashMap<>();
Object key = new Object();
meta.put(key, "data");
key = null;           // after next GC the entry disappears
```
</details>

<details><summary>

## What is JIT compilation?
</summary>

The JVM starts by **interpreting** bytecode. Methods that run often ("hot") are compiled to native machine code by the **Just-In-Time** compiler (C1 quickly, then C2 with heavy optimisations such as inlining, escape analysis and loop unrolling). That's why Java services are slower right after startup ("warm-up") and why benchmarks must warm up first (use JMH).
</details>
