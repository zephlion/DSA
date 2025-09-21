# Java DSA Guide — Deque

*A comprehensive, in-depth guide to `Deque` in Java, a double-ended queue supporting insertion and removal at both ends.*

---

## Table of contents

1. [Introduction](#introduction)
2. [Deque basics](#deque-basics)

   * [What is Deque?](#what-is-deque)
   * [Key characteristics](#key-characteristics)
   * [Implementations](#implementations)
3. [Deque operations](#deque-operations)

   * [Creation](#creation)
   * [Adding elements](#adding-elements)
   * [Removing elements](#removing-elements)
   * [Accessing elements](#accessing-elements)
   * [Iteration](#iteration)
4. [Time & space complexity](#time--space-complexity)
5. [Deque vs Queue vs Stack](#deque-vs-queue-vs-stack)
6. [Examples and code snippets](#examples-and-code-snippets)
7. [Advanced topics](#advanced-topics)

   * [ArrayDeque](#arraydeque)
   * [LinkedList as Deque](#linkedlist-as-deque)
   * [Thread-safe Deques](#thread-safe-deques)
8. [Practice problems](#practice-problems)
9. [Cheat sheet](#cheat-sheet)

---

# Introduction

`Deque` (Double-Ended Queue) is part of the Java Collections Framework. It extends the `Queue` interface and allows insertion and removal of elements from **both ends**.

---

# Deque basics

## What is Deque?

* A linear collection that supports element insertion and removal at both ends.
* Pronounced "deck".
* Extends `Queue` interface.

## Key characteristics

* Can function as both **Queue (FIFO)** and **Stack (LIFO)**.
* Supports null elements in some implementations (`LinkedList`), but `ArrayDeque` does not allow `null`.
* Provides more versatile operations than `Queue`.

## Implementations

* `ArrayDeque` — resizable array-based implementation, high performance.
* `LinkedList` — doubly-linked list implementation.
* `ConcurrentLinkedDeque` — thread-safe, lock-free implementation.

---

# Deque operations

## Creation

```java
Deque<Integer> deque1 = new ArrayDeque<>();
Deque<String> deque2 = new LinkedList<>();
```

## Adding elements

```java
deque1.addFirst(10);
deque1.addLast(20);
deque1.offerFirst(5);
deque1.offerLast(25);
```

## Removing elements

```java
int first = deque1.removeFirst();
int last = deque1.removeLast();

// Safe methods (return null if empty)
deque1.pollFirst();
deque1.pollLast();
```

## Accessing elements

```java
int front = deque1.getFirst();
int back = deque1.getLast();

// Safe methods (return null if empty)
deque1.peekFirst();
deque1.peekLast();
```

## Iteration

```java
for (int val : deque1) System.out.println(val);

Iterator<Integer> it = deque1.descendingIterator();
while (it.hasNext()) System.out.println(it.next());
```

---

# Time & space complexity

* Insert first/last: O(1)
* Remove first/last: O(1)
* Access first/last: O(1)
* Space: O(n)

---

# Deque vs Queue vs Stack

| Feature     | Queue                         | Stack        | Deque                     |
| ----------- | ----------------------------- | ------------ | ------------------------- |
| Order       | FIFO                          | LIFO         | FIFO + LIFO               |
| Ends used   | Rear (insert), Front (remove) | One end only | Both ends (insert/remove) |
| Flexibility | Limited                       | Limited      | Most versatile            |

---

# Examples and code snippets

### Implement queue using Deque

```java
Deque<Integer> queue = new ArrayDeque<>();
queue.offer(1);
queue.offer(2);
System.out.println(queue.poll()); // 1
```

### Implement stack using Deque

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(10);
stack.push(20);
System.out.println(stack.pop()); // 20
```

### Sliding window maximum

```java
public int[] maxSlidingWindow(int[] nums, int k) {
    Deque<Integer> dq = new ArrayDeque<>();
    int[] res = new int[nums.length - k + 1];
    int idx = 0;

    for (int i = 0; i < nums.length; i++) {
        while (!dq.isEmpty() && dq.peekFirst() <= i - k) dq.pollFirst();
        while (!dq.isEmpty() && nums[dq.peekLast()] < nums[i]) dq.pollLast();
        dq.offerLast(i);
        if (i >= k - 1) res[idx++] = nums[dq.peekFirst()];
    }
    return res;
}
```

---

# Advanced topics

## ArrayDeque

* No capacity restrictions (resizes automatically).
* Does not allow `null`.
* Faster than `Stack` and `LinkedList` for stack/queue operations.

## LinkedList as Deque

* Supports `null` elements.
* Slightly slower than `ArrayDeque` due to extra memory overhead.

## Thread-safe Deques

* `ConcurrentLinkedDeque` — lock-free, scalable.
* `LinkedBlockingDeque` — blocking, useful in producer-consumer problems.

---

# Practice problems

1. Implement stack using Deque.
2. Implement queue using Deque.
3. Solve sliding window maximum problem.
4. Check palindrome using Deque.
5. Design browser history using Deque.

---

# Cheat sheet

* Double-ended queue.
* Insert/remove from both ends in O(1).
* Best implementation: `ArrayDeque` (non-thread-safe).
* Use `ConcurrentLinkedDeque` for concurrent environments.