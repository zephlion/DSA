# Linked List - An In-Depth Guide (Java Version)

## 1. Introduction

A Linked List is a fundamental data structure that overcomes some of the limitations of arrays. Unlike arrays, linked lists are dynamic and allow efficient insertions and deletions without shifting elements. They are widely used to implement other data structures like stacks, queues, and graphs.

## 2. What is a Linked List?

A linked list is a linear collection of nodes, where each node contains two parts:

1. **Data** – the actual value stored.
2. **Pointer (or reference)** – a link to the next node in the sequence.

Unlike arrays, elements in a linked list are not stored in contiguous memory locations.

Example node structure in Java:

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

## 3. Properties of Linked Lists

* **Dynamic size:** Can grow or shrink at runtime.
* **Non-contiguous memory allocation:** Nodes are scattered in memory, connected via pointers.
* **Sequential access:** Accessing an element requires traversing from the head node.
* **Efficient insertions/deletions:** Unlike arrays, these operations don’t require shifting elements.

## 4. Advantages of Linked Lists

* Dynamic size allocation.
* Efficient insertions and deletions.
* Can easily represent abstract data types like stacks and queues.

## 5. Disadvantages of Linked Lists

* More memory usage due to storage of pointers.
* Sequential access only (no random access like arrays).
* Cache-unfriendly due to scattered memory allocation.
* Traversal can be slower compared to arrays.

## 6. Types of Linked Lists

* **Singly Linked List:** Each node points to the next node.
* **Doubly Linked List:** Each node points to both next and previous nodes.
* **Circular Linked List:** Last node points back to the head.

## 7. Common Operations on Linked Lists

### 7.1 Traversal

Traversal means visiting each node starting from the head.

```java
class LinkedList {
    Node head;

    public void traverse() {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }
}
```

**Explanation:** Start from the head node, follow the `next` references until reaching the end.

---

### 7.2 Insertion

#### Insert at the Beginning:

```java
public void insertAtBeginning(int data) {
    Node newNode = new Node(data);
    newNode.next = head;
    head = newNode;
}
```

*Time Complexity: O(1)*

#### Insert at the End:

```java
public void insertAtEnd(int data) {
    Node newNode = new Node(data);
    if (head == null) {
        head = newNode;
        return;
    }
    Node current = head;
    while (current.next != null) {
        current = current.next;
    }
    current.next = newNode;
}
```

*Time Complexity: O(n)*

---

### 7.3 Deletion

#### Delete by Value:

```java
public void delete(int key) {
    Node current = head, prev = null;

    // If head node is the key
    if (current != null && current.data == key) {
        head = current.next;
        return;
    }

    while (current != null && current.data != key) {
        prev = current;
        current = current.next;
    }

    if (current != null) {
        prev.next = current.next;
    }
}
```

*Time Complexity: O(n)*

---

### 7.4 Searching

```java
public boolean search(int key) {
    Node current = head;
    while (current != null) {
        if (current.data == key) {
            return true;
        }
        current = current.next;
    }
    return false;
}
```

*Time Complexity: O(n)*

## 8. Time and Space Complexity of Linked List Operations

| Operation       | Time Complexity | Space Complexity |
| --------------- | --------------- | ---------------- |
| Traversal       | O(n)            | O(1)             |
| Insertion (Beg) | O(1)            | O(1)             |
| Insertion (End) | O(n)            | O(1)             |
| Deletion        | O(n)            | O(1)             |
| Search          | O(n)            | O(1)             |

## 9. Real-World Applications of Linked Lists

* Implementation of dynamic memory management.
* Representation of stacks, queues, and graphs.
* Undo functionality in text editors.
* Playlist management in media players.

## 10. Comparison with Arrays

* **Linked List vs Array:**

  * Arrays allow random access; Linked Lists require sequential access.
  * Arrays have fixed size; Linked Lists are dynamic.
  * Arrays are cache-friendly; Linked Lists use extra memory due to pointers.

## 11. Conclusion

Linked Lists are a flexible and powerful data structure, especially useful for dynamic datasets where frequent insertions and deletions are required. Although they lack random access and use more memory, they form the backbone of many advanced data structures and algorithms.
