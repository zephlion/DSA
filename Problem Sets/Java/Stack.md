# Java DSA Guide — Stack

*A comprehensive, in-depth guide to `Stack` in Java, a LIFO (Last In, First Out) data structure widely used in algorithms and problem-solving.*

---

## Table of contents

1. [Introduction](#introduction)
2. [Stack basics](#stack-basics)

   * [What is Stack?](#what-is-stack)
   * [Key characteristics](#key-characteristics)
   * [Internal implementation](#internal-implementation)
3. [Stack operations](#stack-operations)

   * [Creation](#creation)
   * [Push](#push)
   * [Pop](#pop)
   * [Peek](#peek)
   * [Search](#search)
   * [Iteration](#iteration)
4. [Time & space complexity](#time--space-complexity)
5. [Stack vs Deque vs ArrayDeque](#stack-vs-deque-vs-arraydeque)
6. [Examples and code snippets](#examples-and-code-snippets)
7. [Advanced topics](#advanced-topics)

   * [Implementing stack using ArrayList](#implementing-stack-using-arraylist)
   * [Implementing stack using LinkedList](#implementing-stack-using-linkedlist)
   * [Thread safety](#thread-safety)
8. [Practice problems](#practice-problems)
9. [Cheat sheet](#cheat-sheet)

---

# Introduction

`Stack` is a collection in Java that represents a **Last-In, First-Out (LIFO)** data structure. It is widely used for problems like expression evaluation, backtracking, DFS traversal, and function call management.

---

# Stack basics

## What is Stack?

* A linear data structure following the LIFO principle.
* Introduced in Java as a class (`java.util.Stack`) that extends `Vector`.

## Key characteristics

* Supports push, pop, peek, and search operations.
* Allows duplicates.
* Thread-safe (inherited from `Vector`), but may have performance overhead.

## Internal implementation

* Backed by a `Vector`.
* Provides stack-specific methods in addition to `Vector` methods.

---

# Stack operations

## Creation

```java
Stack<Integer> stack = new Stack<>();
```

## Push

```java
stack.push(10);
stack.push(20);
```

## Pop

```java
int val = stack.pop(); // removes and returns top element
```

## Peek

```java
int top = stack.peek(); // returns top element without removing
```

## Search

```java
int pos = stack.search(10); // 1-based position from top
```

## Iteration

```java
for (int val : stack) System.out.println(val);

Iterator<Integer> it = stack.iterator();
while (it.hasNext()) System.out.println(it.next());
```

---

# Time & space complexity

* Push: O(1)
* Pop: O(1)
* Peek: O(1)
* Search: O(n)
* Space: O(n)

---

# Stack vs Deque vs ArrayDeque

| Feature     | Stack (`java.util.Stack`) | Deque (`java.util.Deque`) | ArrayDeque (`java.util.ArrayDeque`) |
| ----------- | ------------------------- | ------------------------- | ----------------------------------- |
| Thread-safe | ✅ Yes (via Vector)        | ❌ No (not by default)     | ❌ No (not by default)               |
| Performance | Slower (sync overhead)    | Faster                    | Faster                              |
| Preferred?  | Legacy, less recommended  | Modern alternative        | Best choice for stack behavior      |

---

# Examples and code snippets

### Reverse a string using stack

```java
String str = "hello";
Stack<Character> stack = new Stack<>();
for (char c : str.toCharArray()) stack.push(c);

StringBuilder rev = new StringBuilder();
while (!stack.isEmpty()) rev.append(stack.pop());

System.out.println(rev.toString());
```

### Balanced parentheses checker

```java
public boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();
    for (char c : s.toCharArray()) {
        if (c == '(' || c == '{' || c == '[') stack.push(c);
        else {
            if (stack.isEmpty()) return false;
            char top = stack.pop();
            if ((c == ')' && top != '(') ||
                (c == '}' && top != '{') ||
                (c == ']' && top != '[')) return false;
        }
    }
    return stack.isEmpty();
}
```

### Implement DFS using stack

```java
public void dfs(int start, List<List<Integer>> graph) {
    boolean[] visited = new boolean[graph.size()];
    Stack<Integer> stack = new Stack<>();
    stack.push(start);

    while (!stack.isEmpty()) {
        int node = stack.pop();
        if (!visited[node]) {
            visited[node] = true;
            System.out.print(node + " ");
            for (int nei : graph.get(node)) stack.push(nei);
        }
    }
}
```

---

# Advanced topics

## Implementing stack using ArrayList

```java
class ArrayListStack<E> {
    private ArrayList<E> list = new ArrayList<>();

    public void push(E item) { list.add(item); }
    public E pop() { return list.remove(list.size() - 1); }
    public E peek() { return list.get(list.size() - 1); }
    public boolean isEmpty() { return list.isEmpty(); }
}
```

## Implementing stack using LinkedList

```java
Deque<Integer> stack = new LinkedList<>();
stack.push(10);
stack.push(20);
System.out.println(stack.pop());
```

## Thread safety

* `Stack` is thread-safe, but with performance cost.
* For modern alternatives, use `ConcurrentLinkedDeque`.

---

# Practice problems

1. Reverse a string using stack.
2. Check for balanced parentheses.
3. Evaluate postfix expression using stack.
4. Implement min stack (getMin in O(1)).
5. Use stack to implement queue.

---

# Cheat sheet

* Stack = LIFO.
* Push/Pop/Peek = O(1).
* Use `ArrayDeque` instead of `Stack` for better performance.
* Thread safety: Stack is synchronized.