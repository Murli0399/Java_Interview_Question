# Low-Level Design (LLD) Problems

How to answer: 1) clarify requirements, 2) list classes and relationships, 3) code the core methods, 4) discuss concurrency and extension.

<details><summary>

## Design an LRU cache with O(1) get and put
</summary>

**Practice:** [LeetCode 146](https://leetcode.com/problems/lru-cache/)

**Approach:** `HashMap` for O(1) lookup + doubly linked list for recency (head = most recent, tail = least recent). Sentinel head/tail nodes remove null checks.

```java
class LRUCache {
    private class Node {
        int key, val; Node prev, next;
        Node(int k, int v) { key = k; val = v; }
    }

    private final int capacity;
    private final Map<Integer, Node> map = new HashMap<>();
    private final Node head = new Node(0, 0), tail = new Node(0, 0);

    LRUCache(int capacity) {
        this.capacity = capacity;
        head.next = tail; tail.prev = head;
    }

    public int get(int key) {
        Node n = map.get(key);
        if (n == null) return -1;
        remove(n); addFirst(n);
        return n.val;
    }

    public void put(int key, int val) {
        Node n = map.get(key);
        if (n != null) { n.val = val; remove(n); addFirst(n); return; }
        if (map.size() == capacity) {
            Node lru = tail.prev;
            remove(lru);
            map.remove(lru.key);
        }
        n = new Node(key, val);
        addFirst(n);
        map.put(key, n);
    }

    private void remove(Node n) { n.prev.next = n.next; n.next.prev = n.prev; }
    private void addFirst(Node n) { n.next = head.next; n.prev = head; head.next.prev = n; head.next = n; }
}
```

**Example:** capacity 2: `put(1,1), put(2,2), get(1)=1, put(3,3)` evicts 2, `get(2)=-1`.

**Follow-ups:**
- Quick version: `LinkedHashMap` with `accessOrder = true` + `removeEldestEntry` (see `04-collections`).
- Thread safety: `synchronized` methods or a `ReentrantLock`; at scale, striped locks. In production use Caffeine or Redis.
- TTL: store an expiry timestamp per node and check it on `get`.
</details>

<details><summary>

## Design a parking lot
</summary>

**Requirements to state:** multiple floors; spot sizes small/medium/large; vehicles bike/car/truck; ticket on entry; charge on exit by duration; show free spots.

**Classes:**
- `ParkingLot`: holds spots; `park(Vehicle)` → `Ticket`, `unpark(Ticket)` → amount
- `Spot`: id, `SpotSize`, current vehicle
- `Vehicle` (abstract) → `Bike`, `Car`, `Truck`, each knows its required `SpotSize`
- `Ticket`: id, vehicle, spot, entry time
- `PricingStrategy` (interface) → `HourlyPricing`, `WeekendPricing` (Strategy pattern)

```java
enum SpotSize { SMALL, MEDIUM, LARGE }

abstract class Vehicle {
    final String plate;
    Vehicle(String plate) { this.plate = plate; }
    abstract SpotSize size();
}
class Car extends Vehicle {
    Car(String p) { super(p); }
    SpotSize size() { return SpotSize.MEDIUM; }
}

class Spot {
    final String id; final SpotSize size; Vehicle vehicle;
    Spot(String id, SpotSize size) { this.id = id; this.size = size; }
    boolean isFree() { return vehicle == null; }
}

record Ticket(String id, Vehicle vehicle, Spot spot, Instant entry) {}

interface PricingStrategy { long price(Duration parked); }

class HourlyPricing implements PricingStrategy {
    public long price(Duration d) { return Math.max(1, (d.toMinutes() + 59) / 60) * 40; } // Rs 40/hour, rounded up
}

class ParkingLot {
    private final List<Spot> spots;
    private final PricingStrategy pricing;

    ParkingLot(List<Spot> spots, PricingStrategy pricing) { this.spots = spots; this.pricing = pricing; }

    synchronized Ticket park(Vehicle v) {
        Spot s = spots.stream()
            .filter(x -> x.isFree() && x.size == v.size())
            .findFirst()
            .orElseThrow(() -> new IllegalStateException("Lot full"));
        s.vehicle = v;
        return new Ticket(UUID.randomUUID().toString(), v, s, Instant.now());
    }

    synchronized long unpark(Ticket t) {
        t.spot().vehicle = null;
        return pricing.price(Duration.between(t.entry(), Instant.now()));
    }
}
```

**Points to say out loud:**
- Strategy keeps pricing open for extension (Open/Closed principle).
- `synchronized` stops two cars getting the same spot; at scale use per-floor locks or a DB row lock.
- Let a bike take a larger spot if no small one is free: put that rule in a `SpotAllocationStrategy`.
- Free-spot display: keep a counter per size, updated on park/unpark, instead of scanning.
</details>

<details><summary>

## Design a rate limiter (token bucket)
</summary>

**Requirement:** allow at most N requests per second per user, with short bursts allowed.

```java
class TokenBucket {
    private final long capacity;
    private final double refillPerNano;
    private double tokens;
    private long lastRefill;

    TokenBucket(long capacity, long refillPerSecond) {
        this.capacity = capacity;
        this.refillPerNano = refillPerSecond / 1_000_000_000.0;
        this.tokens = capacity;
        this.lastRefill = System.nanoTime();
    }

    synchronized boolean tryAcquire() {
        long now = System.nanoTime();
        tokens = Math.min(capacity, tokens + (now - lastRefill) * refillPerNano);
        lastRefill = now;
        if (tokens >= 1) { tokens -= 1; return true; }
        return false;
    }
}

class RateLimiter {
    private final Map<String, TokenBucket> buckets = new ConcurrentHashMap<>();
    boolean allow(String userId) {
        return buckets.computeIfAbsent(userId, id -> new TokenBucket(10, 5)).tryAcquire();
    }
}
```

**Distributed version:** keep the counter in Redis (`INCR` + `EXPIRE` for fixed window, or a Lua script for token bucket) so all instances share limits.
</details>
