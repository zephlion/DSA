# Pareto Problem Set

### Array & Hashing  
<details>
<summary>Problem 1 - Contains Duplicate</summary>

### 🔗 [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

#### 📝 Problem

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and `false` if every element is distinct.

---

#### 💡 Approach / Intuition

* Use a **Set** which automatically stores only unique values.
* If the size of the `Set` is **smaller** than the length of the array, that means duplicates exist.

---

#### 💻 Code

```js
var containsDuplicate = nums => new Set(nums).size !== nums.length;
```

---

#### ⏱️ Time Complexity

* Creating a `Set`: **O(n)**
* Checking `.size`: **O(1)**
* Comparison: **O(1)**
  **➡ Overall: O(n)**

#### 🗂️ Space Complexity

* In the worst case, all `n` elements are unique → stored in the `Set`.
  **➡ O(n)**

---

#### 🧠 Notes

* This is the most concise solution.
* Alternative: Use a **HashMap** or manual iteration to check duplicates.
* Good to compare against the **brute force O(n²)** approach to appreciate efficiency.

</details>


<details>
<summary>Problem 2 - Valid Anagram</summary>

### 🔗 [Valid Anagram](https://leetcode.com/problems/valid-anagram/)

#### 📝 Problem

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise. An **anagram** is a word or phrase formed by rearranging the letters of another.

---

#### 💡 Approach / Intuition

* If the strings have different lengths, they cannot be anagrams.
* Use an array of size **26** (for each lowercase English letter).
* Increment counts for characters in `s`, decrement counts for characters in `t`.
* At the end, if all counts are zero, then the two strings are anagrams.

---

#### 💻 Code

```js
var isAnagram = function(s, t) {
    if (s.length !== t.length) return false;
    
    const alphabet = new Array(26).fill(0);

    for (let index = 0; index < s.length; index++) {
        alphabet[s.charCodeAt(index) - 'a'.charCodeAt(0)]++;
        alphabet[t.charCodeAt(index) - 'a'.charCodeAt(0)]--;
    }

    return alphabet.every(letter => letter === 0);
};
```

---

#### ⏱️ Time Complexity

* Comparing lengths: **O(1)**
* Iterating over both strings: **O(n)**
* Checking with `every`: **O(26)** → constant
  **➡ Overall: O(n)**

#### 🗂️ Space Complexity

* Fixed array of size 26 regardless of input size.
  **➡ O(1)**

---

#### 🧠 Notes

* This solution is efficient and avoids sorting (which would be **O(n log n)**).
* Works only for lowercase English letters. If input includes Unicode/uppercase, need a `Map` or `Object` for flexibility.

</details>


<details>
<summary>Problem 3 - Two Sum</summary>

### 🔗 [Two Sum](https://leetcode.com/problems/two-sum/)

