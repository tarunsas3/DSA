<h1 align="center">✅ Two Sum II: Input Array Is Sorted</h1>

<p align="center">
  <a href="https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/">
    <img src="https://img.shields.io/badge/LeetCode-Two%20Sum%20II-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Two%20Pointers%2C%20Array-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

Since the input array is **sorted**, we can use the **two pointers technique** to efficiently find two numbers that sum up to the target.

- Start with one pointer at the beginning and one at the end.
- Move pointers inward based on the sum until you find the right pair.


## 💡 Approach

1. Initialize two pointers:
   - `left = 0`, `right = len(numbers) - 1`
2. While `left < right`:
   - Calculate the sum: `curr_sum = numbers[left] + numbers[right]`
   - If `curr_sum == target` → return `[left + 1, right + 1]` (1-indexed)
   - If `curr_sum < target` → move `left` pointer to the right
   - If `curr_sum > target` → move `right` pointer to the left


## ❗ Edge Cases

- Only one valid pair will exist (as guaranteed by the problem)
- Must return **1-based indices** (not zero-based)
- Array is guaranteed to be **non-decreasing**


## 🔍 Example

```
Input: numbers = [2, 7, 11, 15], target = 9
Output: [1, 2]
Explanation: 2 + 7 = 9 → return indices [1, 2]
```

## 🧾 Code

```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left, right = 0, len(numbers) - 1

        while left < right:
            curr_sum = numbers[left] + numbers[right]
            if curr_sum == target:
                return [left + 1, right + 1]
            elif curr_sum < target:
                left += 1
            else:
                right -= 1
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

Only two pointers and constant extra space used

## 📌 Summary

- ✅ Uses the sorted nature of the input for efficient two-pointer traversal.
- ✅ No need for a hash map (unlike the original Two Sum problem).
- 💡 Great example of the two-pointers pattern on sorted arrays.
- 🧪 One of the most asked variations of the classic Two Sum problem.
