<h1 align="center">✅ Search in Rotated Sorted Array</h1>

<p align="center">
  <a href="https://leetcode.com/problems/search-in-rotated-sorted-array/">
    <img src="https://img.shields.io/badge/LeetCode-Search%20in%20Rotated%20Sorted%20Array-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Binary%20Search%2C%20Rotated%20Array-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

This is a **twist on binary search** where the array is sorted but **rotated at some pivot**.

We use the fact that **one half of the array is always sorted**:
- If the target is within that sorted half, we search there.
- Otherwise, we search the other half.


## 💡 Approach

1. Initialize `low` and `high` pointers at the start and end of the array.
2. In each iteration:
   - Compute the middle index.
   - If `nums[mid] == target`, return the index.
   - Determine which half is sorted:
     - If **left is sorted**, check if target lies within left → adjust `high`.
     - If **right is sorted**, check if target lies within right → adjust `low`.
3. Return `-1` if not found.


## ❗ Edge Cases

- Array of one element
- Array not rotated at all
- Target not present
- Pivot is at the end/start


## 🔍 Example

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

## 🧾 Code

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        low, high = 0, len(nums) - 1

        while low <= high:
            middle = low + (high - low) // 2

            if nums[middle] == target:
                return middle

            # Left half is sorted
            if nums[middle] >= nums[low]:
                if nums[low] <= target < nums[middle]:
                    high = middle - 1
                else:
                    low = middle + 1

            # Right half is sorted
            else:
                if nums[middle] < target <= nums[high]:
                    low = middle + 1
                else:
                    high = middle - 1

        return -1
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(log n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Leverages sorted-half logic to do binary search
- ✅ Time complexity remains O(log n)
- 🔁 Reusable pattern for other rotated array problems
- 💡 Core building block for more advanced pivot-search tasks
