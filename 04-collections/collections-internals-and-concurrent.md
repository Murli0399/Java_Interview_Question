# Collections: Internals, Queues and Concurrent Collections

<details><summary>

## How does HashMap work internally?
</summary>

A `HashMap` is an array of buckets (`Node<K,V>[] table`).

1. `put(key, value)` computes `hash = key.hashCode() ^ (h >>> 16)` (spreads high bits).
2. Bucket index = `(n - 1) & hash`, where `n` is the table length (always a power of 2).
3. If the bucket is empty, the node is placed there. If not, it walks the bucket: if a key is `equals()`, the value is replaced; otherwise the new node is appended.
4. Since Java 8, a bucket with more than **8** nodes (and table size ≥ 64) turns into a **red-black tree**, so worst-case lookup becomes O(log n) instead of O(n).
5. When `size > capacity * loadFactor` (default 16 × 0.75 = 12), the table **doubles** and entries are redistributed.

```java
Map<String, Integer> stock = new HashMap<>();
stock.put("apple", 10);     // hash("apple") -> bucket i
stock.put("apple", 15);     // same key -> value replaced, size stays 1
System.out.println(stock.get("apple")); // 15
```

**Interview follow-up:** If you override `equals()` but not `hashCode()`, two equal keys can land in different buckets and `get()` returns `null`.
</details>

<details><summary>

## What is the initial capacity and load factor of a collection?
</summary>

- **Initial capacity:** the number of buckets/slots created up front. `HashMap` default is 16; `ArrayList` creates a 10-slot array on the first `add`.
- **Load factor:** how full a hash table may get before it resizes. Default 0.75 balances memory against collisions.

If you know the size in advance, set the capacity to avoid repeated resizing:

```java
// expecting ~1,000 entries: 1000 / 0.75 ≈ 1334 -> next power of 2 is 2048
Map<Long, User> users = new HashMap<>(1334);
List<String> names = new ArrayList<>(1000);
```
</details>

<details><summary>

## Why must HashMap keys be immutable?
</summary>

The bucket is chosen from `hashCode()` at insertion time. If a mutable key changes after insertion, its hash changes and the map looks in the wrong bucket, so the entry is effectively lost.

```java
List<Integer> key = new ArrayList<>(List.of(1, 2));
Map<List<Integer>, String> map = new HashMap<>();
map.put(key, "value");
key.add(3);                       // hashCode changes
System.out.println(map.get(key)); // null - entry is "lost"
```

That is why `String`, `Integer` and records make good keys.
</details>

<details><summary>

## What is the difference between HashMap, LinkedHashMap and TreeMap?
</summary>

| | HashMap | LinkedHashMap | TreeMap |
|---|---|---|---|
| Order | None | Insertion (or access) order | Sorted by key |
| get/put | O(1) average | O(1) average | O(log n) |
| Null key | One allowed | One allowed | Not allowed (natural ordering) |
| Structure | Hash table | Hash table + doubly linked list | Red-black tree |

```java
Map<String, Integer> tree = new TreeMap<>(Map.of("b", 2, "a", 1, "c", 3));
System.out.println(tree);              // {a=1, b=2, c=3}
System.out.println(((TreeMap<String,Integer>) tree).firstKey()); // a
```
</details>

<details><summary>

## How do you build an LRU cache with LinkedHashMap?
</summary>

`LinkedHashMap` with `accessOrder = true` moves an entry to the end on every `get`. Override `removeEldestEntry` to evict when full.

```java
class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacity;

    LRUCache(int capacity) {
        super(capacity, 0.75f, true); // true = access order
        this.capacity = capacity;
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;
    }
}

LRUCache<Integer, String> cache = new LRUCache<>(2);
cache.put(1, "a"); cache.put(2, "b");
cache.get(1);          // 1 becomes most recent
cache.put(3, "c");     // evicts 2
System.out.println(cache.keySet()); // [1, 3]
```

Interviewers often ask for the manual version too (HashMap + doubly linked list); see `10-dsa-coding/lld-problems.md`.
</details>

<details><summary>

## What are the important interfaces related to the Queue interface?
</summary>

