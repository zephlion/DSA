# Data Structures and Algorithms (DSA)

**Data Structures and Algorithms (DSA)** is a core concept in computer science that deals with how data is organized, stored, and processed efficiently.  


## 1. Data Structures
A **data structure** is a way of organizing and storing data so it can be used effectively.  
It defines **how data is arranged in memory** and what operations can be performed on it.  

### Examples
- **Array** – stores elements in contiguous memory (fast access, fixed size).  
- **Linked List** – stores elements with pointers (flexible size, slower access).  
- **Stack** – follows *Last In, First Out (LIFO)*.  
- **Queue** – follows *First In, First Out (FIFO)*.  
- **Tree** – hierarchical data (e.g., family tree, file system).  
- **Graph** – set of nodes and edges (e.g., social networks, maps).  
- **Hash Table** – key-value storage for quick lookup.  


## 2. Algorithms
An **algorithm** is a **step-by-step procedure** or set of rules to solve a problem or perform a task.  
It defines **how data is processed**.  

### Examples
- **Sorting Algorithms**: Bubble Sort, Merge Sort, Quick Sort (arrange data in order).  
- **Searching Algorithms**: Linear Search, Binary Search (find elements).  
- **Graph Algorithms**: Dijkstra’s, BFS, DFS (find shortest path, traverse).  
- **Dynamic Programming**: Solve problems by breaking them into overlapping subproblems (e.g., Fibonacci, Knapsack).  


## 3. Why DSA is Important
- Makes programs **faster** (better performance).  
- Makes programs **scalable** (handle more data efficiently).  
- Helps in **problem-solving and coding interviews** (big tech companies focus heavily on DSA).  
- Forms the foundation for advanced topics like **databases, operating systems, AI, and machine learning**.  


## 🔑 In Short
- **Data Structures** = *how you store data.*  
- **Algorithms** = *how you manipulate data.*  
Together, they allow you to **build efficient, reliable, and scalable software**.  
# Tree - An In-Depth Guide

## 1. Introduction

Trees are hierarchical data structures that represent relationships in a parent-child form. Unlike linear structures (arrays, linked lists, queues, stacks), trees provide a way to model hierarchical data like organizational charts, file systems, and decision processes.


## 2. What is a Tree?

A **Tree** is a collection of nodes connected by edges, where:

* One node is designated as the **root**.
* Every node (except the root) has exactly one parent.
* Nodes may have zero or more children.

Example (visual representation):

```
        A (root)
       / \
      B   C
     / \   \
    D   E   F
```


## 3. Properties of Trees

* **Root:** The topmost node of the tree.
* **Parent and Child:** Relationship between connected nodes.
* **Leaf Node:** A node with no children.
* **Height of Tree:** Length of the longest path from root to a leaf.
* **Depth of Node:** Distance from the root to that node.
* **Subtree:** A tree formed by a node and its descendants.


## 4. Advantages of Trees

* Represent hierarchical data naturally.
* Efficient searching, insertion, and deletion (in balanced trees).
* Basis for advanced data structures like Heaps, Tries, and Binary Search Trees.


## 5. Types of Trees

* **General Tree:** Each node can have arbitrary number of children.
* **Binary Tree:** Each node has at most two children (left and right).
* **Binary Search Tree (BST):** A binary tree with ordered left and right subtrees.
* **Balanced Trees (AVL, Red-Black):** Maintain balance to ensure O(log n) operations.
* **Heap:** A binary tree used in priority queues.
* **Trie:** Specialized tree for storing strings.


## 6. Common Operations on Trees

### 6.1 Traversals

Traversal means visiting all nodes in a specific order.

#### Inorder Traversal (Left → Root → Right)

```python
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# Inorder Traversal
def inorder(root):
    if root:
        inorder(root.left)
        print(root.key, end=" ")
        inorder(root.right)

# Example
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)

inorder(root)  # Output: 4 2 5 1 3
```

#### Preorder Traversal (Root → Left → Right)

```python
def preorder(root):
    if root:
        print(root.key, end=" ")
        preorder(root.left)
        preorder(root.right)

preorder(root)  # Output: 1 2 4 5 3
```

#### Postorder Traversal (Left → Right → Root)

```python
def postorder(root):
    if root:
        postorder(root.left)
        postorder(root.right)
        print(root.key, end=" ")

postorder(root)  # Output: 4 5 2 3 1
```

#### Level Order Traversal (Breadth-First Search)

```python
from collections import deque

def level_order(root):
    if not root:
        return
    queue = deque([root])
    while queue:
        node = queue.popleft()
        print(node.key, end=" ")
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)

level_order(root)  # Output: 1 2 3 4 5
```

