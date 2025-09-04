# Hash Table - An In-Depth Guide

## 1. Introduction

Hash tables (also called hash maps or dictionaries) are a fundamental data structure that provide efficient average‑case lookup, insertion, and deletion. They map keys to values using a hash function that computes an index into an internal array (bucket), enabling near‑constant time access on average.

## 2. What is a Hash Table?

A hash table stores key‑value pairs. For each key, a **hash function** computes an index (bucket) where the value is stored. When multiple keys map to the same bucket—**collisions**—a collision resolution strategy is used (chaining, open addressing, etc.).

Example (built‑in Python dict):

```python
m = {'apple': 3, 'banana': 5}
print(m['apple'])  # 3
m['cherry'] = 7    # insert
```

## 3. Properties of Hash Tables

* **Average-case O(1)** for lookup, insertion, and deletion.
* **Unordered:** No guarantee of order (in older Python versions; modern Python preserves insertion order but that is not a hashing property).
* **Hashable keys:** Keys must be hashable (implement `__hash__` and `__eq__` consistently).
* **Load factor:** Ratio of stored elements to bucket array size; controls resizing.

## 4. Advantages of Hash Tables

* Extremely fast average lookups and updates.
* Flexible key types (strings, tuples, numbers, custom immutable objects).
* Powerful building block for many algorithms and systems (caching, indexes).

## 5. Disadvantages of Hash Tables

* Worst‑case O(n) operations under pathological collisions or poor hash functions.
* Extra memory overhead for buckets and metadata.
* Unordered by nature (unless augmented).
* Harder to support ordered traversal or range queries—trees are better for that.

## 6. Types and Collision Resolution Strategies

* **Chaining (Separate Chaining):** Each bucket holds a linked list (or dynamic array) of entries. Collisions add elements to that list.
* **Open Addressing:** All entries stored in the bucket array. On collision, probe to find another free slot (linear probing, quadratic probing, double hashing).
* **Perfect Hashing / Cuckoo Hashing / Hopscotch:** Advanced strategies for performance guarantees.


## 7. Common Operations (with Python examples and explanations)

### 7.1 Simple usage with `dict`

```python
# create
phone = {'alice': '555-1234', 'bob': '555-5678'}

# lookup
print(phone.get('alice'))     # '555-1234'
print(phone.get('carol', None))  # None if not found

# insert/update
phone['dave'] = '555-9999'

# delete
phone.pop('bob', None)  # remove safely

# iterate
for name, number in phone.items():
    print(name, number)
```

*Explanation:* Python's `dict` is a highly optimized hash table. `get` avoids `KeyError` and supports a default value. Iteration yields items in insertion order (implementation detail since CPython 3.7).

---

### 7.2 Implementing a simple hash table with chaining

```python
class HashTableChaining:
    def __init__(self, capacity=8):
        self.capacity = capacity
        self.buckets = [[] for _ in range(capacity)]
        self.size = 0

    def _hash(self, key):
        return hash(key) % self.capacity

    def put(self, key, value):
        idx = self._hash(key)
        bucket = self.buckets[idx]
        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket[i] = (key, value)
                return
        bucket.append((key, value))
        self.size += 1
        # optional: resize when load factor high

    def get(self, key):
        idx = self._hash(key)
        bucket = self.buckets[idx]
        for k, v in bucket:
            if k == key:
                return v
        raise KeyError(key)

    def remove(self, key):
        idx = self._hash(key)
        bucket = self.buckets[idx]
        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket.pop(i)
                self.size -= 1
                return
        raise KeyError(key)
```

*Explanation:* Each bucket is a Python list of `(key, value)` pairs. `_hash` maps keys to bucket indices. `put` replaces existing key or appends a new pair; `get` and `remove` scan the bucket. Average cost is O(1) if buckets remain small; worst-case O(n) if all keys collide into one bucket.

---

### 7.3 Open Addressing (linear probing) — simplified example

```python
class HashTableLinearProbing:
    def __init__(self, capacity=8):
        self.capacity = capacity
        self.keys = [None] * capacity
        self.values = [None] * capacity
        self.size = 0

    def _hash(self, key):
        return hash(key) % self.capacity

    def put(self, key, value):
        idx = self._hash(key)
        start = idx
        while self.keys[idx] is not None and self.keys[idx] != key:
            idx = (idx + 1) % self.capacity
            if idx == start:
                raise RuntimeError('HashTable full')
        if self.keys[idx] is None:
            self.size += 1
        self.keys[idx] = key
        self.values[idx] = value

    def get(self, key):
        idx = self._hash(key)
        start = idx
        while self.keys[idx] is not None:
            if self.keys[idx] == key:
                return self.values[idx]
            idx = (idx + 1) % self.capacity
            if idx == start:
                break
        raise KeyError(key)

    def remove(self, key):
        # naive remove: find and mark None (can break probe chain)
        idx = self._hash(key)
        start = idx
        while self.keys[idx] is not None:
            if self.keys[idx] == key:
                self.keys[idx] = None
                self.values[idx] = None
                self.size -= 1
                return
            idx = (idx + 1) % self.capacity
            if idx == start:
                break
        raise KeyError(key)
```

*Explanation:* Linear probing stores entries directly in arrays and searches consecutively from the hashed index. It is memory efficient but requires careful handling of deletes and resizing to avoid clustering. Production implementations use tombstones or rehashing to preserve probe sequences.

---

### 7.4 Resizing and Load Factor

To maintain O(1) average operations, hash tables resize (rehash) when the load factor (size/capacity) crosses a threshold (e.g., 0.7). Resizing allocates a bigger bucket array and reinserts all entries.


## 8. Hash Functions and Key Requirements

* Good hash functions distribute keys uniformly across buckets.
* In Python, `hash()` is used for built‑ins; custom objects should implement `__hash__` and `__eq__`.
* Keys must be **immutable** for stable hashing (e.g., `int`, `str`, `tuple`). Mutable types like `list` are unhashable.

Example custom key:

```python
class Point:
    def __init__(self, x, y):
        self.x, self.y = x, y
    def __eq__(self, other):
        return isinstance(other, Point) and self.x==other.x and self.y==other.y
    def __hash__(self):
        return hash((self.x, self.y))
```


## 9. Time and Space Complexity

| Operation       | Average Case | Worst Case |
| --------------- | ------------ | ---------- |
| Lookup (get)    | O(1)         | O(n)       |
| Insert (put)    | O(1)         | O(n)       |
| Delete (remove) | O(1)         | O(n)       |
| Space usage     | O(n)         | O(n)       |

*Average O(1) assumes a good hash function and controlled load factor.*


## 10. Real-World Applications

* Dictionary / Map implementations in programming languages.
* Caching (e.g., LRU caches combine hash table + linked list).
* Database indexing and hash-based joins.
* Symbol tables in compilers and interpreters.
* Sets (uniqueness checks) and membership tests.


## 11. Comparison with Other Data Structures

* **Hash Table vs Array:** Hash tables provide faster lookups for keyed access; arrays provide ordered storage and index access.
* **Hash Table vs Balanced Tree:** Trees (AVL, RB) provide ordered traversal and guaranteed O(log n) worst-case; hash tables give average O(1) but no order.
* **Hash Table vs Trie:** Tries provide prefix-based lookup (strings) with different memory/time trade-offs.


## 12. Conclusion

Hash tables are a cornerstone of efficient algorithms and software systems. Understanding hashing, collision resolution, load factor, and resizing is essential to use and implement hash tables robustly. Python's `dict` provides a production-ready, highly optimized hash table—use it whenever you need fast key-value storage.
