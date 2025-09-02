# Queue - An In-Depth Guide

## 1. Introduction

A **Queue** is a fundamental linear data structure that models a real-world queue (line). It follows the **FIFO (First In, First Out)** principle: the first element added is the first removed. Queues are essential in systems that require ordered processing, buffering, and breadth-first traversal.

## 2. What is a Queue?

A queue is a collection where elements are added at one end (the **rear** or **tail**) and removed from the other end (the **front** or **head**). Elements are processed in the same order they arrive.

Example (in Python, using `collections.deque`):

```python
from collections import deque
q = deque()
q.append(10)    # enqueue
q.append(20)
print(q.popleft())  # dequeue -> 10
```

## 3. Properties of Queues

* **FIFO order:** First-in, first-out.
* **Two ends:** Enqueue at rear, dequeue at front.
* **Dynamic size:** Can grow or shrink (depending on implementation).
* **Use cases:** Scheduling, buffering, BFS, rate-limiting.

## 4. Advantages of Queues

* Predictable ordering of processing.
* Natural fit for producer-consumer problems.
* Efficient insertion and deletion at ends (when implemented with linked lists or `deque`).

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

## 7. Common Operations on Queues (with Python examples)

### 7.1 Enqueue (Insert at rear)

```python
from collections import deque
q = deque()
q.append(1)    # O(1)
q.append(2)
```

*Explanation:* `append()` on `deque` adds to the right (rear) in O(1).

---

### 7.2 Dequeue (Remove from front)

```python
x = q.popleft()  # O(1)
```

*Explanation:* `popleft()` removes and returns the leftmost (front) element in O(1).

---

### 7.3 Peek (View front element)

```python
front = q[0] if q else None
```

*Explanation:* Accessing the leftmost element of `deque` by index is O(1) but check for emptiness first.

---

### 7.4 isEmpty (Check if queue is empty)

```python
is_empty = len(q) == 0
```

*Explanation:* Checking length is O(1).

---

### 7.5 Size (Number of elements)

```python
size = len(q)
```

*Explanation:* `len()` is O(1).

---

### 7.6 Traversal

```python
for item in q:
    print(item)
```

*Explanation:* Iterating over a queue is O(n); order is front → rear.

---

### 7.7 Circular Queue (array-based) example

```python
class CircularQueue:
    def __init__(self, k):
        self.capacity = k + 1  # one slot is kept empty
        self.data = [None] * self.capacity
        self.head = 0
        self.tail = 0

    def is_empty(self):
        return self.head == self.tail

    def is_full(self):
        return (self.tail + 1) % self.capacity == self.head

    def enqueue(self, x):
        if self.is_full():
            raise IndexError('enqueue on full queue')
        self.data[self.tail] = x
        self.tail = (self.tail + 1) % self.capacity

    def dequeue(self):
        if self.is_empty():
            raise IndexError('dequeue from empty queue')
        x = self.data[self.head]
        self.head = (self.head + 1) % self.capacity
        return x

    def front(self):
        if self.is_empty():
            return None
        return self.data[self.head]

    def __len__(self):
        return (self.tail - self.head + self.capacity) % self.capacity
```

*Explanation:* Circular queue avoids shifting by wrapping indices; capacity holds `k` elements using an internal buffer of size `k+1`.

---

### 7.8 Priority Queue example (using `heapq`)

```python
import heapq
pq = []
heapq.heappush(pq, (priority, item))
priority, item = heapq.heappop(pq)
```

*Explanation:* `heapq` implements a min-heap; operations are O(log n). For max-heap behavior, invert priority with negative values.

## 8. Time and Space Complexity of Queue Operations

| Operation          | Time Complexity | Space Complexity |
| ------------------ | --------------- | ---------------- |
| Enqueue            | O(1) (deque)    | O(1)             |
| Dequeue            | O(1) (deque)    | O(1)             |
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
