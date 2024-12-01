# Pareto Problem Set

### Array & Hashing  
<details>
<summary>Problem 1</summary>
  <div>
    
  ### [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
  - Solution:
    ```js
    var containsDuplicate = nums => new Set(nums).size !== nums.length;
    ```
    - Time Complexity - $O(n)$
      - Creating a `Set` - $O(n)$
      - `.size` property - $O(1)$
      - Comparison `!==` - $O(1)$
  
    - Space Complexity - $O(n)$
      - Worst case scenario, store all elements in a `Set` - $O(n)$
  </div>
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
