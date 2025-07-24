<h1 align="center">➕ Max Consecutive Ones III</h1>

<p align="center">
  <a href="https://leetcode.com/problems/max-consecutive-ones-iii/">
    <img src="https://img.shields.io/badge/LeetCode-Max%20Consecutive%20Ones%20III-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We want the **longest subarray of 1s** after flipping at most `k` zeros.  

A **sliding window** is perfect:
- Expand the window with `right` while counting zeros.
- If zeros exceed `k`, shrink the window from `left` until it’s valid.
- Track the maximum window size at every step.

## 💡 Approach

1. Initialize `left = 0`, `zero_count = 0`, `max_len = 0`.  
2. Expand `right` pointer:
   - If `nums[right] == 0`, increment `zero_count`.  
3. While `zero_count > k`, shrink the window:
   - If `nums[left] == 0`, decrement `zero_count`.  
   - Move `left` forward.  
4. Update `max_len` as the length of the current window.  

## ❗ Edge Cases

- `k = 0` → longest block of consecutive 1s without flips.  
- All 1s → return length of array.  
- All 0s and `k > 0` → min(k, len(nums)).  

## 🔍 Example

```
Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
Output: 6
Explanation: Flip two zeros at indices 5 and 10 → [1,1,1,0,0,1,1,1,1,1,1]
```

## 🧾 Code

```
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:
        left = 0
        zero_count = 0
        max_len = 0

        for right in range(len(nums)):
            if nums[right] == 0:
                zero_count += 1

            while zero_count > k:
                if nums[left] == 0:
                    zero_count -= 1
                left += 1

            max_len = max(max_len, right - left + 1)

        return max_len
```
## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Expand–shrink sliding window keeps window valid at all times.
- 🔄 Track zero count to ensure flips ≤ k.
- 🚀 Optimal O(n) time solution.
- 🧠 Great template for “longest subarray with at most X bad elements” problems.