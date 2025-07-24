<h1 align="center">📊 Maximum Average Subarray I</h1>

<p align="center">
  <a href="https://leetcode.com/problems/maximum-average-subarray-i/">
    <img src="https://img.shields.io/badge/LeetCode-Maximum%20Average%20Subarray%20I-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Array-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need the **maximum average of any subarray of length k**.  
Instead of recalculating the sum for every window, use a **sliding window**:
- Start with the sum of the first `k` elements.
- Slide the window by subtracting the leftmost element and adding the next element.
- Track the maximum sum as we go.

## 💡 Approach

1. Compute the sum of the first `k` elements as `curr_sum`.  
2. Set `max_sum = curr_sum`.  
3. Slide the window from index `k` to `n-1`:
   - Subtract the element leaving the window.
   - Add the element entering the window.
   - Update `max_sum` if needed.  
4. Return `max_sum / k`.

## ❗ Edge Cases

- `k = len(nums)` → return average of all numbers.  
- All negative numbers → still works (max can be negative).  
- Single element (`k = 1`) → just return the max element.  

## 🔍 Example

```
Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75
Explanation: The subarray [12,-5,-6,50] has the maximum average (51/4).
```

## 🧾 Code

```
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        curr_sum = sum(nums[:k])
        max_sum = curr_sum

        for i in range(k, len(nums)):
            curr_sum += nums[i] - nums[i - k]
            max_sum = max(max_sum, curr_sum)

        return max_sum / k
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Use a sliding window to avoid recomputing sums.
- 📉 Update the sum in O(1) each step.
- 🚀 Optimal O(n) solution with constant space.
- 🧠 Great introduction to the sliding window pattern.