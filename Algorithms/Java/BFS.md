# Breadth-First Search (BFS) - An In-Depth Guide (Java Version)

## 1. Introduction

**Breadth-First Search (BFS)** is one of the fundamental graph traversal algorithms. It explores vertices of a graph in layers, starting from a source vertex and visiting all its neighbors before moving on to the next level of neighbors.

BFS is widely used for **shortest path in unweighted graphs**, **web crawling**, **social network analysis**, and **network broadcasting**.

## 2. What is BFS?

BFS systematically explores a graph level by level:

* Start from a source vertex.
* Visit all immediate neighbors.
* Then visit neighbors of neighbors, and so on.

It uses a **queue** data structure to keep track of nodes to be visited.

## 3. Properties of BFS

* Traverses level by level.
* Uses a **queue** for order of exploration.
* Guarantees the **shortest path** in an unweighted graph.
* Time complexity depends on number of vertices (V) and edges (E).

## 4. Step-by-Step Example

Consider the following undirected graph:

```
   A
  / \
 B   C
 |   |
 D---E
```

### BFS Process with Queue Visualization

| Step | Action            | Queue State | Visited Set     | Traversal Order  |
| ---- | ----------------- | ----------- | --------------- | ---------------- |
| 1    | Start at A        | \[A]        | {}              | \[]              |
| 2    | Dequeue A → visit | \[B, C]     | {A}             | \[A]             |
| 3    | Dequeue B → visit | \[C, D]     | {A, B}          | \[A, B]          |
| 4    | Dequeue C → visit | \[D, E]     | {A, B, C}       | \[A, B, C]       |
| 5    | Dequeue D → visit | \[E]        | {A, B, C, D}    | \[A, B, C, D]    |
| 6    | Dequeue E → visit | \[]         | {A, B, C, D, E} | \[A, B, C, D, E] |

**Final BFS Traversal Order:** A → B → C → D → E

## 5. BFS Algorithm (Java Implementation)

```java
import java.util.*;

public class BFSExample {

    public static List<String> bfs(Map<String, List<String>> graph, String start) {
        Set<String> visited = new HashSet<>();
        Queue<String> queue = new LinkedList<>();
        List<String> traversalOrder = new ArrayList<>();

        queue.add(start);

        while (!queue.isEmpty()) {
            String vertex = queue.poll(); // Dequeue
            if (!visited.contains(vertex)) {
                visited.add(vertex);
                traversalOrder.add(vertex);

                // Add unvisited neighbors
                for (String neighbor : graph.get(vertex)) {
                    if (!visited.contains(neighbor)) {
                        queue.add(neighbor);
                    }
                }
            }
        }

        return traversalOrder;
    }

    public static void main(String[] args) {
        // Example graph (Adjacency List)
        Map<String, List<String>> graph = new HashMap<>();
        graph.put("A", Arrays.asList("B", "C"));
        graph.put("B", Arrays.asList("A", "D"));
        graph.put("C", Arrays.asList("A", "E"));
        graph.put("D", Arrays.asList("B", "E"));
        graph.put("E", Arrays.asList("C", "D"));

        List<String> result = bfs(graph, "A");
        System.out.println(result);
    }
}
```

### Explanation of Code

1. **Initialize queue** with the starting node.
2. **Use a set `visited`** to track visited nodes.
3. **While the queue is not empty:**

   * Dequeue a node.
   * If unvisited, mark it visited and add its neighbors to the queue.
4. Continue until all reachable nodes are visited.

### Output:

```
[A, B, C, D, E]
```

## 6. Time and Space Complexity

| Operation        | Complexity                                   |
| ---------------- | -------------------------------------------- |
| Time Complexity  | **O(V + E)** (visit each vertex & edge once) |
| Space Complexity | **O(V)** (queue + visited set)               |

## 7. Advantages of BFS

* Finds **shortest path** in unweighted graphs.
* Explores nodes level by level.
* Simple and systematic.

## 8. Disadvantages of BFS

* Requires more memory (queue + visited set).
* Slower compared to DFS in deep but sparse graphs.

## 9. Real-World Applications

* **Shortest path finding** in GPS/navigation.
* **Social networks** (finding friends-of-friends).
* **Web crawlers** (traverse web pages layer by layer).
* **Broadcasting** in computer networks.

## 10. Conclusion

Breadth-First Search is a fundamental algorithm for graph traversal that guarantees shortest paths in unweighted graphs. By mastering BFS, one builds a strong foundation for understanding more advanced algorithms like **Dijkstra’s** and **A**\*.