##### ASCII Visual: Traversal Orders on the Sample Tree

```
        1
       / \
      2   3
     / \
    4   5
```

* Inorder   (L,Root,R): **4 → 2 → 5 → 1 → 3**
* Preorder  (Root,L,R): **1 → 2 → 4 → 5 → 3**
* Postorder (L,R,Root): **4 → 5 → 2 → 3 → 1**
* Level-order (BFS):    **1 → 2 → 3 → 4 → 5**

**Diagram for Level Order Traversal:**

```
Traversal order by levels: 1 → 2 → 3 → 4 → 5
```

---

### 6.2 Insertion in a Binary Search Tree (BST)

```python
def insert(root, key):
    if root is None:
        return Node(key)
    if key < root.key:
        root.left = insert(root.left, key)
    else:
        root.right = insert(root.right, key)
    return root

root = None
root = insert(root, 50)
insert(root, 30)
insert(root, 20)
insert(root, 40)
insert(root, 70)
insert(root, 60)
insert(root, 80)
```

##### ASCII Visual: Inserting 65 into the BST

Before:

```
        50
       /  \
     30    70
    /  \   / \
   20  40 60  80
```

Path for 65: **50 → 70 → 60 → (right is empty)**

After inserting 65:

```
        50
       /  \
     30    70
    /  \   / \
   20  40 60  80
             \
             65
```

```

**Diagram after insertions:**
```

```
      50
     /  \
   30    70
  / \    / \
20  40  60  80
```

````

---

### 6.3 Searching in a Binary Search Tree
```python
def search(root, key):
    if root is None or root.key == key:
        return root
    if key < root.key:
        return search(root.left, key)
    return search(root.right, key)

node = search(root, 40)
print("Found" if node else "Not Found")  # Output: Found
````

**Diagram of search for 40:**

```
Search path: 50 → 30 → 40 (Found)
```

---

### 6.4 Deletion in a BST

```python
def delete(root, key):
    if root is None:
        return root
    if key < root.key:
        root.left = delete(root.left, key)
    elif key > root.key:
        root.right = delete(root.right, key)
    else:
        # Case 1: No child
        if root.left is None:
            return root.right
        elif root.right is None:
            return root.left
        # Case 2: Two children — replace with inorder successor
        temp = minValueNode(root.right)
        root.key = temp.key
        root.right = delete(root.right, temp.key)
    return root

def minValueNode(node):
    current = node
    while current.left is not None:
        current = current.left
    return current

root = delete(root, 20)
```

##### ASCII Visuals: Deletion Cases

**Case A — Delete a leaf (20):**

```
Before                After
------                -----
   30                    30
  /  \                  /  \
20   40       →        X    40
```

**Case B — Delete a node with one child (30 has only left child 25):**

```
Before                After
------                -----
   30                   25
  /          →           
25                        
```

**Case C — Delete a node with two children (delete 50, replace with inorder successor 60):**

```
Before:
        50
       /  \
     30    70
          /  \
         60   80

After:
        60
       /  \
     30    70
            \
            80
```

```

**Diagram of deletion (delete 20):**
```

Before:                  After:
50                      50
/  \                    / &#x20;
30    70                30    70
/ \    / \                  \   /&#x20;
20  40  60  80                40 60  80

```


## 7. Time and Space Complexity of Tree Operations

| Operation              | Average Case | Worst Case (Skewed Tree) |
| ---------------------- | ------------ | ------------------------- |
| Search (BST)           | O(log n)     | O(n)                     |
| Insertion (BST)        | O(log n)     | O(n)                     |
| Deletion (BST)         | O(log n)     | O(n)                     |
| Traversals             | O(n)         | O(n)                     |

*Balanced trees like AVL or Red-Black maintain O(log n) complexity.*


## 8. Real-World Applications of Trees

* **File Systems:** Directory and files are represented as trees.
* **Databases:** Indexing with B-trees and B+ trees.
* **Compilers:** Abstract syntax trees for parsing.
* **Artificial Intelligence:** Decision trees for classification.
* **Networking:** Routing algorithms use spanning trees.


## 9. Comparison with Other Data Structures

* **Trees vs Arrays:** Arrays are linear and allow random access; trees are hierarchical and efficient for sorted data operations.
* **Trees vs Linked Lists:** Linked lists are sequential, trees allow branching.
* **Trees vs Hash Tables:** Hash tables provide O(1) average access, but trees maintain sorted order and allow range queries.

## 10. Conclusion

Trees are powerful hierarchical structures that enable efficient searching, sorting, and hierarchical data storage. Understanding traversal methods, insertion, deletion, and searching forms the foundation for advanced data structures like AVL Trees, Red-Black Trees, and Heaps.
