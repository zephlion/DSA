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

## 7. Graph Representations in Java

### Adjacency List

```java
import java.util.*;

class Graph {
    private Map<String, List<String>> adjList = new HashMap<>();

    public void addVertex(String v) {
        adjList.putIfAbsent(v, new ArrayList<>());
    }

    public void addEdge(String u, String v) {
        adjList.get(u).add(v);
    }

    public void printGraph() {
        for (var entry : adjList.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}

public class GraphExample {
    public static void main(String[] args) {
        Graph graph = new Graph();
        graph.addVertex("A");
        graph.addVertex("B");
        graph.addVertex("C");
        graph.addVertex("D");

        graph.addEdge("A", "B");
        graph.addEdge("A", "C");
        graph.addEdge("B", "D");
        graph.addEdge("C", "D");

        graph.printGraph();
    }
}
```

### Adjacency Matrix

```java
class GraphMatrix {
    private int[][] matrix;
    private String[] vertices;

    public GraphMatrix(int size, String[] labels) {
        matrix = new int[size][size];
        vertices = labels;
    }

    public void addEdge(int u, int v) {
        matrix[u][v] = 1; // directed graph
    }

    public void printMatrix() {
        System.out.print("    ");
        for (String vertex : vertices) {
            System.out.print(vertex + " ");
        }
        System.out.println();

        for (int i = 0; i < matrix.length; i++) {
            System.out.print(vertices[i] + " | ");
            for (int j = 0; j < matrix[i].length; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}

public class GraphMatrixExample {
    public static void main(String[] args) {
        String[] vertices = {"A", "B", "C", "D"};
        GraphMatrix gm = new GraphMatrix(4, vertices);

        gm.addEdge(0, 1); // A → B
        gm.addEdge(0, 2); // A → C
        gm.addEdge(1, 3); // B → D
        gm.addEdge(2, 3); // C → D

        gm.printMatrix();
    }
}
```

## 8. Common Operations on Graphs

### Add Vertex & Edge

Already shown in adjacency list implementation.

### Traversals

**Breadth-First Search (BFS)**

```java
public void bfs(String start) {
    Set<String> visited = new HashSet<>();
    Queue<String> queue = new LinkedList<>();
    queue.add(start);

    while (!queue.isEmpty()) {
        String vertex = queue.poll();
        if (!visited.contains(vertex)) {
            System.out.print(vertex + " ");
            visited.add(vertex);
            queue.addAll(adjList.get(vertex));
        }
    }
}
```

**Depth-First Search (DFS)**

```java
public void dfs(String start, Set<String> visited) {
    if (!visited.contains(start)) {
        System.out.print(start + " ");
        visited.add(start);
        for (String neighbor : adjList.get(start)) {
            dfs(neighbor, visited);
        }
    }
}
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