- `Queue<E>`: FIFO operations `offer`, `poll`, `peek` (return special values) and `add`, `remove`, `element` (throw exceptions).
- `Deque<E>`: double-ended queue; insert/remove at both ends. Works as a queue and as a stack.
- `BlockingQueue<E>`: waits when empty (`take`) or full (`put`); used for producer-consumer.
- `BlockingDeque<E>`: blocking version of `Deque`.
- `TransferQueue<E>`: producer can wait until a consumer receives the element (`transfer`).

```java
Queue<String> q = new ArrayDeque<>();
q.offer("a"); q.offer("b");
System.out.println(q.poll()); // a
System.out.println(q.peek()); // b
```
</details>

<details><summary>

## Explain the Deque interface.
</summary>

A `Deque` supports insertion and removal at both the head and tail. `ArrayDeque` is the recommended implementation for both stacks and queues: it is faster than `Stack` (synchronized, legacy) and `LinkedList` (node allocation per element).

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(1); stack.push(2);
System.out.println(stack.pop());   // 2 (LIFO)

Deque<Integer> queue = new ArrayDeque<>();
queue.offerLast(1); queue.offerLast(2);
System.out.println(queue.pollFirst()); // 1 (FIFO)
```

Note: `ArrayDeque` does not allow `null` elements.
</details>

<details><summary>

## What is a PriorityQueue?
</summary>

A queue that always returns the smallest element (by natural order or a `Comparator`). It is backed by a **binary heap**: `offer`/`poll` are O(log n), `peek` is O(1). Iteration order is **not** sorted.

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
for (int x : new int[]{5, 1, 8, 3}) { minHeap.offer(x); maxHeap.offer(x); }
System.out.println(minHeap.poll()); // 1
System.out.println(maxHeap.poll()); // 8
```

**Classic use:** top-K problems. Keep a min-heap of size K; the root is the K-th largest.

```java
int kthLargest(int[] nums, int k) {
    PriorityQueue<Integer> heap = new PriorityQueue<>();
    for (int n : nums) {
        heap.offer(n);
        if (heap.size() > k) heap.poll();
    }
    return heap.peek();
}
```
</details>

<details><summary>

## Explain the BlockingQueue interface and give implementations.
</summary>

`BlockingQueue` adds methods that wait: `put()` blocks when full, `take()` blocks when empty. It handles all the locking, which makes producer-consumer code simple.

| Implementation | Notes |
|---|---|
| `ArrayBlockingQueue` | Bounded, array-backed, one lock |
| `LinkedBlockingQueue` | Optionally bounded, separate put/take locks (higher throughput) |
| `PriorityBlockingQueue` | Unbounded, priority order |
| `DelayQueue` | Elements become available after a delay |
| `SynchronousQueue` | No capacity; each `put` waits for a `take` |

```java
BlockingQueue<String> queue = new ArrayBlockingQueue<>(10);

Thread producer = new Thread(() -> {
    try {
        for (int i = 0; i < 5; i++) queue.put("job-" + i);
    } catch (InterruptedException e) { Thread.currentThread().interrupt(); }
});

Thread consumer = new Thread(() -> {
    try {
        for (int i = 0; i < 5; i++) System.out.println("processed " + queue.take());
    } catch (InterruptedException e) { Thread.currentThread().interrupt(); }
});

producer.start(); consumer.start();
```

`ThreadPoolExecutor` uses a `BlockingQueue` internally to hold pending tasks.
</details>

<details><summary>

## Can you give an example of the NavigableMap interface?
</summary>

`NavigableMap` (implemented by `TreeMap`) adds closest-match lookups.

```java
NavigableMap<Integer, String> grades = new TreeMap<>();
grades.put(90, "A"); grades.put(75, "B"); grades.put(60, "C"); grades.put(0, "F");

System.out.println(grades.floorEntry(82).getValue()); // B  (largest key <= 82)
System.out.println(grades.ceilingKey(61));            // 75 (smallest key >= 61)
System.out.println(grades.headMap(75, false));        // {0=F, 60=C}
System.out.println(grades.descendingMap());           // {90=A, 75=B, 60=C, 0=F}
```

Real use: price slabs, time-based lookups ("which config was active at time T").
</details>

<details><summary>

## What are the important static methods in the Collections class?
</summary>

