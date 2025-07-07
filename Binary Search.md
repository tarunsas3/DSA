<h1 align="center">✅ Binary Search</h1>

<p align="center">
  <a href="https://leetcode.com/problems/binary-search/">
    <img src="https://img.shields.io/badge/LeetCode-Binary%20Search-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Binary%20Search%2C%20Array-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We're given a **sorted array** and a `target`.  
Since the array is sorted, we can eliminate half the search space at every step — a perfect use case for **binary search**.


## 💡 Approach

1. Initialize two pointers:
   - `left = 0`, `right = len(nums) - 1`
2. While `left <= right`:
   - Compute `mid = (left + right) // 2`
   - If `nums[mid] == target`, return `mid`
   - If `nums[mid] < target`, discard left half → `left = mid + 1`
   - Else discard right half → `right = mid - 1`
3. If not found, return `-1`


## ❗ Edge Cases

- Empty array → return `-1`
- Target at start or end
- Duplicates don’t affect the logic since we only care about **one occurrence**


## 🔍 Example

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
```

Explanation: 9 exists at index 4

## 🧾 Code

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1

        return -1
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(log n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Classic divide & conquer technique
- ✅ Efficient for sorted arrays
- 💡 Forms the foundation for advanced problems like:
  - First/Last Occurrence
  - Search in Rotated Sorted Array
  - Peak Element, Kth Smallest Element
