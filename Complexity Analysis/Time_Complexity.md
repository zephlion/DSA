# Time Complexity - An In-Depth Guide

## 1. Introduction

Time complexity is a measure of the computational time an algorithm takes to complete as a function of the size of the input. It provides a way to evaluate the efficiency of an algorithm and compare multiple approaches to solving the same problem.


## 2. What is Time Complexity?

Time complexity refers to the number of basic operations executed by an algorithm relative to the input size `n`. It helps us understand how the algorithm scales as the input grows.


## 3. Importance of Time Complexity

* Predicts algorithm performance on large inputs.
* Helps compare efficiency across different algorithms.
* Guides developers in choosing scalable solutions.
* Prevents inefficiencies that may cause slow execution.


## 4. Measuring Time Complexity

### Basic Operations

The time complexity depends on the count of fundamental operations (e.g., comparisons, additions, assignments).

### Input Size (n)

`n` usually represents the size of the input (e.g., array length, number of nodes in a graph).

### Counting Steps

Steps are approximated by analyzing loops, recursive calls, and function calls.


## 5. Big O Notation

Big O expresses the **upper bound** (worst-case growth rate) of an algorithm.

### Rules for Simplifying Big O

1. Drop constants (O(2n) → O(n)).
2. Drop less significant terms (O(n² + n) → O(n²)).
3. Focus on growth as `n` → ∞.

### Common Complexities

* **O(1)** – Constant time (e.g., accessing an array element).
* **O(log n)** – Logarithmic time (e.g., binary search).
* **O(n)** – Linear time (e.g., iterating through an array).
* **O(n log n)** – Log-linear time (e.g., merge sort).
* **O(n²)** – Quadratic time (e.g., nested loops, bubble sort).
* **O(2ⁿ)** – Exponential time (e.g., recursive subset generation).
* **O(n!)** – Factorial time (e.g., brute-force permutations).


## 6. Big Omega (Ω) and Big Theta (Θ)

* **Ω (Big Omega)**: Best-case complexity (minimum time).
* **Θ (Big Theta)**: Tight bound; represents average case or typical growth.
* **O (Big O)**: Worst-case complexity.


## 7. Best Case, Worst Case, and Average Case

* **Best Case**: Minimum time (Ω) – Example: Linear search finds element at index 0 → O(1).
* **Worst Case**: Maximum time (O) – Example: Linear search checks entire array → O(n).
* **Average Case**: Expected performance (Θ) – Example: Linear search finds element halfway → O(n/2) ≈ O(n).


## 8. Time Complexity of Common Algorithms

### Searching

* Linear Search: O(n)
* Binary Search: O(log n)

### Sorting

* Bubble Sort: O(n²)
* Insertion Sort: O(n²)
* Merge Sort: O(n log n)
* Quick Sort: O(n log n) average, O(n²) worst case

### Graph Traversals

* Breadth-First Search (BFS): O(V + E)
* Depth-First Search (DFS): O(V + E)

### Dynamic Programming Examples

* Fibonacci (recursive): O(2ⁿ)
* Fibonacci (DP): O(n)


## 9. Analyzing Loops and Recursion

### Single Loops

```python
for i in range(n):
    print(i)
```

Time complexity: O(n).

### Nested Loops

```python
for i in range(n):
    for j in range(n):
        print(i, j)
```

Time complexity: O(n²).

### Multiple Independent Loops

```python
for i in range(n):
    print(i)
for j in range(m):
    print(j)
```

Time complexity: O(n + m).

### Recursive Algorithms

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n-1)
```

Time complexity: O(n).

Example (divide and conquer):

* Merge Sort recursion depth = log n → O(n log n).


## 10. Amortized Time Complexity

Amortized analysis averages costly operations over many cheap ones.

Examples:

* **Dynamic Arrays**: Appending is usually O(1), but occasional resizing takes O(n). Amortized: O(1).
* **Hash Tables**: Rehashing occasionally takes O(n), but insertions are O(1) on average.


## 11. Visualizing Time Complexity

### Growth Rate Comparisons

* O(1) → Flat line.
* O(log n) → Grows slowly.
* O(n) → Straight line.
* O(n log n) → Slightly steeper than linear.
* O(n²) → Parabolic growth.
* O(2ⁿ), O(n!) → Explosive growth.

### Example Table

| Complexity | n = 10 | n = 100 | n = 1000  |
| ---------- | ------ | ------- | --------- |
| O(1)       | 1      | 1       | 1         |
| O(log n)   | 3      | 7       | 10        |
| O(n)       | 10     | 100     | 1000      |
| O(n log n) | 33     | 664     | 10,000    |
| O(n²)      | 100    | 10,000  | 1,000,000 |
| O(2ⁿ)      | 1024   | \~10³⁰  | \~10³⁰⁰   |
| O(n!)      | 3.6M   | \~10¹⁵⁷ | \~10²⁵⁶⁷  |


## 12. Real-World Applications

* Web search algorithms must scale with billions of queries → O(log n) preferred.
* Sorting algorithms in databases → O(n log n).
* Machine learning preprocessing for large datasets.
* Cryptography relies on computational hardness (e.g., exponential complexity problems).


## 13. Conclusion

Time complexity is crucial for analyzing algorithm efficiency. By mastering Big O, Ω, Θ, and amortized analysis, developers can design algorithms that are both scalable and practical. Understanding growth rates ensures systems remain efficient as input sizes increase.
