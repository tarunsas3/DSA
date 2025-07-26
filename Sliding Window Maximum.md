<h1 align="center">📈 Sliding Window Maximum</h1>

<p align="center">
  <a href="https://leetcode.com/problems/sliding-window-maximum/">
    <img src="https://img.shields.io/badge/LeetCode-Sliding%20Window%20Maximum-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Hard-red?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Deque%2C%20Monotonic%20Queue-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We want the **maximum element in each sliding window of size `k`**.  

Naive approach: For each window, scan all `k` elements → O(n·k).  
Optimized approach: Use a **monotonic deque**:
- Store **indices** of elements in decreasing order of their values.
- Front of deque always holds the **max for the current window**.
- Remove elements:
  - From the back if they are **smaller than the current element** (they can’t be future max).
  - From the front if they are **out of the current window**.

This gives us **O(n)**.

## 💡 Approach

1. Use a deque `dq` to store **indices**, not values.  
2. Iterate `right` from 0 to `n-1`:
   - Pop from the back while `nums[dq[-1]] < nums[right]`.  
   - Append `right` to `dq`.  
3. Remove from the front if `dq[0] < right - k + 1` (out of window).  
4. Once `right >= k - 1`, append `nums[dq[0]]` to the result (window max).  

## ❗ Edge Cases

- `k = 1` → every element is its own window max.  
- `k = len(nums)` → result is `[max(nums)]`.  
- All elements same → deque grows to size `k` but values remain same.  

## 🔍 Example

```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation:
Windows: [1,3,-1] → 3  
          [3,-1,-3] → 3  
          [-1,-3,5] → 5  
          [-3,5,3] → 5  
          [5,3,6] → 6  
          [3,6,7] → 7
```

## 🧾 Code

```
from collections import deque

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        dq = deque()  # store indices
        res = []

        for right in range(len(nums)):
            # Remove smaller elements from back
            while dq and nums[dq[-1]] < nums[right]:
                dq.pop()
            dq.append(right)

            # Remove elements out of the current window
            if dq[0] <= right - k:
                dq.popleft()

            # Record max when window has at least k elements
            if right >= k - 1:
                res.append(nums[dq[0]])

        return res
```
## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(k)   |

## 📌 Summary

- ✅ Use a monotonic decreasing deque to track max efficiently.
- 🔄 Remove out-of-window and smaller elements dynamically.
- 🚀 O(n) solution — optimal for large arrays.
- 🧠 Template for many “sliding window with max/min” problems.
