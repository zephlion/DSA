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
