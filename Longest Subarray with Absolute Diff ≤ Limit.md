<h1 align="center">📏 Longest Subarray with Absolute Diff ≤ Limit</h1>

<p align="center">
  <a href="https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit/">
    <img src="https://img.shields.io/badge/LeetCode-Longest%20Subarray%20with%20Abs%20Diff%20≤%20Limit-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Deque%2C%20Monotonic%20Queue-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We want the **longest subarray** where `max(subarray) - min(subarray) ≤ limit`.  

This requires **tracking the min and max** within a sliding window:
- As we expand `right`, maintain:
  - A **decreasing deque** for max values.
  - An **increasing deque** for min values.
- If the difference between front of these deques exceeds `limit`, shrink the window from `left`.
- Track the maximum window size.

This is a standard **monotonic queue** + sliding window pattern.

## 💡 Approach

1. Initialize two deques:  
   - `max_dq` (monotonic decreasing for max values).  
   - `min_dq` (monotonic increasing for min values).  
2. Expand `right`:
   - Insert `nums[right]` into deques (maintaining monotonic order).  
3. Check if `max_dq[0] - min_dq[0] > limit`:
   - If so, pop from deques if `nums[left]` equals their front and move `left`.  
4. Update the max length at each step.  

## ❗ Edge Cases

- `limit = 0` → all numbers in subarray must be equal.  
- Array length = 1 → return 1.  
- Strictly increasing/decreasing arrays with small `limit` → window often shrinks to 1.  

## 🔍 Example

```
Input: nums = [8,2,4,7], limit = 4
Output: 2
Explanation: Longest subarray is [2,4] with max-min = 2 ≤ 4.
```

## 🧾 Code

```
from collections import deque

class Solution:
    def longestSubarray(self, nums: List[int], limit: int) -> int:
        max_dq, min_dq = deque(), deque()
        left = 0
        res = 0

        for right, num in enumerate(nums):
            # Maintain max deque
            while max_dq and num > max_dq[-1]:
                max_dq.pop()
            max_dq.append(num)

            # Maintain min deque
            while min_dq and num < min_dq[-1]:
                min_dq.pop()
            min_dq.append(num)

            # Shrink window if condition violated
            while max_dq[0] - min_dq[0] > limit:
                if max_dq[0] == nums[left]:
                    max_dq.popleft()
                if min_dq[0] == nums[left]:
                    min_dq.popleft()
                left += 1

            res = max(res, right - left + 1)

        return res
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

## 📌 Summary

- ✅ Use two monotonic deques to track min and max efficiently.
- 🔄 Expand–shrink sliding window to maintain validity.
- 🚀 O(n) solution despite requiring dynamic max-min tracking.
- 🧠 Classic pattern for “longest subarray with constraints”.
