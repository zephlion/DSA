# Java DSA Guide — ArrayList

*A comprehensive, in-depth guide to ArrayList in Java, a dynamic array implementation widely used in applications and interviews.*

---

## Table of contents

1. [Introduction](#introduction)
2. [ArrayList basics](#arraylist-basics)

   * [What is ArrayList?](#what-is-arraylist)
   * [Key characteristics](#key-characteristics)
   * [Underlying implementation](#underlying-implementation)
3. [ArrayList operations](#arraylist-operations)

   * [Creation](#creation)
   * [Adding elements](#adding-elements)
   * [Accessing and modifying](#accessing-and-modifying)
   * [Removing elements](#removing-elements)
   * [Iteration](#iteration)
   * [Searching](#searching)
   * [Sorting](#sorting)
4. [Time & space complexity](#time--space-complexity)
5. [Array vs ArrayList](#array-vs-arraylist)
6. [Common pitfalls](#common-pitfalls)
7. [Examples and code snippets](#examples-and-code-snippets)
8. [Advanced topics](#advanced-topics)

   * [Capacity and resizing](#capacity-and-resizing)
   * [Synchronization](#synchronization)
   * [Custom objects in ArrayList](#custom-objects-in-arraylist)
9. [Practice problems](#practice-problems)
10. [Cheat sheet](#cheat-sheet)

---

# Introduction

`ArrayList` is a **resizable array** implementation in Java. It is part of the `java.util` package and provides dynamic sizing, convenient methods, and is commonly used as a flexible alternative to arrays.

---

# ArrayList basics

## What is ArrayList?

* A class in Java that implements the `List` interface.
* Provides dynamic resizing (unlike arrays with fixed size).
* Stores elements in contiguous memory, like arrays.

## Key characteristics

* Allows random access in O(1).
* Duplicates allowed.
* Maintains insertion order.
* Not thread-safe (use `Collections.synchronizedList` or `CopyOnWriteArrayList` for concurrency).

## Underlying implementation

* Backed by an array.
* Resizes automatically when capacity exceeded (usually 1.5x growth).

---

# ArrayList operations

## Creation

```java
ArrayList<Integer> list = new ArrayList<>();
ArrayList<String> names = new ArrayList<>(Arrays.asList("Alice", "Bob"));
```

## Adding elements

```java
list.add(10);
list.add(20);
list.add(1, 15); // insert at index
```

## Accessing and modifying

```java
int x = list.get(0);
list.set(1, 25);
```

## Removing elements

```java
list.remove(0); // by index
list.remove(Integer.valueOf(25)); // by object
list.clear(); // remove all
```

## Iteration

```java
for (int num : list) System.out.println(num);

Iterator<Integer> it = list.iterator();
while (it.hasNext()) System.out.println(it.next());
```

## Searching

```java
boolean found = list.contains(10);
int idx = list.indexOf(15);
```

## Sorting

```java
Collections.sort(list);
list.sort(Comparator.reverseOrder());
```

---

# Time & space complexity

* Access: O(1)
* Search: O(n)
* Insert/remove at end: Amortized O(1)
* Insert/remove at index: O(n)
* Space: O(n)

---

# Array vs ArrayList

| Feature     | Array                | ArrayList                            |
| ----------- | -------------------- | ------------------------------------ |
| Size        | Fixed                | Dynamic                              |
| Performance | Faster (no resizing) | Slight overhead                      |
| API         | Basic                | Rich (add, remove, sort, etc.)       |
| Type        | Can hold primitives  | Only objects (primitives auto-boxed) |

---

# Common pitfalls

* `IndexOutOfBoundsException` if accessing invalid index.
* Performance issues with frequent inserts/removes in the middle.
* Autoboxing/unboxing overhead for primitives.
* Not thread-safe by default.

---

# Examples and code snippets

### Dynamic resizing demo

```java
ArrayList<Integer> list = new ArrayList<>();
for (int i = 0; i < 20; i++) list.add(i);
System.out.println(list);
```

### Removing duplicates using HashSet

```java
ArrayList<Integer> list = new ArrayList<>(Arrays.asList(1,2,2,3,4,4));
Set<Integer> set = new HashSet<>(list);
list = new ArrayList<>(set);
System.out.println(list);
```

### Convert ArrayList to array

```java
Integer[] arr = list.toArray(new Integer[0]);
```

---

# Advanced topics

## Capacity and resizing

* Initial capacity can be set:

```java
ArrayList<Integer> list = new ArrayList<>(100);
```

* Resizing cost: O(n), but amortized insertion is O(1).

## Synchronization

```java
List<Integer> syncList = Collections.synchronizedList(new ArrayList<>());
```

## Custom objects in ArrayList

```java
class Person {
    String name;
    int age;
    Person(String n, int a) { name = n; age = a; }
}

ArrayList<Person> people = new ArrayList<>();
people.add(new Person("Alice", 30));
```

---

# Practice problems

1. Implement dynamic array manually (like ArrayList).
2. Remove duplicates from ArrayList.
3. Find intersection of two ArrayLists.
4. Implement stack using ArrayList.
5. Reverse an ArrayList in place.

---

# Cheat sheet

* Random access: O(1)
* Append: Amortized O(1)
* Insert/delete middle: O(n)
* Use `Collections.sort` for sorting.
* Prefer `ArrayList` over arrays when dynamic resizing or rich API is needed.