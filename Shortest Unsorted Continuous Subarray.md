<h1 align="center">📏 Shortest Unsorted Continuous Subarray</h1>

<p align="center">
  <a href="https://leetcode.com/problems/shortest-unsorted-continuous-subarray/">
    <img src="https://img.shields.io/badge/LeetCode-Shortest%20Unsorted%20Continuous%20Subarray-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Array%2C%20Sorting%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We want the **shortest subarray** which, if sorted, makes the entire array sorted.  

Naive way: Sort the array and compare with the original to find mismatched boundaries.  
Optimized way:  
- Scan from **left** to find the first element that is out of order.  
- Scan from **right** to find the last element that is out of order.  
- Expand boundaries outward if there are smaller/larger values within that subarray.

## 💡 Approach

1. **Find initial boundaries**:  
   - Move `left` until elements are non-decreasing.  
   - Move `right` until elements are non-increasing.  
   - If array is already sorted → return `0`.  
2. **Find min & max** in the unsorted segment.  
3. **Expand boundaries**:  
   - Move `left` backward until all elements on the left are ≤ `min`.  
   - Move `right` forward until all elements on the right are ≥ `max`.  
4. Return `right - left + 1`.

## ❗ Edge Cases

- Already sorted array → return 0.  
- All elements same → return 0.  
- Subarray extends to edges → handle bounds carefully.  

## 🔍 Example

```
Input: nums = [2,6,4,8,10,9,15]
Output: 5
Explanation: Sorting [6,4,8,10,9] makes the array sorted.
```

## 🧾 Code

```
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        n = len(nums)
        left, right = 0, n - 1

        # Find initial left boundary
        while left < n - 1 and nums[left] <= nums[left + 1]:
            left += 1
        if left == n - 1:  # Already sorted
            return 0

        # Find initial right boundary
        while right > 0 and nums[right] >= nums[right - 1]:
            right -= 1

        # Find min and max within the unsorted region
        sub_min = min(nums[left:right + 1])
        sub_max = max(nums[left:right + 1])

        # Expand left
        while left > 0 and nums[left - 1] > sub_min:
            left -= 1

        # Expand right
        while right < n - 1 and nums[right + 1] < sub_max:
            right += 1

        return right - left + 1
```
## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Identify initial unsorted segment, then expand based on min & max.
- 🚀 O(n) solution without sorting.
- 🧠 Pattern: "Find minimal unsorted segment + adjust boundaries."
