# Stack - An In-Depth Guide

## 1. Introduction

Stacks are a fundamental data structure in computer science, widely used for solving problems related to expression evaluation, backtracking, and memory management. A stack follows the **LIFO (Last In, First Out)** principle, meaning the last element inserted is the first one to be removed.

## 2. What is a Stack?

A stack is a linear data structure where elements are inserted and removed only from one end, called the **top**. This structure mimics the idea of stacking plates — you can only add or remove the top plate.

Example in Java:

```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();
        stack.push(10);  // push
        stack.push(20);
        System.out.println(stack.pop()); // pop → 20
    }
}
```

## 3. Properties of Stacks

* **LIFO order:** Last element pushed is the first one popped.
* **Single access point:** Only the top of the stack can be accessed.
* **Dynamic size:** Can grow or shrink as needed.

## 4. Advantages of Stacks

* Simple and efficient for problems requiring reversal or backtracking.
* Useful in function call management (system call stack).
* Provides controlled access to data.

## 5. Disadvantages of Stacks

* Limited access (only top element is available).
* Not efficient for searching arbitrary elements.
* Can cause stack overflow if memory exceeds limits.

## 6. Types of Stacks

* **Static Stack:** Implemented using arrays with fixed size.
* **Dynamic Stack:** Implemented using linked lists for flexibility.

## 7. Common Operations on Stacks

### Push (Insert element)

Adds an element to the top of the stack.

```java
Stack<Integer> stack = new Stack<>();
stack.push(5);  // push 5
stack.push(10); // push 10
System.out.println(stack); // [5, 10]
```

### Pop (Remove element)

Removes the top element.

```java
Stack<Integer> stack = new Stack<>();
stack.push(5);
stack.push(10);
stack.push(15);
int removed = stack.pop();
System.out.println(removed); // 15
System.out.println(stack);   // [5, 10]
```

### Peek (View top element)

Accesses the top element without removing it.

```java
Stack<Integer> stack = new Stack<>();
stack.push(5);
stack.push(10);
stack.push(15);
int top = stack.peek();
System.out.println(top); // 15
```

### isEmpty (Check if stack is empty)

```java
Stack<Integer> stack = new Stack<>();
System.out.println(stack.isEmpty()); // true
```

### Size (Get number of elements)

```java
Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.push(3);
stack.push(4);
System.out.println(stack.size()); // 4
```

## 8. Time and Space Complexity of Stack Operations

| Operation | Time Complexity | Space Complexity |
| --------- | --------------- | ---------------- |
| Push      | O(1)            | O(1)             |
| Pop       | O(1)            | O(1)             |
| Peek      | O(1)            | O(1)             |
| isEmpty   | O(1)            | O(1)             |
| Size      | O(1)            | O(1)             |

## 9. Real-World Applications of Stacks

* Function call management (call stack in programming languages).
* Undo/Redo functionality in editors.
* Expression evaluation and syntax parsing.
* Depth-First Search (DFS) in graphs.
* Balanced parenthesis checking.

## 10. Comparison with Other Data Structures

* **Stack vs Queue:** Stack uses LIFO, while queue uses FIFO.
* **Stack vs Array:** Stacks restrict access to the last inserted element, while arrays allow random access.
* **Stack vs Linked List:** A stack can be implemented using a linked list, but linked lists allow more flexibility in insertion and deletion at different positions.

## 11. Conclusion

Stacks are one of the most essential data structures. Their simplicity and efficiency make them ideal for managing hierarchical data, recursion, and backtracking problems. Understanding stacks lays the groundwork for mastering more complex structures and algorithms.
