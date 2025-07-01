<h1 align="center">✅ Longest Consecutive Sequence</h1>

<p align="center">
  <a href="https://leetcode.com/problems/longest-consecutive-sequence/">
    <img src="https://img.shields.io/badge/LeetCode-Longest%20Consecutive%20Sequence-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Array%2C%20Hashing%2C%20Set-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We want to find the longest sequence of consecutive integers (e.g., `[3, 4, 5, 6]`) in an array.  
Sorting the array would work but take `O(n log n)` time.  
Instead, we can use a `set` to enable constant-time lookups and build sequences only from the starting number.

## 💡 Approach

1. Add all elements to a set `seen` for O(1) access.
2. Loop through each number in the set.
3. Only try to build a sequence from numbers that **don't have a predecessor** (`num - 1` not in set).
4. From each such number, incrementally build the sequence as long as `num + 1`, `num + 2`, ... exist in the set.
5. Track and return the longest length found.

## ❗ Edge Cases

- `[]` → return `0` (empty array has no sequence)  
- `[100]` → return `1` (single element forms a sequence of length 1)  
- Repeated numbers should not affect result due to use of `set`

## 🔍 Example

```
Input: nums = [2, 20, 4, 10, 3, 4, 5]
Output: 4
Explanation: The longest consecutive sequence is [2, 3, 4, 5].
```

## 🧾 Code

```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if not nums:
            return 0

        seen = set(nums)
        longest = 0

        for num in seen:
            if num - 1 not in seen:
                curr = num
                length = 1
                while curr + 1 in seen:
                    curr += 1
                    length += 1
                longest = max(longest, length)

        return longest
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |


## 📌 Summary

- ✅ Uses a set for constant-time lookups
- ✅ Only attempts sequence building from start elements
- ✅ Fully satisfies O(n) time constraint
- 💡 Elegant way to avoid sorting and redundant work
