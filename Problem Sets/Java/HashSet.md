# Java DSA Guide — HashSet

*A comprehensive, in-depth guide to `HashSet` in Java, a widely used data structure for storing unique elements.*

---

## Table of contents

1. [Introduction](#introduction)
2. [HashSet basics](#hashset-basics)

   * [What is HashSet?](#what-is-hashset)
   * [Key characteristics](#key-characteristics)
   * [Internal implementation](#internal-implementation)
3. [HashSet operations](#hashset-operations)

   * [Creation](#creation)
   * [Adding elements](#adding-elements)
   * [Accessing](#accessing)
   * [Removing elements](#removing-elements)
   * [Iteration](#iteration)
   * [Searching](#searching)
4. [Time & space complexity](#time--space-complexity)
5. [HashSet vs HashMap vs TreeSet](#hashset-vs-hashmap-vs-treeset)
6. [Examples and code snippets](#examples-and-code-snippets)
7. [Advanced topics](#advanced-topics)

   * [Load factor and resizing](#load-factor-and-resizing)
   * [Custom objects in HashSet](#custom-objects-in-hashset)
   * [Null elements](#null-elements)
   * [Thread safety](#thread-safety)
8. [Practice problems](#practice-problems)
9. [Cheat sheet](#cheat-sheet)
10. [Further reading](#further-reading)

---

# Introduction

`HashSet` is a part of the Java Collections Framework. It represents a collection that contains **no duplicate elements** and is backed by a `HashMap` internally.

---

# HashSet basics

## What is HashSet?

* Implements the `Set` interface.
* Stores unique elements only.
* Order of elements is not guaranteed.
* Backed by a `HashMap` (keys stored with a dummy constant value).

## Key characteristics

* No duplicates allowed.
* Allows **one null element**.
* Average O(1) performance for basic operations.

## Internal implementation

* Internally uses `HashMap<E,Object>`.
* Every added element is stored as a key in the map with a dummy value (`PRESENT`).

---

# HashSet operations

## Creation

```java
Set<Integer> set = new HashSet<>();
Set<String> setWithCapacity = new HashSet<>(32, 0.75f);
```

## Adding elements

```java
set.add(10);
set.add(20);
set.add(10); // duplicate ignored
```

## Accessing

* No direct access by index (unlike `ArrayList`).
* Elements can only be iterated.

## Removing elements

```java
set.remove(20);
set.clear();
```

## Iteration

```java
for (int val : set) System.out.println(val);

Iterator<Integer> it = set.iterator();
while (it.hasNext()) System.out.println(it.next());
```

## Searching

```java
boolean exists = set.contains(10);
```

---

# Time & space complexity

* Insert: O(1) average
* Search: O(1) average
* Delete: O(1) average
* Worst case (all collisions): O(n)
* Space: O(n)

---

# HashSet vs HashMap vs TreeSet

| Feature     | HashSet        | HashMap                      | TreeSet                     |
| ----------- | -------------- | ---------------------------- | --------------------------- |
| Stores      | Unique values  | Key-value pairs              | Unique values               |
| Nulls       | 1 null element | 1 null key, many null values | No nulls allowed            |
| Ordering    | Unordered      | Unordered                    | Sorted (natural/comparator) |
| Performance | O(1) average   | O(1) average                 | O(log n)                    |

---

# Examples and code snippets

### Remove duplicates from a list

```java
List<Integer> nums = Arrays.asList(1,2,2,3,4,4);
Set<Integer> unique = new HashSet<>(nums);
System.out.println(unique);
```

### Find intersection of two sets

```java
Set<Integer> a = new HashSet<>(Arrays.asList(1,2,3));
Set<Integer> b = new HashSet<>(Arrays.asList(2,3,4));
a.retainAll(b);
System.out.println(a); // [2,3]
```

### Check if all elements are unique

```java
public boolean allUnique(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for (int n : nums) if (!set.add(n)) return false;
    return true;
}
```

---

# Advanced topics

## Load factor and resizing

* Default capacity = 16, load factor = 0.75.
* Automatically resizes when load exceeded.

## Custom objects in HashSet

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

Set<Person> people = new HashSet<>();
people.add(new Person("Alice", 1));
```

## Null elements

* Allows at most one `null` element.

## Thread safety

* Not thread-safe.
* Wrap with:

```java
Set<Integer> syncSet = Collections.synchronizedSet(new HashSet<>());
```

* Or use `ConcurrentHashMap.newKeySet()`.

---

# Practice problems

1. Remove duplicates from a list using HashSet.
2. Find intersection of two arrays using HashSet.
3. Check if all characters in a string are unique.
4. Find first repeated element in an array.
5. Implement set operations: union, intersection, difference.

---

# Cheat sheet

* Insert/contains/remove: O(1) average.
* Allows one null element.
* Backed by HashMap.
* Not thread-safe.
* Use TreeSet if ordering required.