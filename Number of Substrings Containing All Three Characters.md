<h1 align="center">🔤 Number of Substrings Containing All Three Characters</h1>

<p align="center">
  <a href="https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/">
    <img src="https://img.shields.io/badge/LeetCode-Number%20of%20Substrings%20Containing%20All%20Three%20Characters-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to count substrings that contain at least one occurrence of each character `'a'`, `'b'`, and `'c'`.  

A **sliding window** is ideal:
- Expand the right pointer to include characters.
- Once the window contains all 3 characters, **shrink from the left** while still maintaining validity.
- For each valid window, all substrings starting at `left` and ending at or after `right` are valid.

## 💡 Approach

1. Use two pointers (`left`, `right`) and a frequency dictionary for `'a'`, `'b'`, `'c'`.
2. Expand `right` to include new characters.
3. When all 3 characters are present:
   - Count substrings: `count += (len(s) - right)`  
     (all substrings starting at `left` with end ≥ `right` are valid)
   - Shrink `left` to look for smaller valid windows.
4. Continue until `right` reaches the end.

## ❗ Edge Cases

- String shorter than 3 → return `0`
- All same character → return `0`
- Already balanced (e.g., `"abc"`) → count 1

## 🔍 Example

```
Input: s = "abcabc"
Output: 10
Explanation: The substrings are:
"abc", "abca", "abcab", "abcabc", "bca", "bcab", "bcabc", "cab", "cabc", "abc"
```

## 🧾 Code

```
class Solution:
    def numberOfSubstrings(self, s: str) -> int:
        count = {'a': 0, 'b': 0, 'c': 0}
        left = 0
        res = 0

        for right in range(len(s)):
            count[s[right]] += 1

            while all(count[c] > 0 for c in 'abc'):
                res += len(s) - right
                count[s[left]] -= 1
                left += 1

        return res
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Sliding window + two pointers for efficient counting.
- 📐 Key trick: once window is valid, all suffixes beyond right are valid too.
- 🔄 Greedy shrinking ensures minimal window and counts all possibilities.
- 🚀 Optimal O(n) solution for this substring-counting problem.