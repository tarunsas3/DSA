<h1 align="center">⚡ Binary Subarrays With Sum</h1>

<p align="center">
  <a href="https://leetcode.com/problems/binary-subarrays-with-sum/">
    <img src="https://img.shields.io/badge/LeetCode-Binary%20Subarrays%20With%20Sum-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Prefix%20Sum%2C%20HashMap%2C%20Sliding%20Window-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to count **subarrays whose sum equals `goal`**.  
This is similar to the **Subarray Sum Equals K** problem, but since the array is **binary (0/1)**, it simplifies:
- Use a **prefix sum**: running sum of elements.
- Use a hashmap to store how many times each prefix sum has appeared.
- At each index, if `curr_sum - goal` exists in the hashmap, add its count to the result.

This avoids checking all subarrays individually.

## 💡 Approach

1. Initialize `count = {0:1}` to handle subarrays starting at index 0.  
2. Iterate through `nums`, keeping a running `curr_sum`.  
3. For each `curr_sum`, check if `curr_sum - goal` exists in `count`.  
4. Add that count to the result.  
5. Update `count[curr_sum]`.  

## ❗ Edge Cases

- `goal = 0` → subarrays of all zeros count.  
- All 1s with `goal > len(nums)` → result = 0.  
- Empty array → result = 0.  

## 🔍 Example

```
Input: nums = [1,0,1,0,1], goal = 2
Output: 4
Explanation: Subarrays with sum = 2:
[1,0,1], [0,1,0,1], [1,0,1,0], [0,1,0,1]
```

## 🧾 Code

```
from collections import defaultdict

class Solution:
    def numSubarraysWithSum(self, nums: List[int], goal: int) -> int:
        count = defaultdict(int)
        count[0] = 1
        curr_sum = 0
        res = 0

        for num in nums:
            curr_sum += num
            res += count[curr_sum - goal]
            count[curr_sum] += 1

        return res
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |


## 📌 Summary

- ✅ Use prefix sum + hashmap for O(n) counting.
- 🔄 Avoid brute-force checking of subarrays.
- 🚀 Works efficiently for large arrays.
- 🧠 A standard trick for subarray-sum counting problems.
