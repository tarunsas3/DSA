<h1 align="center">😊 Count Number of Nice Subarrays</h1>

<p align="center">
  <a href="https://leetcode.com/problems/count-number-of-nice-subarrays/">
    <img src="https://img.shields.io/badge/LeetCode-Count%20Number%20of%20Nice%20Subarrays-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Prefix%20Sum%2C%20HashMap-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to count subarrays with exactly `k` **odd numbers**.  

This can be solved using a **prefix sum + hashmap** (counting technique):  
- Treat the number of odds seen so far as a running prefix sum.
- For each index, we count how many previous prefix sums are exactly `current_sum - k`.  
This gives us the number of subarrays ending at this index with exactly `k` odds.

Alternatively, we can use a **sliding window** to count subarrays with **at most k** odds and subtract subarrays with **at most (k-1)** odds.

We’ll use the prefix-sum + hashmap approach here (cleaner).

## 💡 Approach

1. Initialize `prefix_count = {0:1}` to handle the base case (no odds seen yet).
2. Maintain a `curr` variable for the current count of odds seen so far.
3. For each number:
   - If it’s odd, increment `curr`.
   - Add to the result: `prefix_count[curr - k]` (if it exists).
   - Increment `prefix_count[curr]`.
4. Return the result.

## ❗ Edge Cases

- All even numbers → only subarrays with `k=0` count.  
- `k` > number of odds in array → return `0`.  
- Small arrays (size < k) → return `0`.

## 🔍 Example

```
Input: nums = [1,1,2,1,1], k = 3
Output: 2
Explanation: The subarrays are [1,1,2,1] and [1,2,1,1].
```

## 🧾 Code

```
from collections import defaultdict

class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        prefix_count = defaultdict(int)
        prefix_count[0] = 1
        curr = 0
        res = 0

        for num in nums:
            curr += num % 2
            res += prefix_count[curr - k]
            prefix_count[curr] += 1

        return res
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

## 📌 Summary

- ✅ Prefix-sum + hashmap elegantly counts subarrays with exactly k odds.
- 🔁 Avoids brute-force enumeration of all subarrays.
- 🧠 Alternative: sliding window approach (at most k minus at most k-1).
- 🚀 Runs in O(n) — efficient for large inputs.