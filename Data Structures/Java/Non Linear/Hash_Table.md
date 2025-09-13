# Hash Table - An In-Depth Guide (Java Version)

## 1. Introduction

Hash tables (also called hash maps or dictionaries) are a fundamental data structure that provide efficient average-case lookup, insertion, and deletion. They map keys to values using a hash function that computes an index into an internal array (bucket), enabling near-constant time access on average.

## 2. What is a Hash Table?

A hash table stores key-value pairs. For each key, a **hash function** computes an index (bucket) where the value is stored. When multiple keys map to the same bucket—**collisions**—a collision resolution strategy is used (chaining, open addressing, etc.).

Example using Java's built-in `HashMap`:

```java
import java.util.*;

public class HashTableExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("apple", 3);
        map.put("banana", 5);

        System.out.println(map.get("apple")); // 3
        map.put("cherry", 7); // insert
    }
}
```

## 3. Properties of Hash Tables

* **Average-case O(1)** for lookup, insertion, and deletion.
* **Unordered:** No guarantee of order (use `LinkedHashMap` or `TreeMap` for order variants).
* **Hashable keys:** Keys must implement `hashCode()` and `equals()` consistently.
* **Load factor:** Ratio of stored elements to bucket array size; controls resizing.

## 4. Advantages of Hash Tables

* Extremely fast average lookups and updates.
* Flexible key types (Strings, numbers, custom immutable objects).
* Building block for caching, indexing, sets.

## 5. Disadvantages of Hash Tables

* Worst-case O(n) operations under pathological collisions or poor hash functions.
* Extra memory overhead.
* No natural ordering.
* More complex for ordered traversal—trees are better.

## 6. Types and Collision Resolution Strategies

* **Chaining (Separate Chaining):** Each bucket holds a linked list (or dynamic array).
* **Open Addressing:** All entries stored in the bucket array; probe for next free slot.
* **Advanced:** Cuckoo hashing, hopscotch, etc.

## 7. Common Operations

### 7.1 Simple usage with `HashMap`

```java
import java.util.*;

public class HashMapUsage {
    public static void main(String[] args) {
        Map<String, String> phone = new HashMap<>();

        // create
        phone.put("alice", "555-1234");
        phone.put("bob", "555-5678");

        // lookup
        System.out.println(phone.get("alice"));     // 555-1234
        System.out.println(phone.getOrDefault("carol", null)); // null if not found

        // insert/update
        phone.put("dave", "555-9999");

        // delete
        phone.remove("bob");

        // iterate
        for (Map.Entry<String, String> entry : phone.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}
```

---

### 7.2 Implementing a simple hash table with chaining

```java
import java.util.*;

class HashTableChaining<K, V> {
    private List<Entry<K, V>>[] buckets;
    private int capacity;
    private int size;

    static class Entry<K, V> {
        K key;
        V value;
        Entry(K key, V value) {
            this.key = key;
            this.value = value;
        }
    }

    @SuppressWarnings("unchecked")
    public HashTableChaining(int capacity) {
        this.capacity = capacity;
        this.buckets = new LinkedList[capacity];
        for (int i = 0; i < capacity; i++) {
            buckets[i] = new LinkedList<>();
        }
        this.size = 0;
    }

    private int hash(K key) {
        return Math.abs(key.hashCode()) % capacity;
    }

    public void put(K key, V value) {
        int idx = hash(key);
        for (Entry<K, V> entry : buckets[idx]) {
            if (entry.key.equals(key)) {
                entry.value = value;
                return;
            }
        }
        buckets[idx].add(new Entry<>(key, value));
        size++;
    }

    public V get(K key) {
        int idx = hash(key);
        for (Entry<K, V> entry : buckets[idx]) {
            if (entry.key.equals(key)) {
                return entry.value;
            }
        }
        return null;
    }

    public void remove(K key) {
        int idx = hash(key);
        Iterator<Entry<K, V>> it = buckets[idx].iterator();
        while (it.hasNext()) {
            Entry<K, V> entry = it.next();
            if (entry.key.equals(key)) {
                it.remove();
                size--;
                return;
            }
        }
    }
}
```

---

### 7.3 Open Addressing (Linear Probing)

```java
class HashTableLinearProbing<K, V> {
    private Object[] keys;
    private Object[] values;
    private int capacity;
    private int size;

    public HashTableLinearProbing(int capacity) {
        this.capacity = capacity;
        this.keys = new Object[capacity];
        this.values = new Object[capacity];
        this.size = 0;
    }

    private int hash(K key) {
        return Math.abs(key.hashCode()) % capacity;
    }

    public void put(K key, V value) {
        int idx = hash(key);
        int start = idx;
        while (keys[idx] != null && !keys[idx].equals(key)) {
            idx = (idx + 1) % capacity;
            if (idx == start) throw new RuntimeException("HashTable full");
        }
        if (keys[idx] == null) size++;
        keys[idx] = key;
        values[idx] = value;
    }

    @SuppressWarnings("unchecked")
    public V get(K key) {
        int idx = hash(key);
        int start = idx;
        while (keys[idx] != null) {
            if (keys[idx].equals(key)) return (V) values[idx];
            idx = (idx + 1) % capacity;
            if (idx == start) break;
        }
        return null;
    }

    public void remove(K key) {
        int idx = hash(key);
        int start = idx;
        while (keys[idx] != null) {
            if (keys[idx].equals(key)) {
                keys[idx] = null;
                values[idx] = null;
                size--;
                return;
            }
            idx = (idx + 1) % capacity;
            if (idx == start) break;
        }
    }
}
```

## 8. Hash Functions and Key Requirements

* Good hash functions distribute keys uniformly.
* In Java, `hashCode()` is used with `equals()`.
* Keys should be immutable (e.g., String, Integer).

Example custom key:

```java
class Point {
    int x, y;
    Point(int x, int y) { this.x = x; this.y = y; }
```
