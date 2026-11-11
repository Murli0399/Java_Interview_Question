<details><summary>

## [Easy] What is the difference between Iterator and ListIterator?
</summary>

| | `Iterator` | `ListIterator` |
|---|---|---|
| Works on | Any `Collection` | Only `List` |
| Direction | Forward only | **Forward and backward** (`hasPrevious`, `previous`) |
| Modify while iterating | `remove()` | `remove()`, **`set()`**, **`add()`** |
| Position | No index | `nextIndex()`, `previousIndex()` |
| Start position | Beginning | Any index: `list.listIterator(i)` |

```java
List<String> names = new ArrayList<>(List.of("asha", "ravi", "kiran"));
ListIterator<String> it = names.listIterator();
while (it.hasNext()) {
	String n = it.next();
	it.set(n.toUpperCase());           // replace in place
	if (n.equals("ravi")) it.add("MEENA");   // insert after current
}
System.out.println(names);              // [ASHA, RAVI, MEENA, KIRAN]
```

Modifying the list directly (not through the iterator) during iteration throws `ConcurrentModificationException`.
</details>

<details><summary>

## [Medium] What is the time complexity of common collection operations?
</summary>

| Collection | get / access | add | remove | contains / search | Ordering |
|---|---|---|---|---|---|
| `ArrayList` | O(1) by index | O(1) amortised at end, O(n) in middle | O(n) | O(n) | Insertion |
| `LinkedList` | O(n) | O(1) at ends | O(1) at ends, O(n) to find | O(n) | Insertion |
| `ArrayDeque` | – | O(1) at ends | O(1) at ends | O(n) | Insertion |
| `HashSet` / `HashMap` | O(1) average (O(log n) worst, treeified buckets) | O(1) avg | O(1) avg | O(1) avg | None |
| `LinkedHashSet` / `LinkedHashMap` | O(1) avg | O(1) avg | O(1) avg | O(1) avg | Insertion (or access) |
| `TreeSet` / `TreeMap` | O(log n) | O(log n) | O(log n) | O(log n) | Sorted |
| `PriorityQueue` | O(1) `peek` | O(log n) `offer` | O(log n) `poll`, O(n) arbitrary remove | O(n) | Heap (only the head is ordered) |
| `ConcurrentHashMap` | O(1) avg | O(1) avg | O(1) avg | O(1) avg | None |

In an interview, mention the assumptions: hash-based O(1) depends on a good `hashCode()`; `ArrayList.add` is amortised because the array occasionally resizes.
</details>

<details><summary>

## [Medium] What is the difference between List.of(), Arrays.asList() and Collections.unmodifiableList()?
</summary>

| | `List.of(...)` (Java 9) | `Arrays.asList(...)` | `Collections.unmodifiableList(list)` |
|---|---|---|---|
| Add / remove | ❌ `UnsupportedOperationException` | ❌ (fixed size) | ❌ |
| `set(i, x)` | ❌ | ✅ (writes through to the array) | ❌ |
| Nulls | ❌ `NullPointerException` | ✅ | ✅ (if the source has them) |
| Backed by | Its own internal storage (truly immutable) | The original **array** | The original **list** – a read-only **view** |
| Reflects later changes to the source? | No | Array changes show in the list | **Yes** – changes to the original list show through |

```java
List<String> source = new ArrayList<>(List.of("a", "b"));
List<String> view = Collections.unmodifiableList(source);
List<String> copy = List.copyOf(source);    // immutable snapshot

source.add("c");
System.out.println(view);   // [a, b, c] - view sees the change
System.out.println(copy);   // [a, b]    - snapshot doesn't
```

For a truly immutable copy, use `List.copyOf(...)` or `Stream.toList()`.
</details>

<details><summary>

## [Medium] How does HashSet work internally?
</summary>

A `HashSet` is backed by a **`HashMap`**. Each element you add is stored as a **key** in that map, with a shared dummy object (`PRESENT`) as the value.

- `add(e)` → `map.put(e, PRESENT)`; returns `true` if the key wasn't already there.
- `contains(e)` → `map.containsKey(e)`.
- `remove(e)` → `map.remove(e)`.

So uniqueness comes from `hashCode()` and `equals()` of the elements, exactly like `HashMap` keys. If you put mutable objects in a set and then change fields used in `hashCode()`, `contains()` can no longer find them. `LinkedHashSet` is backed by a `LinkedHashMap`, and `TreeSet` by a `TreeMap`.
</details>

<details><summary>

## [Medium] How do you choose the right collection?
</summary>

| Need | Choose |
|---|---|
| Ordered list, fast index access (most common) | `ArrayList` |
| Queue / stack / deque | `ArrayDeque` |
| Unique elements, fast lookup | `HashSet` |
| Unique elements, keep insertion order | `LinkedHashSet` |
| Unique elements, sorted, range queries | `TreeSet` |
| Key-value lookup | `HashMap` |
| Key-value with insertion order or LRU cache | `LinkedHashMap` |
| Sorted keys, floor/ceiling lookups | `TreeMap` |
| Always get the min/max (top-K, scheduling) | `PriorityQueue` |
| Keys are enums | `EnumMap` / `EnumSet` |
| Shared between threads | `ConcurrentHashMap`, `CopyOnWriteArrayList` (read-heavy), `ConcurrentLinkedQueue`, `BlockingQueue` (producer-consumer) |
| Fixed data that must not change | `List.of`, `Set.of`, `Map.of`, `List.copyOf` |

Program to the interface (`List<String> names = new ArrayList<>()`), so you can change the implementation later.
</details>

<details><summary>

## [Hard] What are EnumMap, WeakHashMap and IdentityHashMap used for?
</summary>

- **`EnumMap<K extends Enum<K>, V>`** – keys are enum constants; stored internally as an **array indexed by ordinal**, so it's very fast and compact, and iterates in enum declaration order. Use it whenever keys are an enum (e.g. counts per `OrderStatus`). `EnumSet` is the matching set (a bit vector).
- **`WeakHashMap`** – keys are held by **weak references**: when a key object is no longer referenced anywhere else, its entry is removed automatically after GC. Used for caches/metadata attached to objects whose lifecycle you don't control. Note that `String` literals and boxed small integers are never collected, so they're bad keys here.
- **`IdentityHashMap`** – compares keys with **`==` instead of `equals()`**. Used in frameworks for object-graph traversal (serialization, deep copy, cycle detection) where two equal but distinct objects must be treated separately.

```java
EnumMap<DayOfWeek, Integer> shifts = new EnumMap<>(DayOfWeek.class);
shifts.put(DayOfWeek.MONDAY, 3);

Map<String, Integer> identity = new IdentityHashMap<>();
identity.put(new String("k"), 1);
identity.put(new String("k"), 2);
System.out.println(identity.size());   // 2 - different objects, even though equal
```
</details>
