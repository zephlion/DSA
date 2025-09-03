# Graph - An In-Depth Guide

## 1. Introduction

Graphs are one of the most versatile and widely used data structures in computer science. They are used to model relationships between entities, such as social networks, transportation systems, and the web.

## 2. What is a Graph?

A graph is a collection of **nodes (vertices)** connected by **edges**. Graphs can be:

* **Directed or Undirected**: Edges may have a direction (one-way) or no direction (two-way).
* **Weighted or Unweighted**: Edges may carry weights (like distance, cost, or capacity).
* **Cyclic or Acyclic**: Graphs may contain cycles (loops) or be cycle-free.

Example representation:

```
Vertices: {A, B, C, D}
Edges: {(A,B), (A,C), (B,D), (C,D)}
```

**Visual (Adjacency Representation):**

```
A → B → D
  ↘ C → D
B → D
C → D
D
```

## 3. Properties of Graphs

* **V** = number of vertices
* **E** = number of edges
* Sparse graph: E << V²
* Dense graph: E ≈ V²
* Representations: adjacency matrix, adjacency list, edge list

## 4. Advantages of Graphs

* Flexible to represent complex relationships.
* Efficient algorithms exist for traversal, shortest paths, spanning trees, etc.
* Widely applicable in real-world domains.

## 5. Disadvantages of Graphs

* Can be memory-intensive, especially adjacency matrices for sparse graphs.
* Algorithm complexity can be high (e.g., shortest path, max flow).
* Implementation can be more complex compared to linear structures.

## 6. Types of Graphs

* **Undirected Graph**: Edges have no direction.
* **Directed Graph (Digraph)**: Edges have direction.
* **Weighted Graph**: Each edge has an associated weight.
* **DAG (Directed Acyclic Graph)**: Directed with no cycles.
* **Complete Graph**: Every vertex is connected to every other vertex.

## 7. Graph Representations in Python

### Adjacency List

```python
# Using a dictionary of lists
graph = {
    'A': ['B', 'C'],
    'B': ['D'],
    'C': ['D'],
    'D': []
}
```

**Diagram (Adjacency List):**

```
A: B, C
B: D
C: D
D:
```

### Adjacency Matrix

```python
# For 4 vertices: A, B, C, D
# 0 = no edge, 1 = edge exists
matrix = [
    [0, 1, 1, 0],  # A
    [0, 0, 0, 1],  # B
    [0, 0, 0, 1],  # C
    [0, 0, 0, 0]   # D
]
```

**Diagram (Adjacency Matrix):**

```
    A B C D
A | 0 1 1 0
B | 0 0 0 1
C | 0 0 0 1
D | 0 0 0 0
```

## 8. Common Operations on Graphs

### Add Vertex

```python
def add_vertex(graph, v):
    if v not in graph:
        graph[v] = []

add_vertex(graph, 'E')
```

### Add Edge

```python
def add_edge(graph, u, v):
    if u in graph:
        graph[u].append(v)
    else:
        graph[u] = [v]

add_edge(graph, 'A', 'E')
```

### Traversals

**Breadth-First Search (BFS)**

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])

    while queue:
        vertex = queue.popleft()
        if vertex not in visited:
            print(vertex, end=" ")
            visited.add(vertex)
            queue.extend(graph[vertex])

bfs(graph, 'A')
```

**Example Traversal (BFS):**

```
A B C D
```

**Depth-First Search (DFS)**

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    if start not in visited:
        print(start, end=" ")
        visited.add(start)
        for neighbor in graph[start]:
            dfs(graph, neighbor, visited)

dfs(graph, 'A')
```

**Example Traversal (DFS):**

```
A B D C
```

### Search for an Element

```python
def search(graph, start, target):
    visited = set()
    queue = [start]
    while queue:
        node = queue.pop(0)
        if node == target:
            return True
        if node not in visited:
            visited.add(node)
            queue.extend(graph[node])
    return False

print(search(graph, 'A', 'D'))  # True
```

## 9. Time and Space Complexity

| Operation           | Adjacency List | Adjacency Matrix |
| ------------------- | -------------- | ---------------- |
| Add Vertex          | O(1)           | O(V²)            |
| Add Edge            | O(1)           | O(1)             |
| Remove Edge         | O(E)           | O(1)             |
| BFS / DFS Traversal | O(V + E)       | O(V²)            |

## 10. Real-World Applications

* **Social Networks**: Users as nodes, friendships as edges.
* **Navigation Systems**: Cities as nodes, roads as edges.
* **Web Crawling**: Web pages as nodes, hyperlinks as edges.
* **Recommendation Systems**: Items and users as nodes, preferences as edges.
* **Dependency Resolution**: Build systems, package managers.

## 11. Comparison with Other Data Structures

* **Graphs vs Trees**: A tree is a special type of graph (connected, acyclic). Graphs are more general.
* **Graphs vs Arrays/Lists**: Arrays/lists represent linear data, while graphs represent relationships.
* **Graphs vs Hash Tables**: Hash tables store key-value mappings, while graphs store relational mappings.

## 12. Conclusion

Graphs are powerful structures that model relationships between entities. With traversal and pathfinding algorithms, they become indispensable in problem-solving across domains like networking, AI, and data science.
