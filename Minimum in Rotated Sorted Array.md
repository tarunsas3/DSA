<h1 align="center">✅ Find Minimum in Rotated Sorted Array</h1>

<p align="center">
  <a href="https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/">
    <img src="https://img.shields.io/badge/LeetCode-Find%20Minimum%20in%20Rotated%20Sorted%20Array-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Binary%20Search%2C%20Array-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We’re given a **rotated sorted array** with **no duplicates**.  
We need to find the **minimum element**, which is the **inflection point** where the array was rotated.

Binary Search is ideal because:
- One half of the array is always sorted.
- The minimum lies in the **unsorted half**.


## 💡 Approach

1. Initialize pointers: `left = 0`, `right = len(nums) - 1`
2. Track `res = nums[0]` as the current minimum
3. While `left <= right`:
   - If `nums[left] < nums[right]`, current subarray is sorted → update `res` and break
   - Compute `mid = (left + right) // 2`
   - Update `res = min(res, nums[mid])`
   - If `nums[mid] >= nums[left]`:
     - Left half is sorted → move right → `left = mid + 1`
   - Else:
     - Right half is unsorted (minimum must be here) → `right = mid - 1`
4. Return `res`


## ❗ Edge Cases

- Not rotated (already sorted) → return `nums[0]`
- Only one element → return `nums[0]`
- Two elements → minimum is the smaller of the two


## 🔍 Example

```
Input: nums = [4,5,6,7,0,1,2]
Output: 0
```

Explanation: 0 is the minimum element in the rotated array

## 🧾 Code

```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1
        res = nums[0]

        while left <= right:
            if nums[left] < nums[right]:
                res = min(res, nums[left])
                break

            mid = (left + right) // 2
            res = min(res, nums[mid])

            if nums[mid] >= nums[left]:
                left = mid + 1
            else:
                right = mid - 1

        return res
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(log n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Efficient search using binary search logic
- ✅ Always look toward the unsorted half of the array
- 💡 Commonly used with rotated arrays and inflection point problems
- 🔁 Related to:
  - Search in Rotated Sorted Array
  - Minimum in Rotated Sorted Array II (with duplicates)
