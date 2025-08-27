# Data Structures - An In-Depth Guide

## 1. Introduction

Data structures are fundamental concepts in computer science that define how data is organized, stored, and accessed. They directly impact the efficiency of algorithms and play a vital role in software development, system design, and problem-solving.


## 2. Primitive Data Structures

Primitive data structures are the basic building blocks provided by most programming languages.

* **Integer**: Represents whole numbers. Used for counting, indexing, and arithmetic operations.
* **Float / Double**: Represents real numbers with decimals. Useful for scientific calculations, measurements, and precise computations.
* **Character**: Stores a single symbol, letter, or digit. Essential for text processing.
* **String**: A sequence of characters. Used in handling text, file processing, and user input.
* **Boolean**: Represents logical values: `true` or `false`. Used in conditions, branching, and logic control.


## 3. Non-Primitive Data Structures

Non-primitive structures are built using primitive types and can store multiple values.

### 3.1 Linear Data Structures

Data is arranged sequentially.

* **Array**

  * Stores elements in contiguous memory.
  * Provides constant-time access using indices.
  * Limitation: fixed size.
  * Use cases: Lookup tables, storing fixed-size datasets.

* **Linked List**

  * Collection of nodes where each node contains data and a pointer to the next node.
  * Types:

    * Singly Linked List: Each node points to the next.
    * Doubly Linked List: Each node points to both previous and next nodes.
    * Circular Linked List: Last node points back to the first.
  * Flexible size but slower access compared to arrays.

* **Stack**

  * Follows **Last In, First Out (LIFO)** principle.
  * Operations: `push`, `pop`, `peek`.
  * Use cases: Undo functionality, function call management.

* **Queue**

  * Follows **First In, First Out (FIFO)**.
  * Variants:

    * Simple Queue
    * Circular Queue
    * Priority Queue (elements dequeued by priority)
    * Deque (double-ended queue)
  * Use cases: Task scheduling, buffering.

### 3.2 Non-Linear Data Structures

Data is organized hierarchically or as networks.

* **Tree**

  * A hierarchical structure of nodes.
  * Variants:

    * Binary Tree: Each node has up to two children.
    * Binary Search Tree (BST): Left child < Parent < Right child.
    * AVL Tree: Self-balancing BST.
    * Red-Black Tree: Balanced search tree used in databases.
    * B-Tree & B+ Tree: Efficient for disk storage and indexing.
    * Heap: Binary tree used for priority-based tasks.

      * Min Heap: Parent < Children.
      * Max Heap: Parent > Children.
    * Trie: Specialized tree for storing strings.
    * Segment Tree: Used for range queries and modifications.
  * Use cases: File systems, databases, compilers.

* **Graph**

  * A collection of nodes (vertices) connected by edges.
  * Types:

    * Directed vs Undirected
    * Weighted vs Unweighted
    * Cyclic vs Acyclic
  * Use cases: Social networks, shortest path problems, network routing.

### 3.3 Hash-Based Data Structures

* **Hash Table**: Stores key-value pairs with fast lookups.
* **Hash Map**: Implementation of hash table in many languages.
* **Hash Set**: Stores unique elements using hashing.
* Use cases: Databases, caching, uniqueness checks.


## 4. Use Cases and Applications

* Arrays: Image processing, lookup tables.
* Linked Lists: Dynamic memory allocation, music playlists.
* Stacks: Undo/redo operations, function calls.
* Queues: Print job scheduling, order processing.
* Trees: File systems, database indexing.
* Graphs: GPS navigation, social networks.
* Hash Tables: Caching, dictionaries, search engines.


## 5. Complexity Analysis

Data structures affect the time and space complexity of operations.

* **Time Complexity**: Measures execution time for operations (e.g., insertion, deletion, search).
* **Space Complexity**: Measures memory usage.

Example:

* Array search: O(n)
* Binary search (sorted array): O(log n)
* Hash table lookup: O(1) average case


## 6. Comparison of Data Structures

* Arrays vs Linked Lists: Arrays allow fast access, linked lists allow flexible size.
* Stacks vs Queues: Different order of insertion/removal.
* Trees vs Graphs: Trees are hierarchical, graphs are network-based.
* Hash Tables vs Arrays: Hash tables provide faster lookups for large datasets.


## 7. Real-World Analogies

* **Array**: Like lockers in a row, each with a number.
* **Linked List**: Like a treasure hunt where each clue points to the next.
* **Stack**: Like a stack of plates; last placed is first removed.
* **Queue**: Like a line at a ticket counter.
* **Tree**: Like a family tree.
* **Graph**: Like a map of cities connected by roads.
* **Hash Table**: Like a dictionary where each word is mapped to its meaning.


## 8. Conclusion

Data structures form the foundation of computer science. Mastering them is essential for writing efficient algorithms, solving complex problems, and excelling in technical interviews. Choosing the right data structure ensures programs are optimized for speed, memory, and scalability.