#### 📝 Problem

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`. You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

---

#### 💡 Approach / Intuition

* Use a **hash map** to store numbers we’ve already seen along with their indices.
* For each number `current`, check if `target - current` already exists in the map.
* If it does, return the indices. If not, store the current number and its index in the map.

---

#### 💻 Code

```js
var twoSum = function(nums, target) {
    const object = new Object();

    for (let index = 0; index < nums.length; index++) {
        const current = nums[index];
        if (target - current in object) {
            return [index, object[target - current]];
        }
        object[current] = index;
    }
};
```

---

#### ⏱️ Time Complexity

* Iterating over `nums`: **O(n)**
* Hash lookup (`target - current in object`): **O(1)**
  **➡ Overall: O(n)**

#### 🗂️ Space Complexity

* In the worst case, store all `n` elements in the hash map.
  **➡ O(n)**

---

#### 🧠 Notes

* This is the **optimal solution** using hashing.
* A brute-force solution would check all pairs (nested loops), resulting in **O(n²)** time.
* Be mindful of returning the indices in the **correct order**.

</details>


<details>
<summary>Problem 4 - Group Anagrams</summary>

### 🔗 [Group Anagrams](https://leetcode.com/problems/group-anagrams/)

#### 📝 Problem

Given an array of strings `strs`, group the anagrams together. You can return the answer in **any order**.

---

#### 💡 Approach / Intuition

* Anagrams have the same characters when sorted.
* Sort each string alphabetically → use it as a key in a hash map.
* Group strings with the same sorted key together.
* Return all grouped values from the hash map.

---

#### 💻 Code

```js
var groupAnagrams = function(strs) {
    const object = new Object();
    for (let i = 0; i < strs.length; i++) {
        const sorted = strs[i].split('').sort().join('');
        if (sorted in object) {
            object[sorted].push(strs[i]);
        } else {
            object[sorted] = [strs[i]];
        }
    }
    return Object.values(object);
};
```

---

#### ⏱️ Time Complexity

* Splitting each string: **O(k)**
* Sorting each string: **O(k log k)**
* Processing all strings: **O(n)**
  **➡ Overall: O(n · k log k)**

#### 🗂️ Space Complexity

* Hash map stores up to `n` strings with average length `k`.
  **➡ O(n · k)**

---

#### 🧠 Notes

* Sorting-based approach is simple and effective.
* Alternative: use **character frequency counts** as keys for an **O(n · k)** solution.
* Useful problem for practicing **hash maps + string manipulation**.

</details>


<details>
<summary>Problem 5 - Top K Frequent Elements</summary>

### 🔗 [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

#### 📝 Problem

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in **any order**.

---

#### 💡 Approach / Intuition

* Count the frequency of each element using a hash map.
* Sort the elements by their frequency in descending order.
* Extract the first `k` elements from the sorted result.

---

#### 💻 Code

```js
var topKFrequent = function(nums, k) {
    const object = new Object();
    const array = new Array();
    
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] in object) {
            object[nums[i]] += 1;
        } else {
            object[nums[i]] = 1;
        }
    }
    
    const sorted = Object.entries(object).sort((a, b) => b[1] - a[1]);
    
    for (let i = 0; i < k; i++) {
        array.push(Number(sorted[i][0]));
    }
    
    return array;
};
```

---

#### ⏱️ Time Complexity

* Counting frequencies: **O(n)**
* Sorting frequencies: **O(n log n)**
  **➡ Overall: O(n log n)**

#### 🗂️ Space Complexity

* Hash map to store frequencies: **O(n)**
* Result array: up to **O(k)**
  **➡ O(n)**

---

#### 🧠 Notes

* This approach is straightforward but involves sorting.
* Optimized approach: use a **bucket sort** or **heap/priority queue** to achieve **O(n)** time.
* Useful problem for practicing **frequency counting + sorting/heap techniques**.

</details>


<details>
<summary>Problem 6 - Valid Sudoku</summary>

### 🔗 [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)

#### 📝 Problem

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes must contain the digits `1-9` without repetition.

---

#### 💡 Approach / Intuition

* Use **three sets of hash sets**:

  * `rows[i]` to track digits in each row.
  * `cols[j]` to track digits in each column.
  * `boxes[boxIndex]` to track digits in each 3x3 sub-grid.
* For each cell:

  * Skip if it's `.`.
  * Calculate its `boxIndex = Math.floor(i / 3) * 3 + Math.floor(j / 3)`.
  * If the digit is already in the row, column, or box → return `false`.
  * Otherwise, add it to all three.
* If no conflicts, return `true`.

---

#### 💻 Code

```js
var isValidSudoku = function(board) {
    const rows = new Array(9).fill(null).map(() => new Set());
    const cols = new Array(9).fill(null).map(() => new Set());
    const boxes = new Array(9).fill(null).map(() => new Set());
    
    for (let i = 0; i < 9; i++) {
        for (let j = 0; j < 9; j++) {
            const num = board[i][j];
            if (num !== '.') {
                const boxIndex = Math.floor(i / 3) * 3 + Math.floor(j / 3);
                if (rows[i].has(num) || cols[j].has(num) || boxes[boxIndex].has(num)) {
                    return false;
                }
                rows[i].add(num);
                cols[j].add(num);
                boxes[boxIndex].add(num);
            }
        }
    }
    return true;
};
```

---

#### ⏱️ Time Complexity

* Iterating through a `9x9` board: **O(1)** (constant size).
* Each set operation: **O(1)**.
* **➡ Overall: O(1)**

#### 🗂️ Space Complexity

* Three arrays of 9 sets each, with at most 9 elements in each set.
  **➡ O(1)** (constant space).

---

#### 🧠 Notes

* Since the board size is fixed (`9x9`), time and space complexity are constant.
* Important edge case: ensure **sub-box indexing** is correct.
* This solution can be extended for generalized Sudoku boards by scaling the iteration and box calculation.

</details>


<details>
<summary>Problem 7 - Product of Array Except Self</summary>

### 🔗 [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self)

#### 📝 Problem

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

The algorithm should run in **O(n)** time and without using division.

---

#### 💡 Approach / Intuition

* Use **two passes** to calculate prefix and suffix products:

  * **Left pass**: Compute the running product of all numbers to the left of `i`.
  * **Right pass**: Compute the running product of all numbers to the right of `i`.
* Multiply left and right products for each index.
* Store results in the same `answer` array to maintain **O(1) extra space**.

---

#### 💻 Code

```js
var productExceptSelf = function(nums) {
    const answer = new Array(nums.length).fill(1);

    let left_product = 1;
    for (let i = 0; i < nums.length; i++) {
        answer[i] *= left_product;
        left_product *= nums[i];
    }

    let right_product = 1;
    for (let i = nums.length - 1; i >= 0; i--) {
        answer[i] *= right_product;
        right_product *= nums[i];
    }

    return answer;
};
```

---

#### ⏱️ Time Complexity

* Two passes through `nums` → **O(n)**.
* Constant work inside each loop.
* **➡ Overall: O(n)**

#### 🗂️ Space Complexity

* Output array excluded (per problem statement).
* Only `left_product` and `right_product` variables used.
* **➡ O(1)** extra space.

---

#### 🧠 Notes

* Division is not allowed, so prefix/suffix method is optimal.
* The solution handles **zero values** correctly:

  * If there are two or more zeros, all results are zero.
  * If exactly one zero exists, only that index will have the product of non-zero elements, others are zero.

</details>


<details>
<summary>Problem 8 - Longest Consecutive Sequence</summary>

### 🔗 [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

#### 📝 Problem

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

The algorithm should run in **O(n)** time.

---

#### 💡 Approach / Intuition

* Use a **HashSet** to store all unique numbers in `nums`.
* For each number, check if it is the **start of a sequence** (i.e., `num - 1` is not in the set).
* If it is the start, extend the sequence by checking consecutive numbers (`num + 1`, `num + 2`, …).
* Track the maximum length seen.

---

#### 💻 Code

```js
var longestConsecutive = function(nums) {
    const set = new Set(nums);
    let count = 0;

    for (let el of set) {
        if (!set.has(el - 1)) {
            let len = 1;
            while (set.has(el + len)) {
                len++;
            }
            count = Math.max(count, len);
        }
    }

    return count;
};
```

---

#### ⏱️ Time Complexity

* Creating the set → **O(n)**.
* Iterating over set elements → **O(n)**.
* Inner `while` loop runs only across sequences once → amortized **O(n)**.
* **➡ Overall: O(n)**

#### 🗂️ Space Complexity

* HashSet stores all unique elements → **O(n)**.

---

#### 🧠 Notes

* Works even if numbers are unsorted.
* Efficient since each number is checked at most twice.
* Skips redundant checks by only starting sequences at their smallest element.

</details>


### Two Pointers
<details>
<summary>Problem 1</summary>
  <div>
    
  ### [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
  - Solution:
    ```js
    var isPalindrome = function(s) {
        let left = 0, right = s.length - 1;
        
        while (left < right) {
            if (!/[a-zA-Z0-9]/.test(s[left])) left++;
            else if (!/[a-zA-Z0-9]/.test(s[right])) right--;
            else if (s[left].toLowerCase() !== s[right].toLowerCase()) return false;
            else {
                left++;
                right--;
            }
        }
        return true;
    };
    ```
    - Time Complexity - $O(n)$
      - We iterate through the string once, where `n` is the length of the string. Each operation (skipping or comparing characters) is constant time.
  
    - Space Complexity - $O(1)$
      - The solution uses constant extra space, with only a few variables (`left`, `right`) for traversal.
  </div>
</details>

<details>
<summary>Problem 2</summary>
  <div>
    
  ### [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
  - Solution:
    ```js
    var twoSum = function(numbers, target) {
        let left = 0, right = numbers.length - 1;
        
        while (left < right) {
            const sum = numbers[left] + numbers[right];
            
            if (sum === target) {
                return [left + 1, right + 1];
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return [];
    };
    ```
    - Time Complexity - $O(n)$
      - We iterate through the array once with two pointers, so the time complexity is linear in terms of the number of elements (`n`).
  
    - Space Complexity - $O(1)$
      - The solution uses a `constant amount of extra space`, with only a few variables for the pointers and the sum.
  </div>
</details>

<details>
<summary>Problem 3</summary>
  <div>
    
  ### [3Sum](https://leetcode.com/problems/3sum/)
  - Solution:
    ```js
     var threeSum = function (nums) {
        const result = new Array();
        const sorted = nums.sort((a, b) => a - b);
    
        for (let i = 0; i < sorted.length; i++) {
            if (sorted[i] > 0) break;
    
            if (i > 0 && sorted[i] === sorted[i - 1]) continue;
    
            let j = i + 1;
            let k = sorted.length - 1;
    
            while (j < k) {
                let total = sorted[i] + sorted[j] + sorted[k];
    
                if (total > 0) {
                    k--;
                } else if (total < 0) {
                    j++;
                } else {
                    result.push([sorted[i], sorted[j], sorted[k]]);
    
                    while (j < k && sorted[j] === sorted[j + 1]) {
                        j++;
                    }
    
                    while (j < k && sorted[k] === sorted[k - 1]) {
                        k--;
                    }
    
                    j++;
                    k--;
                }
            }
        }
    
        return result;
    };
    ```
    - Time Complexity -  $O(n^2)$
      - We sort the array in $O(n \log n)$, and for each element, we perform a two-pointer search which takes $O(n)$, resulting in a total complexity of $O(n^2)$.
  
    - Space Complexity - $O(1)$
      - The solution uses constant extra space (excluding the output array). The sorting and two-pointer techniques only use a fixed amount of additional space.
  </div>
</details>

<details>
<summary>Problem 4</summary>
  <div>
    
  ### [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
  - Solution:
    ```js
    var maxArea = function(height) {
        let area = 0
        let left = 0
        let right = height.length - 1
        while(left < right){
            area = Math.max(area, (right - left) * Math.min(height[left], height[right]))
            if(height[left] < height[right]){
                left++
            } else {
                right--
            }
        }
        return area
    };
    ```
    - Time Complexity - $O(n)$
      - We iterate through the array once with two pointers (`left` and `right`), so the time complexity is linear in terms of the number of elements (`n`).
  
    - Space Complexity - $O(1)$
      - The solution uses `constant extra space`, with only a few variables to track the pointers and the maximum area.
  </div>
</details>

### Sliding Window
<details>
<summary>Problem 1</summary>
  <div>
    
  ### [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock)
  - Solution:
    ```js
   
    ```
    - Time Complexity - $O(n)$
      - 
  
    - Space Complexity - $O(1)$
      - 
  </div>
</details>
