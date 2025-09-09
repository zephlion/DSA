# Queue - An In-Depth Guide (Java Version)

## 1. Introduction

A **Queue** is a fundamental linear data structure that models a real-world queue (line). It follows the **FIFO (First In, First Out)** principle: the first element added is the first removed. Queues are essential in systems that require ordered processing, buffering, and breadth-first traversal.

## 2. What is a Queue?

A queue is a collection where elements are added at one end (the **rear** or **tail**) and removed from the other end (the **front** or **head**). Elements are processed in the same order they arrive.

Example (in Java, using `LinkedList`):

```java
import java.util.*;

Queue<Integer> q = new LinkedList<>();
q.add(10);     // enqueue
q.add(20);
System.out.println(q.poll());  // dequeue -> 10
```

## 3. Properties of Queues

* **FIFO order:** First-in, first-out.
* **Two ends:** Enqueue at rear, dequeue at front.
* **Dynamic size:** Can grow or shrink (depending on implementation).
* **Use cases:** Scheduling, buffering, BFS, rate-limiting.

## 4. Advantages of Queues

* Predictable ordering of processing.
* Natural fit for producer-consumer problems.
* Efficient insertion and deletion at ends (when implemented with linked lists).

## 5. Disadvantages of Queues

* No random access by index; only front or rear operations are efficient.
* Simple array-based queues require shifting elements or circular buffering.
* Not suitable when out-of-order processing is required.

## 6. Types of Queues

* **Simple Queue (Linear Queue):** Basic FIFO queue; may require shifting when implemented with arrays.
* **Circular Queue (Ring Buffer):** Wraps around array to reuse freed space.
* **Priority Queue:** Elements are dequeued based on priority rather than arrival order (commonly implemented with heaps).
* **Double-Ended Queue (Deque):** Allows insertion and deletion at both ends.
* **Blocking Queue:** Thread-safe queue that blocks on enqueue/dequeue when full/empty (used in concurrent programming).

## 7. Common Operations on Queues (with Java examples)

### 7.1 Enqueue (Insert at rear)

```java
Queue<Integer> q = new LinkedList<>();
q.add(1);    // O(1)
q.add(2);
```

*Explanation:* `add()` inserts at the rear.

---

### 7.2 Dequeue (Remove from front)

```java
int x = q.poll();  // O(1)
```

*Explanation:* `poll()` removes and returns the head, or `null` if empty.

---

### 7.3 Peek (View front element)

```java
Integer front = q.peek(); // O(1)
```

*Explanation:* `peek()` returns the head without removing it.

---

### 7.4 isEmpty (Check if queue is empty)

```java
boolean isEmpty = q.isEmpty();
```

*Explanation:* O(1) operation.

---

### 7.5 Size (Number of elements)

```java
int size = q.size();
```

*Explanation:* `size()` is O(1).

---

### 7.6 Traversal

```java
for (int item : q) {
    System.out.println(item);
}
```

*Explanation:* Iterating is O(n); order is front → rear.

---

### 7.7 Circular Queue (array-based) example

```java
class CircularQueue {
    private int[] data;
    private int head;
    private int tail;
    private int capacity;

    public CircularQueue(int k) {
        capacity = k + 1; // one slot kept empty
        data = new int[capacity];
        head = 0;
        tail = 0;
    }

    public boolean isEmpty() {
        return head == tail;
    }

    public boolean isFull() {
        return (tail + 1) % capacity == head;
    }

    public void enqueue(int x) {
        if (isFull()) throw new RuntimeException("enqueue on full queue");
        data[tail] = x;
        tail = (tail + 1) % capacity;
    }

    public int dequeue() {
        if (isEmpty()) throw new RuntimeException("dequeue from empty queue");
        int x = data[head];
        head = (head + 1) % capacity;
        return x;
    }

    public Integer front() {
        if (isEmpty()) return null;
        return data[head];
    }

    public int size() {
        return (tail - head + capacity) % capacity;
    }
}
```

*Explanation:* Circular queue avoids shifting by wrapping indices.

---

### 7.8 Priority Queue example

```java
import java.util.*;

PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(5);
pq.add(1);
pq.add(3);

System.out.println(pq.poll()); // 1 (smallest element)
```

*Explanation:* `PriorityQueue` is a min-heap; operations are O(log n). For max-heap, pass a custom comparator.

## 8. Time and Space Complexity of Queue Operations

| Operation          | Time Complexity | Space Complexity |
| ------------------ | --------------- | ---------------- |
| Enqueue            | O(1)            | O(1)             |
| Dequeue            | O(1)            | O(1)             |
| Peek               | O(1)            | O(1)             |
| Traversal          | O(n)            | O(1)             |
| Circular Queue ops | O(1)            | O(n)             |
| Priority Queue ops | O(log n)        | O(n)             |

## 9. Real-World Applications of Queues

* Task scheduling and job processing (message queues, print queues).
* Breadth-First Search (BFS) in graphs.
* Producer-consumer problems and buffering (I/O, network packets).
* Rate limiting and token buckets.
* Event handling and task dispatching in servers.

## 10. Comparison with Other Data Structures

* **Queues vs Stacks:** Queue is FIFO; Stack is LIFO.
* **Queues vs Deques:** Deque supports insertion/removal at both ends; queue restricts to one end for enqueue and the other for dequeue.
* **Queues vs Priority Queues:** Priority queues order by priority, not arrival order; operations are costlier (O(log n)).

## 11. Conclusion

Queues are simple yet powerful. Choosing the right implementation (array, circular buffer, linked list, deque, or heap) depends on requirements like concurrency, bounded capacity, ordering by priority, and performance constraints. Understanding queues is essential for designing efficient and correct systems.