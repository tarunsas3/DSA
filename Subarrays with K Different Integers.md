<h1 align="center">📊 Subarrays with K Different Integers</h1>

<p align="center">
  <a href="https://leetcode.com/problems/subarrays-with-k-different-integers/">
    <img src="https://img.shields.io/badge/LeetCode-Subarrays%20with%20K%20Different%20Integers-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Hard-red?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20HashMap%2C%20Counting-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to count the number of subarrays that contain **exactly `K` distinct integers**.  
A direct way is complex — but there's a trick:
- **Count subarrays with at most `K` distinct** (`atMost(K)`).
- **Count subarrays with at most `K-1` distinct** (`atMost(K-1)`).
- Subtract:  

```
exactlyK = atMost(K) - atMost(K-1)
```

This simplifies the problem into counting **at most K** distinct subarrays using a **sliding window**.

## 💡 Approach

1. Implement `atMost(k)`:
 - Use a sliding window with a `count` map to track frequencies.
 - Expand `right` pointer, adding elements to `count`.
 - If distinct elements exceed `k`, shrink from `left`.
 - Add `(right - left + 1)` to result (number of valid subarrays ending at `right`).  
2. Return `atMost(K) - atMost(K-1)`.

## ❗ Edge Cases

- `K = 0` → return 0.  
- `K > len(nums)` → return 0.  
- All elements same → subarrays with exactly 1 distinct.  

## 🔍 Example

```
Input: nums = [1,2,1,2,3], K = 2
Output: 7
Explanation: Subarrays with exactly 2 distinct: 
[1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,3]
```

## 🧾 Code

```
from collections import defaultdict

class Solution:
    def subarraysWithKDistinct(self, nums: List[int], k: int) -> int:
        def atMost(k):
            count = defaultdict(int)
            left = 0
            res = 0
            distinct = 0
            
            for right in range(len(nums)):
                if count[nums[right]] == 0:
                    distinct += 1
                count[nums[right]] += 1

                while distinct > k:
                    count[nums[left]] -= 1
                    if count[nums[left]] == 0:
                        distinct -= 1
                    left += 1

                res += right - left + 1
            return res
        
        return atMost(k) - atMost(k - 1)
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

## 📌 Summary

- ✅ Use inclusion-exclusion: exactlyK = atMost(K) - atMost(K-1).
- 🔄 Sliding window efficiently tracks distinct count.
- 🚀 O(n) solution works well for large inputs.
- 🧠 A powerful trick for "exactly K" problems using "at most K".
