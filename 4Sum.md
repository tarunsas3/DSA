<h1 align="center">➕ 4Sum</h1>

<p align="center">
  <a href="https://leetcode.com/problems/4sum/">
    <img src="https://img.shields.io/badge/LeetCode-4Sum-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Two%20Pointers%2C%20Sorting%2C%20Array-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

This is an extension of **3Sum**:
- Instead of 3 numbers, we need 4 whose sum equals the target.
- Sort the array for **two-pointer optimization**.
- Fix two indices (`i` and `j`), then use two pointers (`left`, `right`) for the remaining two.
- Carefully skip duplicates to avoid repeating quadruplets.

## 💡 Approach

1. Sort `nums`.  
2. Iterate `i` from `0` to `n-4`:
   - Skip duplicates for `i`.  
3. Iterate `j` from `i+1` to `n-3`:
   - Skip duplicates for `j`.  
4. Use two pointers:
   - `left = j + 1`, `right = n - 1`.  
   - While `left < right`:
     - Compute `curr_sum = nums[i] + nums[j] + nums[left] + nums[right]`.  
     - If `curr_sum == target`: store the quadruplet, skip duplicates for `left` and `right`.  
     - If `curr_sum < target`: move `left` forward.  
     - If `curr_sum > target`: move `right` backward.  
5. Return the list of unique quadruplets.

## ❗ Edge Cases

- Fewer than 4 numbers → return [].  
- All duplicates → return one quadruplet if sum matches.  
- Large numbers → watch for integer overflow in some languages (Python handles this natively).  

## 🔍 Example

```python
Input: nums = [1,0,-1,0,-2,2], target = 0
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

## 🧾 Code

```
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        res = []
        n = len(nums)

        for i in range(n - 3):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            for j in range(i + 1, n - 2):
                if j > i + 1 and nums[j] == nums[j - 1]:
                    continue
                left, right = j + 1, n - 1
                while left < right:
                    curr_sum = nums[i] + nums[j] + nums[left] + nums[right]
                    if curr_sum == target:
                        res.append([nums[i], nums[j], nums[left], nums[right]])
                        left += 1
                        right -= 1
                        while left < right and nums[left] == nums[left - 1]:
                            left += 1
                        while left < right and nums[right] == nums[right + 1]:
                            right -= 1
                    elif curr_sum < target:
                        left += 1
                    else:
                        right -= 1
        return res
```
## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n³)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Sort + two-pointer reduces complexity from brute force O(n⁴) to O(n³).
- 🔄 Skip duplicates for uniqueness.
- 🚀 Works efficiently for moderate-sized arrays.
- 🧠 Pattern: Generalization of 3Sum for 4 elements.
