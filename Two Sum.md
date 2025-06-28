<h1 align="center">✅ Two Sum</h1>

<p align="center">
  <a href="https://leetcode.com/problems/two-sum/">
    <img src="https://img.shields.io/badge/LeetCode-Two%20Sum-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Array%2C%20Hashing-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We want to find two numbers in the array that add up to the given `target`.  
While iterating through the array, we can check if the **complement** of the current number (i.e., `target - current`) has already been seen.

If so, we’ve found our answer.  
If not, we store the current number’s value and index for future lookups.


## 💡 Approach

1. Initialize an empty hash map `seen` to store value → index mappings.
2. For each index `i` and value `v` in `nums`:
   - Compute the complement as `target - v`.
   - If `complement` is already in `seen`, return `[seen[complement], i]`.
   - Else, store `v` with its index in the map.
3. The solution is guaranteed to exist, so return is always hit.


## ❗ Edge Cases

- Duplicate numbers like `[5, 5]` with `target = 10` → handled correctly  
- Negative numbers or large ranges → still O(n)  
- Solution always returns the pair with the **smaller index first**


## 🔍 Example

```
Input: nums = [3, 4, 5, 6], target = 7
Output: [0, 1]
Explanation: nums[0] + nums[1] == 7
```

## 🧾 Code

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen = {}
        for i, v in enumerate(nums):
            comp = target - v
            if comp in seen:
                return [seen[comp], i]
            seen[v] = i
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

📌 Summary

- ✅ Efficient single-pass solution using a hash map
- ✅ Handles negative and duplicate values
- ✅ Clean, readable, and industry-style Python
