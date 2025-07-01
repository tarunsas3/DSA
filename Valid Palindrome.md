<h1 align="center">✅ Valid Palindrome</h1>

<p align="center">
  <a href="https://leetcode.com/problems/valid-palindrome/">
    <img src="https://img.shields.io/badge/LeetCode-Valid%20Palindrome-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Two%20Pointers%2C%20String-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

A string is a palindrome if it reads the same forwards and backwards.  
Since we only care about **alphanumeric characters** and must ignore **cases**, we can use two pointers to efficiently check characters from both ends, skipping over non-alphanumerics.


## 💡 Approach

1. Use two pointers: `left` starting at 0, and `right` at the end of the string.
2. While `left < right`:
   - Skip any non-alphanumeric characters using `.isalnum()`.
   - Compare lowercase characters at both pointers.
   - If they differ, return `False`.
   - Move `left` forward and `right` backward.
3. If the loop completes, return `True`.


## ❗ Edge Cases

- Empty string `""` → return `True` (empty string is a valid palindrome)
- `"a."` → return `True` (only `a` remains after cleaning)
- Strings with all punctuation should not cause errors


## 🔍 Example

```
Input: s = "A man, a plan, a canal: Panama"
Output: True
Explanation: After removing non-alphanumerics and lowering case → "amanaplanacanalpanama"
```

## 🧾 Code

```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        left, right = 0, len(s) - 1

        while left < right:
            while left < right and not s[left].isalnum():
                left += 1
            while left < right and not s[right].isalnum():
                right -= 1

            if s[left].lower() != s[right].lower():
                return False

            left += 1
            right -= 1

        return True
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

Constant space used since no extra strings are built (just two pointers)

## 📌 Summary

- ✅ Efficient two-pointer method
- ✅ Handles mixed casing and non-alphanumeric characters gracefully
- ✅ Optimal solution in both time and space
- 💡 A classic problem to practice string and pointer manipulation