```java
List<Integer> nums = new ArrayList<>(List.of(5, 3, 9, 1));

Collections.sort(nums);                         // [1, 3, 5, 9]
Collections.reverse(nums);                      // [9, 5, 3, 1]
Collections.shuffle(nums);
int max = Collections.max(nums);                // 9
int freq = Collections.frequency(nums, 3);      // 1
Collections.swap(nums, 0, 1);
int idx = Collections.binarySearch(List.of(1, 3, 5), 3); // 1 (list must be sorted)

List<Integer> readOnly = Collections.unmodifiableList(nums);
List<Integer> syncList = Collections.synchronizedList(new ArrayList<>());
List<String> empty = Collections.emptyList();
List<String> filled = Collections.nCopies(3, "x"); // [x, x, x]
```
</details>

<details><summary>

## What is the difference between synchronized and concurrent collections?
</summary>

- **Synchronized collections** (`Collections.synchronizedMap`, `Vector`, `Hashtable`) wrap every method in one lock. Only one thread works at a time, and iteration still needs manual locking.
- **Concurrent collections** (`ConcurrentHashMap`, `CopyOnWriteArrayList`, `ConcurrentLinkedQueue`) use fine-grained locks or lock-free CAS, so many threads proceed in parallel, and iterators don't throw `ConcurrentModificationException`.

```java
Map<String, Integer> sync = Collections.synchronizedMap(new HashMap<>());
synchronized (sync) {                 // required while iterating
    for (String k : sync.keySet()) System.out.println(k);
}

Map<String, Integer> concurrent = new ConcurrentHashMap<>();
concurrent.merge("hits", 1, Integer::sum); // atomic, no external lock
```
</details>

<details><summary>

## How does ConcurrentHashMap work in Java 8+?
</summary>

- No segment locks any more (that was Java 7). The table is a plain array of nodes.
- Inserting into an **empty bucket** uses a lock-free **CAS**.
- Inserting into a non-empty bucket locks **only that bucket's first node** (`synchronized`).
- Reads (`get`) take no lock; fields are `volatile`, so readers see the latest values.
- Resizing is done cooperatively by multiple threads.
- `null` keys and values are **not allowed**, because `get()` returning `null` must mean "absent" unambiguously in concurrent code.

Use the atomic compound methods instead of check-then-act:

```java
ConcurrentHashMap<String, Integer> counts = new ConcurrentHashMap<>();

// WRONG: race between get and put
// if (!counts.containsKey(w)) counts.put(w, 1); else counts.put(w, counts.get(w) + 1);

counts.merge("java", 1, Integer::sum);                    // atomic increment
counts.computeIfAbsent("cache", k -> expensiveLoad(k));   // load once
```
</details>

<details><summary>

## Explain the copy-on-write approach.
</summary>

`CopyOnWriteArrayList` and `CopyOnWriteArraySet` create a **new copy of the underlying array on every write**. Readers iterate over an unchanging snapshot with no locking.

- Great when reads vastly outnumber writes (listener lists, config).
- Terrible for frequent writes (each write is O(n) copy).
- Iterators never throw `ConcurrentModificationException`, but they don't see later writes.

```java
List<String> listeners = new CopyOnWriteArrayList<>(List.of("a", "b"));
for (String l : listeners) {
    listeners.add("c"); // allowed; this loop still sees only [a, b]
}
System.out.println(listeners); // [a, b, c, c]
```
</details>

<details><summary>

## What is the compare-and-swap (CAS) approach?
</summary>

CAS is a CPU instruction: "set the value to `new` **only if** it is still `expected`", returning whether it succeeded. Threads retry in a loop instead of blocking on a lock. `AtomicInteger`, `ConcurrentHashMap` and `ConcurrentLinkedQueue` are built on it.

```java
AtomicInteger counter = new AtomicInteger();

// what incrementAndGet() does internally (simplified)
int prev, next;
do {
    prev = counter.get();
    next = prev + 1;
} while (!counter.compareAndSet(prev, next));
```

Trade-off: no blocking or deadlocks, but heavy contention means many retries. The **ABA problem** (value changes A→B→A) is solved with `AtomicStampedReference`.
</details>

<details><summary>

