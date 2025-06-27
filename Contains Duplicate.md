<h1 align="center">✅ Contains Duplicate</h1>

<p align="center">
  <a href="https://leetcode.com/problems/contains-duplicate/">
    <img src="https://img.shields.io/badge/LeetCode-Contains%20Duplicate-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Array%2C%20Hashing%2C%20Set-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We use a **set** to keep track of elements we've already seen.  
If we encounter the same number again while traversing the array, it means there's a duplicate.


## 💡 Approach

1. Initialize an empty `set` called `seen`.
2. Loop through each number in `nums`:
   - If it's already in `seen`, return `True`.
   - Otherwise, add it to the set.
3. If the loop ends without finding a duplicate, return `False`.


## ❗ Edge Cases

- `[]` → return `False` (empty array, no duplicates)  
- `[1]` → return `False` (only one element)  
- Large array with all unique values → should still be handled efficiently


## 🔍 Example

```python
Input: nums = [1, 2, 3, 1]
Output: True
Explanation: 1 is repeated.
```

### 🧾 Code
```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

### 📌 Summary

- ✅ Set allows O(1) average-case lookups and inserts.
- ✅ Early exit improves performance.
- 💡 Very common pattern in duplicate-checking problems.

