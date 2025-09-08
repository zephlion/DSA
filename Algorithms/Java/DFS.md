# Depth-First Search (DFS) - An In-Depth Guide (Java Version)

## 1. Introduction

Depth-First Search (DFS) is a fundamental graph traversal algorithm that explores as far as possible along one branch before backtracking. It is widely used in pathfinding, cycle detection, topological sorting, and solving puzzles.

## 2. What is DFS?

DFS starts from a source node and explores each branch deeply before moving to another branch. It can be implemented using **recursion (system call stack)** or an **explicit stack**.

## 3. Properties of DFS

* **Traversal order:** Goes deep along a path before backtracking.
* **Data structure used:** Stack (explicit or implicit via recursion).
* **Connectivity:** Can explore connected components in a graph.

## 4. Step-by-Step Working with Example

Consider the following undirected graph:

```
Graph:
    A
   / \
  B   C
 / \   \
D   E   F
```

### Adjacency List Representation

```
A: [B, C]
B: [A, D, E]
C: [A, F]
D: [B]
E: [B]
F: [C]
```

### DFS Traversal (starting from A)

Traversal order: **A → B → D → E → C → F**

### ASCII Visualization of DFS

```
Stack changes during DFS (explicit stack):
Start: [A]
Visit A → Push [C, B]
Stack: [C, B]
Visit B → Push [E, D]
Stack: [C, E, D]
Visit D → Pop → Stack: [C, E]
Visit E → Pop → Stack: [C]
Visit C → Push [F]
Stack: [F]
Visit F → Pop → Stack: []
```

## 5. DFS Algorithm (Java Implementation)

### Recursive Implementation

```java
import java.util.*;

public class DFSRecursiveExample {

    public static void dfsRecursive(Map<String, List<String>> graph, String node, Set<String> visited) {
        if (!visited.contains(node)) {
            System.out.print(node + " ");
            visited.add(node);
            for (String neighbor : graph.get(node)) {
                dfsRecursive(graph, neighbor, visited);
            }
        }
    }

    public static void main(String[] args) {
        // Example graph
        Map<String, List<String>> graph = new HashMap<>();
        graph.put("A", Arrays.asList("B", "C"));
        graph.put("B", Arrays.asList("A", "D", "E"));
        graph.put("C", Arrays.asList("A", "F"));
        graph.put("D", Arrays.asList("B"));
        graph.put("E", Arrays.asList("B"));
        graph.put("F", Arrays.asList("C"));

        Set<String> visited = new HashSet<>();
        dfsRecursive(graph, "A", visited); // Output: A B D E C F
    }
}
```

### Iterative Implementation using Stack

```java
import java.util.*;

public class DFSIterativeExample {

    public static void dfsIterative(Map<String, List<String>> graph, String start) {
        Set<String> visited = new HashSet<>();
        Stack<String> stack = new Stack<>();
        stack.push(start);

        while (!stack.isEmpty()) {
            String node = stack.pop();
            if (!visited.contains(node)) {
                System.out.print(node + " ");
                visited.add(node);

                // Add neighbors in reverse order to maintain traversal order
                List<String> neighbors = graph.get(node);
                ListIterator<String> it = neighbors.listIterator(neighbors.size());
                while (it.hasPrevious()) {
                    String neighbor = it.previous();
                    if (!visited.contains(neighbor)) {
                        stack.push(neighbor);
                    }
                }
            }
        }
    }

    public static void main(String[] args) {
        // Example graph
        Map<String, List<String>> graph = new HashMap<>();
        graph.put("A", Arrays.asList("B", "C"));
        graph.put("B", Arrays.asList("A", "D", "E"));
        graph.put("C", Arrays.asList("A", "F"));
        graph.put("D", Arrays.asList("B"));
        graph.put("E", Arrays.asList("B"));
        graph.put("F", Arrays.asList("C"));

        dfsIterative(graph, "A"); // Output: A B D E C F
    }
}
```

## 6. Time and Space Complexity

| Operation     | Time Complexity | Space Complexity |
| ------------- | --------------- | ---------------- |
| DFS Traversal | O(V + E)        | O(V)             |

Where:

* **V** = Number of vertices
* **E** = Number of edges

## 7. Advantages of DFS

* Simple and easy to implement.
* Requires less memory than BFS in sparse graphs.
* Useful for pathfinding and cycle detection.
* Backbone for algorithms like topological sort and strongly connected components.

## 8. Disadvantages of DFS

* May get stuck in deep or infinite paths if cycles aren’t handled.
* Not guaranteed to find the shortest path (unlike BFS).

## 9. Real-World Applications of DFS

* **Pathfinding:** Solving mazes and puzzles.
* **Cycle Detection:** Detecting cycles in graphs.
* **Topological Sorting:** For dependency resolution.
* **Connected Components:** Finding isolated subgraphs.
* **Artificial Intelligence:** Backtracking-based problem solving (e.g., Sudoku, N-Queens).

## 10. Conclusion

DFS is a core algorithm in graph theory that explores deeply before backtracking. Its recursive nature makes it elegant, and its stack-based approach ensures systematic traversal. Despite not always finding the shortest path, it plays a vital role in many graph-based and AI algorithms.
