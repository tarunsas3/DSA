<h1 align="center">🪟 Minimum Window Substring</h1>

<p align="center">
  <a href="https://leetcode.com/problems/minimum-window-substring/">
    <img src="https://img.shields.io/badge/LeetCode-Minimum%20Window%20Substring-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Hard-red?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Two%20Pointers%2C%20HashMap-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We want the **smallest substring of `s`** that contains **all characters of `t`** (including duplicates).  

This is a **classic variable-size sliding window** problem:
- Expand `right` to include characters until the window is valid (contains all of `t`).
- Once valid, try shrinking from `left` to minimize the window.
- Track the smallest valid window throughout.

## 💡 Approach

1. Build a frequency map `t_count` for `t`.  
2. Use two pointers (`left`, `right`) to define the window.  
3. Use `window_count` to track counts in the current window.  
4. Maintain a `have` counter for how many required characters are satisfied and a `need = len(t_count)`.  
5. Expand `right`:
   - Add `s[right]` to `window_count`.  
   - If its count matches `t_count`, increment `have`.  
6. When `have == need` (window valid):
   - Update the smallest window if needed.  
   - Shrink from `left` until it’s no longer valid.  
7. Return the smallest valid window or `""` if none exists.

## ❗ Edge Cases

- `t` longer than `s` → return `""`.  
- `s` or `t` empty → return `""`.  
- Characters in `t` not in `s` → return `""`.  

## 🔍 Example

```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: "BANC" is the smallest window containing 'A', 'B', and 'C'.
```

## 🧾 Code

```
from collections import Counter

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if not s or not t:
            return ""

        t_count = Counter(t)
        window_count = {}
        have, need = 0, len(t_count)
        res, res_len = [-1, -1], float("inf")
        left = 0

        for right in range(len(s)):
            char = s[right]
            window_count[char] = window_count.get(char, 0) + 1

            if char in t_count and window_count[char] == t_count[char]:
                have += 1

            while have == need:
                # Update result
                if (right - left + 1) < res_len:
                    res = [left, right]
                    res_len = right - left + 1

                # Shrink window
                window_count[s[left]] -= 1
                if s[left] in t_count and window_count[s[left]] < t_count[s[left]]:
                    have -= 1
                left += 1

        l, r = res
        return s[l:r+1] if res_len != float("inf") else ""
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Expand–shrink sliding window to maintain minimal valid substring.
- 📐 Track counts with have vs need for efficient validity check.
- 🚀 Optimal O(n) solution, works well for large strings.
- 🧠 Classic hard-level template for window problems.