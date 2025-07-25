<h1 align="center">🔀 Permutation in String</h1>

<p align="center">
  <a href="https://leetcode.com/problems/permutation-in-string/">
    <img src="https://img.shields.io/badge/LeetCode-Permutation%20in%20String-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Two%20Pointers%2C%20String-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to check if **any permutation of `s1` exists as a substring in `s2`**.  
This means: does `s2` contain a substring of length `len(s1)` with the **same character frequency** as `s1`?  

This is a perfect use case for a **fixed-size sliding window**:
- Maintain a window of size `len(s1)` on `s2`.
- Use frequency counters for characters in the window and `s1`.
- If they match at any point → return `True`.

## 💡 Approach

1. If `len(s1) > len(s2)`, return `False`.  
2. Build a frequency counter for `s1` (`count1`).  
3. Use a sliding window of size `len(s1)` on `s2`:
   - Add the new character at `right`.
   - Remove the old character at `left` (once the window size exceeds `len(s1)`).
   - Compare `count1` with the window's counter. If equal → return `True`.  
4. If no match found → return `False`.

## ❗ Edge Cases

- `s1` longer than `s2` → impossible.  
- All characters same in `s1` → need continuous block of same chars in `s2`.  
- `s1` length 1 → check if that char exists in `s2`.  

## 🔍 Example

```
Input: s1 = "ab", s2 = "eidbaooo"
Output: True
Explanation: "ba" is a permutation of "ab".
```

## 🧾 Code

```
from collections import Counter

class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        len1, len2 = len(s1), len(s2)
        if len1 > len2:
            return False

        count1 = Counter(s1)
        window = Counter()

        for i in range(len2):
            window[s2[i]] += 1

            if i >= len1:
                window[s2[i - len1]] -= 1
                if window[s2[i - len1]] == 0:
                    del window[s2[i - len1]]

            if window == count1:
                return True

        return False
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Fixed-size sliding window keeps character counts efficiently.
- 🔄 Compare window frequency with target frequency.
- 🚀 O(n) solution works for large strings.
- 🧠 Great pattern for “substring contains permutation” problems.