# Java DSA Guide — ArrayDeque

*A comprehensive, in-depth guide to `ArrayDeque` in Java, a resizable array-based implementation of the double-ended queue (Deque) interface.*

---

## Table of contents

1. [Introduction](#introduction)
2. [ArrayDeque basics](#arraydeque-basics)

   * [What is ArrayDeque?](#what-is-arraydeque)
   * [Key characteristics](#key-characteristics)
   * [Internal implementation](#internal-implementation)
3. [ArrayDeque operations](#arraydeque-operations)

   * [Creation](#creation)
   * [Adding elements](#adding-elements)
   * [Removing elements](#removing-elements)
   * [Accessing elements](#accessing-elements)
   * [Iteration](#iteration)
4. [Time & space complexity](#time--space-complexity)
5. [ArrayDeque vs Stack vs LinkedList](#arraydeque-vs-stack-vs-linkedlist)
6. [Examples and code snippets](#examples-and-code-snippets)
7. [Advanced topics](#advanced-topics)

   * [Capacity and resizing](#capacity-and-resizing)
   * [Null handling](#null-handling)
   * [Thread safety](#thread-safety)
8. [Practice problems](#practice-problems)
9. [Cheat sheet](#cheat-sheet)

---

# Introduction

`ArrayDeque` is a resizable-array implementation of the `Deque` interface. It is more efficient than `Stack` and `LinkedList` when used as a stack or queue, making it one of the most versatile data structures in Java.

---

# ArrayDeque basics

## What is ArrayDeque?

* Part of `java.util` package.
* Implements `Deque<E>`.
* Supports insertion and removal at both ends.
* Provides better performance than `Stack` (legacy) and `LinkedList` (due to contiguous memory).

## Key characteristics

* No capacity restrictions — grows automatically.
* **Does not allow `null` elements**.
* Not thread-safe.
* Provides amortized O(1) time for insertions and removals at both ends.

## Internal implementation

* Backed by a resizable circular array.
* Automatically doubles in size when capacity exceeded.

---

# ArrayDeque operations

## Creation

```java
Deque<Integer> deque = new ArrayDeque<>();
Deque<String> dequeWithCapacity = new ArrayDeque<>(32);
```

## Adding elements

```java
deque.addFirst(10);
deque.addLast(20);
deque.offerFirst(5);
deque.offerLast(25);
```

## Removing elements

```java
int first = deque.removeFirst();
int last = deque.removeLast();

// Safe methods (return null if empty)
deque.pollFirst();
deque.pollLast();
```

## Accessing elements

```java
int front = deque.getFirst();
int back = deque.getLast();

// Safe methods (return null if empty)
deque.peekFirst();
deque.peekLast();
```

## Iteration

```java
for (int val : deque) System.out.println(val);

Iterator<Integer> it = deque.descendingIterator();
while (it.hasNext()) System.out.println(it.next());
```

---

# Time & space complexity

* Insert/remove first/last: O(1) amortized
* Access first/last: O(1)
* Iteration: O(n)
* Space: O(n)

---

# ArrayDeque vs Stack vs LinkedList

| Feature       | ArrayDeque                  | Stack (`java.util.Stack`) | LinkedList                                  |
| ------------- | --------------------------- | ------------------------- | ------------------------------------------- |
| Thread-safe   | ❌ No                        | ✅ Yes (synchronized)      | ❌ No                                        |
| Null elements | ❌ Not allowed               | ✅ Allowed                 | ✅ Allowed                                   |
| Performance   | Fastest (contiguous memory) | Slower (sync overhead)    | Slower (node overhead)                      |
| Preferred use | Queue & stack impl.         | Legacy, avoid if possible | When frequent insertions/removals in middle |

---

# Examples and code snippets

### Implement stack using ArrayDeque

```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(10);
stack.push(20);
System.out.println(stack.pop()); // 20
```

### Implement queue using ArrayDeque

```java
Deque<Integer> queue = new ArrayDeque<>();
queue.offer(1);
queue.offer(2);
System.out.println(queue.poll()); // 1
```

### Palindrome checker

```java
public boolean isPalindrome(String s) {
    Deque<Character> dq = new ArrayDeque<>();
    for (char c : s.toCharArray()) dq.addLast(c);
    while (dq.size() > 1) if (dq.pollFirst() != dq.pollLast()) return false;
    return true;
}
```

---

# Advanced topics

## Capacity and resizing

* Grows automatically when capacity exceeded.
* Resizing is rare, so amortized O(1).

## Null handling

* Does not allow `null` elements.
* Prevents ambiguity in `poll`/`peek` methods that return `null` when empty.

## Thread safety

* Not thread-safe.
* Use `Collections.synchronizedDeque(new ArrayDeque<>())` for basic synchronization.
* For high concurrency, prefer `ConcurrentLinkedDeque`.

---

# Practice problems

1. Implement stack using ArrayDeque.
2. Implement queue using ArrayDeque.
3. Check if a string is a palindrome using ArrayDeque.
4. Design a sliding window maximum using ArrayDeque.
5. Simulate browser forward/back navigation with ArrayDeque.

---

# Cheat sheet

* ArrayDeque = resizable circular array.
* No nulls allowed.
* Faster than `Stack` and `LinkedList` for queue/stack.
* Insert/remove both ends in O(1) amortized.