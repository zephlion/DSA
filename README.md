# Pareto Problem Set
### [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
- Solution:
  ```js
  var containsDuplicate = nums => new Set(nums).size !== nums.length;
  ```
  - Time Complexity - $`O(n)`$
    - Creating a `Set` - $`O(n)`$
    - `.size` property - $`O(1)`$
    - Comparison `!==` - $`O(1)`$

  - Space Complexity - $`O(n)`$
    - Worst case scenario, store all elements in a `Set` - $`O(n)`$
 
### [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
- Solution:
  - Time Complexity:
  - Space Complexity:
