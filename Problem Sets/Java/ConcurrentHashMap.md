# Java DSA Guide — ConcurrentHashMap

*A comprehensive, in-depth guide to `ConcurrentHashMap` in Java, a thread-safe implementation of HashMap designed for concurrent applications.*

---

## Table of contents

1. [Introduction](#introduction)
2. [ConcurrentHashMap basics](#concurrenthashmap-basics)

   * [What is ConcurrentHashMap?](#what-is-concurrenthashmap)
   * [Key characteristics](#key-characteristics)
   * [Internal implementation](#internal-implementation)
3. [ConcurrentHashMap operations](#concurrenthashmap-operations)

   * [Creation](#creation)
   * [Adding elements](#adding-elements)
   * [Accessing](#accessing)
   * [Updating](#updating)
   * [Removing elements](#removing-elements)
   * [Iteration](#iteration)
   * [Bulk operations](#bulk-operations)
4. [Time & space complexity](#time--space-complexity)
5. [HashMap vs ConcurrentHashMap vs Hashtable](#hashmap-vs-concurrenthashmap-vs-hashtable)
6. [Examples and code snippets](#examples-and-code-snippets)
7. [Advanced topics](#advanced-topics)

   * [Lock striping](#lock-striping)
   * [Concurrent updates](#concurrent-updates)
   * [Null handling](#null-handling)
   * [Performance considerations](#performance-considerations)
8. [Practice problems](#practice-problems)
9. [Cheat sheet](#cheat-sheet)
10. [Further reading](#further-reading)

---

# Introduction

`ConcurrentHashMap` is a thread-safe variant of `HashMap` introduced in Java 1.5 as part of `java.util.concurrent`. It is designed for highly concurrent environments, allowing safe access and updates by multiple threads without requiring explicit synchronization.

---

# ConcurrentHashMap basics

## What is ConcurrentHashMap?

* A concurrent, scalable implementation of `Map`.
* Allows multiple threads to read and update simultaneously.
* Avoids global synchronization bottlenecks of `Hashtable`.

## Key characteristics

* No `null` keys or `null` values allowed.
* Thread-safe without explicit synchronization.
* Better performance than synchronized `HashMap` or `Hashtable`.

## Internal implementation

* Prior to Java 8: Used **segment-based locking** (lock striping).
* Since Java 8: Uses **CAS (Compare-And-Swap)**, `synchronized` blocks, and **tree bins** for handling collisions.

---

# ConcurrentHashMap operations

## Creation

```java
ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();
ConcurrentHashMap<Integer, String> mapWithCapacity = new ConcurrentHashMap<>(32);
```

## Adding elements

```java
map.put(1, "Alice");
map.putIfAbsent(2, "Bob");
```

## Accessing

```java
String val = map.get(1);
```

## Updating

```java
map.replace(1, "Alice", "Alicia");
map.compute(2, (k, v) -> v + " Smith");
map.merge(3, "Charlie", (oldVal, newVal) -> oldVal + ", " + newVal);
```

## Removing elements

```java
map.remove(2);
map.remove(1, "Alicia");
```

## Iteration

```java
for (Map.Entry<Integer, String> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}

map.forEach(1, (k,v) -> System.out.println(k + ":" + v));
```

## Bulk operations

* `forEach`
* `search`
* `reduce`

```java
map.forEach(2, (k,v) -> System.out.println(k + "=" + v));
String found = map.search(2, (k,v) -> v.startsWith("A") ? v : null);
```

---

# Time & space complexity

* Get: O(1) average
* Put: O(1) average
* Remove: O(1) average
* Iteration: O(n)
* Space: O(n)

---

# HashMap vs ConcurrentHashMap vs Hashtable

| Feature                      | HashMap      | ConcurrentHashMap              | Hashtable     |
| ---------------------------- | ------------ | ------------------------------ | ------------- |
| Thread-safe                  | ❌ No         | ✅ Yes                          | ✅ Yes         |
| Null keys                    | 1 allowed    | ❌ Not allowed                  | ❌ Not allowed |
| Null values                  | Many allowed | ❌ Not allowed                  | ❌ Not allowed |
| Performance (multi-threaded) | Poor         | Excellent                      | Poor          |
| Locking strategy             | None         | Fine-grained (CAS + bin locks) | Global lock   |

---

# Examples and code snippets

### Counting word frequencies concurrently

```java
ConcurrentHashMap<String, Integer> freq = new ConcurrentHashMap<>();

List<String> words = Arrays.asList("apple", "banana", "apple", "orange", "banana");

words.parallelStream().forEach(word ->
    freq.merge(word, 1, Integer::sum)
);

System.out.println(freq);
```

### Safe concurrent updates

```java
ExecutorService service = Executors.newFixedThreadPool(3);
ConcurrentHashMap<Integer, String> cmap = new ConcurrentHashMap<>();

for (int i = 0; i < 5; i++) {
    final int key = i;
    service.submit(() -> cmap.put(key, "Val" + key));
}

service.shutdown();
service.awaitTermination(1, TimeUnit.SECONDS);
System.out.println(cmap);
```

---

# Advanced topics

## Lock striping

* Pre-Java 8: Map divided into segments, each with its own lock.
* Java 8+: Replaced with finer-grained mechanisms.

## Concurrent updates

* Uses CAS to minimize locking.
* Collisions handled with linked lists or tree bins.

## Null handling

* Does not allow `null` keys or values to avoid ambiguity in concurrent operations.

## Performance considerations

* Scales well under high concurrency.
* Use `putIfAbsent`, `compute`, `merge` for atomic updates.

---

# Practice problems

1. Implement word frequency counter with `ConcurrentHashMap`.
2. Design thread-safe cache using `ConcurrentHashMap`.
3. Demonstrate atomic updates with `computeIfAbsent`.
4. Parallel reduce operation on values in a map.
5. Compare performance of `Hashtable` vs `ConcurrentHashMap`.

---

# Cheat sheet

* Thread-safe `HashMap` alternative.
* No `null` keys or values.
* Atomic operations: `putIfAbsent`, `compute`, `merge`.
* Optimized for concurrent reads and updates.
* Use bulk operations (`forEach`, `search`, `reduce`) for parallelism.