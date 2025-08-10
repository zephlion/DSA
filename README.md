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
<summary>Problem 2</summary>
  <div>
    
  ### [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
  - Solution:
    ```js
    var isAnagram = function(s, t) {
        if (s.length !== t.length) return false
        
        const alphabet = new Array(26).fill(0)
    
        for(let index = 0; index < s.length; index++){
            alphabet[s.charCodeAt(index) - 'a'.charCodeAt(0)]++
            alphabet[t.charCodeAt(index) - 'a'.charCodeAt(0)]--
        }
    
        return alphabet.every(letter => letter === 0)
    };
    ```
    - Time Complexity: $O(n)$
      - Comparing the lengths of `s` and `t` - $O(1)$
      - Iterating over the string `s` and `t` - $O(n)$, where $n$ is the length of the strings.
      - The `every` method - $O(26)$, which is a constant operation.
    - Space Complexity: $O(1)$
      - The `alphabet` array has a fixed size of 26, regardless of the input size.
  </div>
</details>

<details>
<summary>Problem 3</summary>
  <div>
    
  ### [Two Sum](https://leetcode.com/problems/two-sum/)
  - Solution:
    ```js
    var twoSum = function(nums, target) {
    const object = new Object()

    for(let index = 0; index < nums.length; index++){
        const current = nums[index]
        if(target - current in object){
            return [index, object[target - current]]
        }
        object[current] = index
      }
    };
    ```
    - Time Complexity: $O(n)$
      - Iterating over the `nums` array - $O(n)$, where $n$ is the length of the array.
      - Checking for the existence of `target - current` in the `object` (hash lookup) - $O(1)$.
    - Space Complexity: $O(n)$
      - Storing up to `n` elements in the object (hash table) in the worst case.
  </div>
</details>

<details>
<summary>Problem 4</summary>
  <div>
    
  ### [Group Anagrams](https://leetcode.com/problems/group-anagrams/)
  - Solution:
    ```js
    var groupAnagrams = function(strs) {
        const object = new Object()
        for(let i = 0; i < strs.length; i++){
            const sorted = strs[i].split('').sort().join('')
            if(sorted in object){
                object[sorted].push(strs[i])
            } else {
                object[sorted] = [strs[i]]
            }
        }
        return Object.values(object)
    };
    ```
    - Time Complexity: $O(n \cdot k \log k)$
      - Splitting each string into an array - $O(k)$, where `k` is the average length of the strings.
      - Sorting each string's characters - $O(k \log k)$.
      - Iterating through all strings in `strs` - $O(n)$, where `n` is the number of strings.
    - Space Complexity: $O(n \cdot k)$
      - Storing up to `n` strings in the `object`, with each string having a length of at most `k`.
  </div>
</details>

<details>
<summary>Problem 5</summary>
  <div>
    
  ### [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
  - Solution:
    ```js
    var topKFrequent = function(nums, k) {
        const object = new Object()
        const array = new Array()
        
        for (let i = 0; i < nums.length; i++) {
            if (nums[i] in object) {
                object[nums[i]] += 1
            } else {
                object[nums[i]] = 1
            }
        }
        
        const sorted = Object.entries(object).sort((a, b) => b[1] - a[1])
        
        for (let i = 0; i < k; i++) {
            array.push(Number(sorted[i][0]))
        }
        
        return array
    };
    ```
    - Time Complexity: $O(n \log n)$
      - Counting frequencies - $O(n)$, where `n` is the length of the array.
      - Sorting the entries of the object - $O(n \log n)$.
    - Space Complexity: $O(n)$
      - The space required for the `object`, `hash map` and the `array` to store the result.
  </div>
</details>

<details>
<summary>Problem 6</summary>
  <div>
    
  ### [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)
  - Solution:
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
                    
                    if (rows[i].has(num) || cols[j].has(num) || boxes[boxIndex].has(num)) return false;
    
                    rows[i].add(num);
                    cols[j].add(num);
                    boxes[boxIndex].add(num);
                }
            }
        }
        return true;
    };
    ```
    - Time Complexity: $O(1)$
      - We iterate through all cells in a `fixed-size 9x9 grid` (constant size).
      - For each cell, checking or adding a value to a `Set` takes constant time, $O(1)$.
    - Space Complexity: $O(1)$
      - We use `3 sets` for `rows`, `columns`, and `boxes`. Each set `holds at most 9 unique elements`, meaning the space used by these sets is `constant`.
  </div>
</details>

<details>
<summary>Problem 7</summary>
  <div>
    
  ### [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self)
  - Solution:
    ```js
    var productExceptSelf = function(nums) {
        const answer = new Array(nums.length).fill(1)
    
        let left_product = 1
        for(let i = 0; i < nums.length; i++){
            answer[i] *= left_product;
            left_product *= nums[i]
        }
    
        let right_product = 1
        for(let i = nums.length - 1; i >= 0; i--){
            answer[i] *= right_product
            right_product *= nums[i]
        }
        return answer
    };
    ```
    - Time Complexity: $O(n)$
      - We make two passes through the array (`n` iterations each) to calculate the left and right products.
    - Space Complexity: $O(1)$
      - We only use a few extra variables (`left_product`, `right_product`), which take constant space.
  </div>
</details>

<details>
<summary>Problem 8</summary>
  <div>
    
  ### [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
  - Solution:
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
    - Time Complexity: $O(n)$
      - Creating the `Set` - $O(n)$, where `n` is the number of elements in `nums`.
      - `Iterating over the elements` of the `set` - $O(n)$.
      - The inner `while loop` executes at most once for each consecutive sequence of numbers, so the total time is still $O(n)$.
    - Space Complexity: $O(n)$
      - The `Set` stores all unique elements in `nums`, requiring $O(n)$ space in the worst case.
  </div>
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
