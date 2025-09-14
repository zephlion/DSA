# Java DSA Guide — Arrays

*A comprehensive, in-depth guide to arrays for Java developers preparing for interviews or building production systems.*

---

## Table of contents

1. [Introduction](#introduction)
2. [Arrays](#arrays)

   * [Definitions & characteristics](#definitions--characteristics)
   * [Declaration & initialization in Java](#declaration--initialization-in-java)
   * [Core operations and time/space complexity](#core-operations-and-timecomplexity)
   * [Common patterns & algorithms](#common-patterns--algorithms)
   * [Practical examples & code](#practical-examples--code)
   * [When to use arrays vs ArrayList](#when-to-use-arrays-vs-arraylist)
   * [Edge cases and pitfalls](#edge-cases-and-pitfalls)
3. [Practice problems & solutions](#practice-problems--solutions)
4. [Cheat sheet: complexities & quick patterns](#cheat-sheet-complexities--quick-patterns)

---

# Introduction

Arrays are foundational data structures. They provide contiguous memory storage and constant-time indexed access. Mastering arrays — their strengths, trade-offs, and algorithmic patterns — is crucial for writing fast, correct Java code and for interview success.

---

# Arrays

## Definitions & characteristics

* **Array**: A fixed-size, contiguous block of memory storing elements of the same type.
* **Properties**:

  * Indexed access in O(1).
  * Fixed capacity (native arrays).
  * Good locality of reference (cache-friendly).

## Declaration & initialization in Java

```java
// primitive array
int[] a = new int[10];
int[] b = {1, 2, 3, 4};

// array of objects
String[] s = new String[5];

// multi-dimensional
int[][] matrix = new int[3][4];
```

## Core operations and time/space complexity

* Access `a[i]`: O(1)
* Update `a[i]`: O(1)
* Iterate: O(n)
* Search (unsorted) linear: O(n)
* Insert/delete at end (if space): O(1) for dynamic array; at arbitrary index: O(n)
* Space: O(n)

## Common patterns & algorithms

### 1) Two pointers

```java
public boolean twoSumSorted(int[] nums, int target) {
    int l = 0, r = nums.length - 1;
    while (l < r) {
        int sum = nums[l] + nums[r];
        if (sum == target) return true;
        if (sum < target) l++; else r--;
    }
    return false;
}
```

### 2) Sliding window

Used for subarray / substring problems (max/min sum/length).

### 3) Prefix sums

```java
int[] prefix = new int[n+1];
for (int i = 0; i < n; i++) prefix[i+1] = prefix[i] + arr[i];
// sum of arr[l..r] = prefix[r+1] - prefix[l]
```

### 4) Sorting first

Sorting simplifies many array problems (two-pointer, duplicates).

### 5) In-place modification & tricks

* Mark visited indices.
* Use XOR for swaps (not recommended for readability).

## Practical examples & code

### Reverse an array

```java
public void reverse(int[] a) {
    int l = 0, r = a.length - 1;
    while (l < r) {
        int tmp = a[l];
        a[l++] = a[r];
        a[r--] = tmp;
    }
}
```

### Move zeros to the end

```java
public void moveZeroes(int[] nums) {
    int j = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != 0) nums[j++] = nums[i];
    }
    while (j < nums.length) nums[j++] = 0;
}
```

### Kadane’s algorithm

```java
public int maxSubArray(int[] nums) {
    int best = nums[0];
    int cur = nums[0];
    for (int i = 1; i < nums.length; i++) {
        cur = Math.max(nums[i], cur + nums[i]);
        best = Math.max(best, cur);
    }
    return best;
}
```

### Binary search

```java
public int binarySearch(int[] a, int target) {
    int l = 0, r = a.length - 1;
    while (l <= r) {
        int mid = l + (r - l) / 2;
        if (a[mid] == target) return mid;
        if (a[mid] < target) l = mid + 1; else r = mid - 1;
    }
    return -1;
}
```

## When to use arrays vs ArrayList

* Arrays: fixed size, primitive performance.
* ArrayList: dynamic size, convenient API.

## Edge cases and pitfalls

* Out-of-bounds.
* Null arrays.
* Integer overflow when summing.

---

# Practice problems & solutions

1. Reverse an array in place.
2. Move zeros to end.
3. Kadane’s algorithm.
4. Binary search variants.
5. Find missing number using XOR.

---

# Cheat sheet: complexities & quick patterns

* Access: O(1)
* Insert/delete arbitrary index: O(n)
* Search: O(n) unsorted, O(log n) sorted
* Sort: O(n log n)

Patterns:

* Two pointers
* Sliding window
* Prefix sums
* Sorting + two-pointer