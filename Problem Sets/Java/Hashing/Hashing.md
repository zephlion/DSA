# Java DSA Guide — Hashing

*A comprehensive, in-depth guide to hashing for Java developers preparing for interviews or building production systems.*

---

## Table of contents

1. [Introduction](#introduction)
2. [Hashing basics](#hashing-basics)

   * [What is hashing?](#what-is-hashing)
   * [Hash function properties](#hash-function-properties)
   * [Hash table & collision resolution](#hash-table--collision-resolution)
   * [Load factor & resizing](#load-factor--resizing)
3. [Hashing in Java](#hashing-in-java)

   * [HashMap](#hashmap)
   * [HashSet](#hashset)
   * [LinkedHashMap](#linkedhashmap)
   * [TreeMap vs HashMap](#treemap-vs-hashmap)
   * [ConcurrentHashMap](#concurrenthashmap)
4. [Designing hash functions in Java](#designing-hash-functions-in-java)

   * [hashCode and equals contract](#hashcode-and-equals-contract)
   * [Good practices](#good-practices)
5. [Common hashing-based algorithms](#common-hashing-based-algorithms)

   * [Two-sum](#two-sum)
   * [Group anagrams](#group-anagrams)
   * [Top K frequent elements](#top-k-frequent-elements)
   * [Longest substring without repeating characters](#longest-substring-without-repeating-characters)
   * [Contains duplicate](#contains-duplicate)
6. [Implementing a simple hash table](#implementing-a-simple-hash-table)
7. [Performance tuning](#performance-tuning)
8. [Practice problems](#practice-problems)
9. [Cheat sheet](#cheat-sheet)

---

# Introduction

Hashing is one of the most powerful techniques in computer science. It allows for average **O(1)** lookup, insertion, and deletion using hash tables. Java provides robust implementations (`HashMap`, `HashSet`, `ConcurrentHashMap`) that are used extensively in production systems and interview problems.

---

# Hashing basics

## What is hashing?

Hashing is the process of mapping data of arbitrary size (keys) to a fixed range of integers (hash codes). These integers are then used to determine where to store the key–value pair in a hash table.

## Hash function properties

A good hash function should:

* Be deterministic (same input → same hash).
* Distribute keys uniformly.
* Minimize collisions.
* Be fast to compute.

## Hash table & collision resolution

* **Collision**: when two keys map to the same bucket.
* **Chaining**: store colliding entries in a linked list or balanced tree.
* **Open addressing**: find another empty slot (linear probing, quadratic probing, double hashing).

## Load factor & resizing

* Load factor = `entries / buckets`.
* Default in Java: 0.75.
* When exceeded, table resizes (rehashing entries).

---

# Hashing in Java

## HashMap

* Stores key–value pairs.
* Average O(1) operations.
* Collisions handled by chaining, with trees for long chains (Java 8+).

Example:

```java
Map<String, Integer> map = new HashMap<>();
map.put("apple", 2);
map.put("banana", 3);
System.out.println(map.get("apple"));
```

## HashSet

* Backed by `HashMap`.
* Stores unique elements only.

```java
Set<Integer> set = new HashSet<>();
set.add(10);
set.add(20);
System.out.println(set.contains(10));
```

## LinkedHashMap

* Maintains insertion or access order.
* Useful for caches (e.g., LRU).

## TreeMap vs HashMap

* `TreeMap`: O(log n), sorted order.
* `HashMap`: O(1) average, unordered.

## ConcurrentHashMap

* Thread-safe implementation.
* Allows concurrent reads/writes without locking entire map.

---

# Designing hash functions in Java

## hashCode and equals contract

* If `a.equals(b)`, then `a.hashCode() == b.hashCode()`.
* If `a.hashCode() == b.hashCode()`, not necessarily `a.equals(b)`.

Example:

```java
public class Person {
    private final String name;
    private final int id;

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
```

## Good practices

* Use immutable keys.
* Prefer `Objects.hash` or `Arrays.hashCode`.
* Avoid expensive computations in `hashCode`.

---

# Common hashing-based algorithms

## Two-sum

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) return new int[] { map.get(complement), i };
        map.put(nums[i], i);
    }
    return null;
}
```

## Group anagrams

```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> map = new HashMap<>();
    for (String s : strs) {
        char[] arr = s.toCharArray();
        Arrays.sort(arr);
        String key = new String(arr);
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(s);
    }
    return new ArrayList<>(map.values());
}
```

## Top K frequent elements

```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums) freq.put(n, freq.getOrDefault(n, 0) + 1);

    PriorityQueue<Integer> heap = new PriorityQueue<>((a, b) -> freq.get(a) - freq.get(b));

    for (int n : freq.keySet()) {
        heap.add(n);
        if (heap.size() > k) heap.poll();
    }

    int[] res = new int[k];
    for (int i = k - 1; i >= 0; i--) res[i] = heap.poll();
    return res;
}
```

## Longest substring without repeating characters

```java
public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> map = new HashMap<>();
    int start = 0, max = 0;
    for (int i = 0; i < s.length(); i++) {
        char c = s.charAt(i);
        if (map.containsKey(c)) start = Math.max(start, map.get(c) + 1);
        map.put(c, i);
        max = Math.max(max, i - start + 1);
    }
    return max;
}
```

## Contains duplicate

```java
public boolean containsDuplicate(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for (int n : nums) if (!set.add(n)) return true;
    return false;
}
```

---

# Implementing a simple hash table

```java
public class SimpleHashMap<K, V> {
    private static class Node<K,V> {
        final K key; V value; Node<K,V> next;
        Node(K k, V v, Node<K,V> n) { key = k; value = v; next = n; }
    }

    private Node<K,V>[] buckets;
    private static final int DEFAULT_CAP = 16;
    private int size = 0;

    @SuppressWarnings("unchecked")
    public SimpleHashMap() { buckets = (Node<K,V>[]) new Node[DEFAULT_CAP]; }

    private int idx(Object key) {
        return (key == null) ? 0 : (key.hashCode() & 0x7fffffff) % buckets.length;
    }

    public V get(Object key) {
        int i = idx(key);
        for (Node<K,V> n = buckets[i]; n != null; n = n.next)
            if (Objects.equals(n.key, key)) return n.value;
        return null;
    }

    public void put(K key, V value) {
        int i = idx(key);
        for (Node<K,V> n = buckets[i]; n != null; n = n.next)
            if (Objects.equals(n.key, key)) { n.value = value; return; }
        buckets[i] = new Node<>(key, value, buckets[i]);
        size++;
    }
}
```

---

# Performance tuning

* Choose initial capacity if size is known.
* Keep load factor reasonable (default 0.75).
* Avoid poor `hashCode` implementations.
* Use primitive-specialized maps for efficiency.
* Use `ConcurrentHashMap` for concurrency.

---

# Practice problems

1. Two-sum
2. Group anagrams
3. Longest substring without repeating characters
4. Subarray sum equals k (prefix sum + HashMap)
5. LRU Cache using LinkedHashMap

---

# Cheat sheet

* HashMap get/put/remove: O(1) average
* Worst-case O(n) if poor hash or many collisions
* HashSet: uniqueness via HashMap
* LinkedHashMap: maintains order
* TreeMap: O(log n), sorted order
