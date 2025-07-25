<h1 align="center">🔍 Find All Anagrams in a String</h1>

<p align="center">
  <a href="https://leetcode.com/problems/find-all-anagrams-in-a-string/">
    <img src="https://img.shields.io/badge/LeetCode-Find%20All%20Anagrams%20in%20a%20String-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20String%2C%20HashMap-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to find **all starting indices** of substrings in `s` that are **anagrams of `p`**.  
This is similar to **Permutation in String**, but instead of returning `True/False`, we collect **all valid windows**.  

We can use a **fixed-size sliding window**:
- Maintain frequency counts for `p` and the current window in `s`.
- If the counts match → record the starting index.

## 💡 Approach

1. If `len(p) > len(s)`, return `[]`.  
2. Build a frequency counter for `p` (`p_count`).  
3. Slide a window of size `len(p)` across `s`:
   - Add the new character at `right`.
   - Remove the character leaving the window (`left`).
   - If the window matches `p_count`, store `left`.  
4. Return the list of starting indices.

## ❗ Edge Cases

- `p` longer than `s` → return empty list.  
- All characters in `p` are the same → check for repeated sequences.  
- `p` length 1 → just find occurrences of that character.  

## 🔍 Example

```
Input: s = "cbaebabacd", p = "abc"
Output: [0, 6]
Explanation: The substrings starting at indices 0 ("cba") and 6 ("bac") are anagrams of "abc".
```

## 🧾 Code

```
from collections import Counter

class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        len_p, len_s = len(p), len(s)
        if len_p > len_s:
            return []

        p_count = Counter(p)
        window = Counter()
        res = []

        for i in range(len_s):
            window[s[i]] += 1

            if i >= len_p:
                window[s[i - len_p]] -= 1
                if window[s[i - len_p]] == 0:
                    del window[s[i - len_p]]

            if window == p_count:
                res.append(i - len_p + 1)

        return res
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Sliding window efficiently tracks character counts.
- 📍 Record indices when window matches p_count.
- 🚀 O(n) solution — avoids checking all substrings.
- 🧠 Very similar to "Permutation in String", but collects all valid positions.