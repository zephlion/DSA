# Java DSA Guide — HashMap

*A comprehensive, in-depth guide to `HashMap` in Java, one of the most widely used data structures for key–value storage.*

---

## Table of contents

1. [Introduction](#introduction)
2. [HashMap basics](#hashmap-basics)

   * [What is HashMap?](#what-is-hashmap)
   * [Key characteristics](#key-characteristics)
   * [Internal implementation](#internal-implementation)
3. [HashMap operations](#hashmap-operations)

   * [Creation](#creation)
   * [Adding entries](#adding-entries)
   * [Accessing and modifying](#accessing-and-modifying)
   * [Removing entries](#removing-entries)
   * [Iteration](#iteration)
   * [Searching](#searching)
4. [Time & space complexity](#time--space-complexity)
5. [Collision handling](#collision-handling)
6. [HashMap vs Hashtable vs ConcurrentHashMap](#hashmap-vs-hashtable-vs-concurrenthashmap)
7. [Examples and code snippets](#examples-and-code-snippets)
8. [Advanced topics](#advanced-topics)

   * [Load factor and resizing](#load-factor-and-resizing)
   * [Custom objects as keys](#custom-objects-as-keys)
   * [Null keys and values](#null-keys-and-values)
   * [Thread safety](#thread-safety)
9. [Practice problems](#practice-problems)
10. [Cheat sheet](#cheat-sheet)

---

# Introduction

`HashMap` is a part of the Java Collections Framework. It stores **key–value pairs** and allows fast retrieval using hashing. It is the go-to data structure for most mapping needs in Java.

---

# HashMap basics

## What is HashMap?

* Implements `Map<K,V>` interface.
* Stores key–value mappings with unique keys.
* Average O(1) time complexity for insert, delete, and lookup.

## Key characteristics

* Allows **one null key** and multiple null values.
* Does **not maintain insertion order** (use `LinkedHashMap` if ordering needed).
* Backed by an array of buckets, each bucket stores a linked list or tree of entries.

## Internal implementation

* Keys are hashed via `hashCode()`.
* Hash value determines bucket index.
* Java 8+: if bucket chain grows beyond threshold, linked list converted to balanced tree (O(log n)).

---

# HashMap operations

## Creation

```java
Map<String, Integer> map = new HashMap<>();
Map<String, Integer> mapWithCapacity = new HashMap<>(32, 0.75f);
```

## Adding entries

```java
map.put("apple", 3);
map.put("banana", 5);
```

## Accessing and modifying

```java
int val = map.get("apple");
map.put("apple", 10); // update
map.getOrDefault("pear", 0);
```

## Removing entries

```java
map.remove("banana");
map.clear();
```

## Iteration

```java
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " => " + entry.getValue());
}

map.forEach((k, v) -> System.out.println(k + ": " + v));
```

## Searching

```java
boolean exists = map.containsKey("apple");
boolean hasValue = map.containsValue(10);
```

---

# Time & space complexity

* Insert: O(1) average
* Search: O(1) average
* Delete: O(1) average
* Worst case (all collisions): O(n)
* Space: O(n)

---

# Collision handling

* Uses **separate chaining** (linked lists).
* Since Java 8: if a bucket’s chain > 8, structure becomes a **red–black tree**.
* Reduces worst-case complexity from O(n) to O(log n).

---

# HashMap vs Hashtable vs ConcurrentHashMap

| Feature          | HashMap                      | Hashtable          | ConcurrentHashMap                     |
| ---------------- | ---------------------------- | ------------------ | ------------------------------------- |
| Thread-safe      | No                           | Yes (synchronized) | Yes (concurrent locks)                |
| Null keys/values | 1 null key, many null values | No nulls           | No null keys, null values not allowed |
| Performance      | Faster                       | Slower             | Fast under concurrency                |

---

# Examples and code snippets

### Word frequency counter

```java
String text = "apple banana apple";
Map<String, Integer> freq = new HashMap<>();
for (String word : text.split(" ")) {
    freq.put(word, freq.getOrDefault(word, 0) + 1);
}
System.out.println(freq);
```

### Caching with HashMap

```java
Map<Integer, String> cache = new HashMap<>();
cache.put(1, "one");
cache.put(2, "two");
System.out.println(cache.get(1));
```

---

# Advanced topics

## Load factor and resizing

* Default capacity = 16.
* Default load factor = 0.75.
* When size > capacity \* load factor, table doubles in size.

## Custom objects as keys

```java
class Person {
    String name;
    int id;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person p = (Person) o;
        return id == p.id && Objects.equals(name, p.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, id);
    }
}

Map<Person, Integer> map = new HashMap<>();
map.put(new Person("Alice", 1), 25);
```

## Null keys and values

* One null key allowed.
* Multiple null values allowed.

```java
map.put(null, 100);
map.put("pear", null);
```

## Thread safety

* Use `Collections.synchronizedMap(map)` for synchronization.
* Or use `ConcurrentHashMap` for better performance in concurrent environments.

---

# Practice problems

1. Implement frequency counter using HashMap.
2. Find first non-repeating character in a string.
3. Design LRU cache using LinkedHashMap.
4. Group words by anagrams.
5. Find two numbers that sum to target using HashMap.

---

# Cheat sheet

* Insert/get/remove: O(1) average.
* Worst-case: O(log n) with tree bins (Java 8+).
* Allows null key (1) and multiple null values.
* Not thread-safe.