## What is a Lock? How is it different from synchronized?
</summary>

`java.util.concurrent.locks.Lock` (e.g. `ReentrantLock`) does what `synchronized` does, plus:

- `tryLock()` / `tryLock(timeout)`: give up instead of waiting forever (helps avoid deadlock)
- `lockInterruptibly()`: waiting can be interrupted
- Fairness option: longest-waiting thread goes first
- Multiple `Condition`s per lock (finer than `wait/notify`)
- `ReadWriteLock`: many readers or one writer

You must unlock in `finally`; `synchronized` releases automatically.

```java
private final ReentrantLock lock = new ReentrantLock();

void transfer(Account from, Account to, int amount) throws InterruptedException {
    if (lock.tryLock(1, TimeUnit.SECONDS)) {
        try {
            from.debit(amount);
            to.credit(amount);
        } finally {
            lock.unlock();
        }
    } else {
        throw new IllegalStateException("Could not acquire lock, retry later");
    }
}
```
</details>

<details><summary>

## When does a collection throw UnsupportedOperationException?
</summary>

When you modify a collection that doesn't support modification: `List.of()`, `Map.of()`, `Collections.unmodifiableList()`, or `Arrays.asList()` (fixed size: `set` works, `add`/`remove` don't).

```java
List<Integer> fixed = Arrays.asList(1, 2, 3);
fixed.set(0, 9);   // OK
fixed.add(4);      // UnsupportedOperationException

List<Integer> immutable = List.of(1, 2);
immutable.set(0, 5); // UnsupportedOperationException

List<Integer> mutable = new ArrayList<>(List.of(1, 2)); // copy to modify
mutable.add(3);      // OK
```
</details>

<details><summary>

## What is the difference between fail-fast and fail-safe iterators?
</summary>

- **Fail-fast** (`ArrayList`, `HashMap`): track a `modCount`; if the collection is structurally changed during iteration (other than via the iterator), they throw `ConcurrentModificationException`.
- **Fail-safe / weakly consistent** (`ConcurrentHashMap`, `CopyOnWriteArrayList`): iterate a snapshot or tolerate concurrent changes; never throw CME.

```java
List<Integer> list = new ArrayList<>(List.of(1, 2, 3, 4));

// for (Integer x : list) if (x % 2 == 0) list.remove(x);  // ConcurrentModificationException

Iterator<Integer> it = list.iterator();
while (it.hasNext()) if (it.next() % 2 == 0) it.remove(); // safe
// or simply:
list.removeIf(x -> x % 2 == 0);
```
</details>

<details><summary>

## What are atomic operations and atomic classes in Java?
</summary>

An atomic operation completes fully or not at all; no other thread can see it half-done. `count++` is **not** atomic (read, add, write). `java.util.concurrent.atomic` provides lock-free atomic classes:

- `AtomicInteger`, `AtomicLong`, `AtomicBoolean`, `AtomicReference`
- `LongAdder`: better than `AtomicLong` under heavy contention (spreads updates across cells)

```java
AtomicInteger requests = new AtomicInteger();
ExecutorService pool = Executors.newFixedThreadPool(4);
for (int i = 0; i < 1000; i++) pool.submit(requests::incrementAndGet);
pool.shutdown();
pool.awaitTermination(5, TimeUnit.SECONDS);
System.out.println(requests.get()); // always 1000

LongAdder hits = new LongAdder();
hits.increment();
System.out.println(hits.sum());
```
</details>

<details><summary>

## Comparable vs Comparator: how do you sort by multiple fields?
</summary>

`Comparable` defines one natural order inside the class (`compareTo`). `Comparator` defines external, swappable orders. Java 8 comparators chain cleanly:

```java
record Employee(String name, String dept, double salary) {}

List<Employee> emps = new ArrayList<>(List.of(
    new Employee("Asha", "Eng", 90_000),
    new Employee("Ravi", "Eng", 120_000),
    new Employee("Meena", "Sales", 70_000)));

emps.sort(Comparator.comparing(Employee::dept)
                    .thenComparing(Employee::salary, Comparator.reverseOrder())
                    .thenComparing(Employee::name));
// Eng/Ravi, Eng/Asha, Sales/Meena
```
</details>
