<h1 align="center">💎 Maximum Erasure Value</h1>

<p align="center">
  <a href="https://leetcode.com/problems/maximum-erasure-value/">
    <img src="https://img.shields.io/badge/LeetCode-Maximum%20Erasure%20Value-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20HashSet%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We want the **maximum sum of a subarray with all unique elements**.  
This is a **sliding window** problem:
- Use a set to ensure all elements in the window are unique.
- Expand the window with `right` and add to the current sum.
- If a duplicate is found, **shrink from `left`** until it’s unique again.
- Track the maximum sum seen.

## 💡 Approach

1. Initialize `left = 0`, `curr_sum = 0`, `max_sum = 0`, and an empty `seen` set.  
2. Iterate `right` over `nums`:
   - While `nums[right]` is in `seen`, remove `nums[left]` from set and subtract from `curr_sum`, increment `left`.
   - Add `nums[right]` to `seen` and update `curr_sum`.
   - Update `max_sum = max(max_sum, curr_sum)`.  
3. Return `max_sum`.

## ❗ Edge Cases

- All numbers unique → sum of entire array.  
- All numbers same → max single element.  
- Empty array → return 0.  

## 🔍 Example

```
Input: nums = [4,2,4,5,6]
Output: 17
Explanation: The subarray [2,4,5,6] has the maximum sum 17.
```

## 🧾 Code

```
class Solution:
    def maximumUniqueSubarray(self, nums: List[int]) -> int:
        seen = set()
        left = 0
        curr_sum = 0
        max_sum = 0

        for right in range(len(nums)):
            while nums[right] in seen:
                seen.remove(nums[left])
                curr_sum -= nums[left]
                left += 1
            seen.add(nums[right])
            curr_sum += nums[right]
            max_sum = max(max_sum, curr_sum)

        return max_sum
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

## 📌 Summary

- ✅ Expand–shrink sliding window ensures unique elements.
- 💡 Maintain running sum dynamically (no recomputation).
- 🚀 O(n) optimal solution with constant-time updates.
- 🧠 Pattern: "max sum of subarray with uniqueness constraint."
