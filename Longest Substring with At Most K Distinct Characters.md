<h1 align="center">🔡 Longest Substring with At Most K Distinct Characters</h1>

<p align="center">
  <a href="https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/">
    <img src="https://img.shields.io/badge/LeetCode-Longest%20Substring%20with%20At%20Most%20K%20Distinct%20Characters-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20HashMap-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need the **longest substring** containing **at most K distinct characters**.  
This is a **classic sliding window** problem:
- Expand the window by moving `right` and adding characters to a frequency map.
- If the number of distinct characters exceeds `K`, shrink from `left` until valid.
- Track the maximum window length at each step.

## 💡 Approach

1. Use two pointers: `left` and `right`.  
2. Use a `char_count` dictionary to track character frequencies in the window.  
3. Expand `right` one character at a time:  
   - Add/update frequency in `char_count`.  
4. While `len(char_count) > k`, shrink the window:  
   - Decrease frequency of `s[left]`.  
   - If frequency becomes 0, remove it from `char_count`.  
   - Move `left` forward.  
5. Track the **maximum window length** during iteration.

## ❗ Edge Cases

- `k = 0` → return 0.  
- String length < k → return length of string.  
- All characters same → whole string is valid.

## 🔍 Example

```
Input: s = "eceba", k = 2
Output: 3
Explanation: "ece" is the longest substring with at most 2 distinct characters.
```

## 🧾 Code

```
from collections import defaultdict

class Solution:
    def lengthOfLongestSubstringKDistinct(self, s: str, k: int) -> int:
        if k == 0 or not s:
            return 0

        left = 0
        char_count = defaultdict(int)
        max_len = 0

        for right in range(len(s)):
            char_count[s[right]] += 1

            while len(char_count) > k:
                char_count[s[left]] -= 1
                if char_count[s[left]] == 0:
                    del char_count[s[left]]
                left += 1

            max_len = max(max_len, right - left + 1)

        return max_len
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(k)   |

## 📌 Summary

- ✅ Sliding window keeps track of valid substrings dynamically.
- 🔄 When distinct characters exceed k, shrink window from the left.
- 🧠 Pattern applies to many “longest substring with condition” problems.
- 🚀 Optimized for O(n) time complexity.