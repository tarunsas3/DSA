<h1 align="center">➕ 3Sum Closest</h1>

<p align="center">
  <a href="https://leetcode.com/problems/3sum-closest/">
    <img src="https://img.shields.io/badge/LeetCode-3Sum%20Closest-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Two%20Pointers%2C%20Sorting%2C%20Array-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We want the **sum of 3 numbers closest to a target**.  
This is similar to **3Sum**:
- Sort the array.
- Fix one element, then use two pointers (`left`, `right`) to find the best pair.
- Track the **closest sum** to the target while iterating.

Sorting ensures we can adjust pointers efficiently based on whether the sum is too big or too small.

## 💡 Approach

1. Sort `nums`.  
2. Initialize `closest_sum` as a very large value.  
3. For each index `i` from `0` to `n-3`:
   - Set `left = i + 1`, `right = n - 1`.  
   - While `left < right`:
     - Compute `curr_sum = nums[i] + nums[left] + nums[right]`.
     - If `abs(curr_sum - target) < abs(closest_sum - target)`, update `closest_sum`.
     - If `curr_sum < target`: move `left` forward.
     - If `curr_sum > target`: move `right` backward.
     - If exactly equal to `target`: return `curr_sum` (best possible).  
4. Return `closest_sum`.

## ❗ Edge Cases

- Length < 3 → not valid (per constraints).  
- Duplicates → still works, since we don’t skip duplicates here (we need closest sum, not unique triplets).  

## 🔍 Example

```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The closest sum is 2 (-1 + 2 + 1).
```

## 🧾 Code

```
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        closest_sum = float('inf')

        for i in range(len(nums) - 2):
            left, right = i + 1, len(nums) - 1

            while left < right:
                curr_sum = nums[i] + nums[left] + nums[right]

                if abs(curr_sum - target) < abs(closest_sum - target):
                    closest_sum = curr_sum

                if curr_sum < target:
                    left += 1
                elif curr_sum > target:
                    right -= 1
                else:
                    return curr_sum  # exact match

        return closest_sum
```
## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n²)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Sort + two-pointer gives an efficient O(n²) solution.
- 🔄 Adjust pointers based on sum relative to target.
- 🚀 Early return when exact match is found.
- 🧠 Classic 3Sum pattern adapted for "closest sum".
