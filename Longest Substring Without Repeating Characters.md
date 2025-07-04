<h1 align="center">✅ Longest Substring Without Repeating Characters</h1>

<p align="center">
  <a href="https://leetcode.com/problems/longest-substring-without-repeating-characters/">
    <img src="https://img.shields.io/badge/LeetCode-Longest%20Substring%20Without%20Repeating%20Characters-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Hashing%2C%20String-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We need to find the length of the **longest substring** without any repeating characters.  
To do this efficiently, we can use the **sliding window** technique:
- Expand the window until there's a duplicate.
- Then, move the left pointer to shrink the window and remove the duplicate.


## 💡 Approach

1. Use a hash set to keep track of characters in the current window.
2. Initialize two pointers: `left` and `right` to 0.
3. While expanding `right`, check if character is in the set:
   - If yes, shrink window from `left` until duplicate is removed.
   - If no, add character and update the result with max window length.
4. Return the maximum window length found.


## ❗ Edge Cases

- Empty string → return 0
- All unique characters → return length of the string
- String of all identical characters → max length is 1


## 🔍 Example

```
Input: s = "abcabcbb"
Output: 3
Explanation: The longest substring without repeating characters is "abc" (length 3)
```

## 🧾 Code

```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        charSet = set()
        left = 0
        maxLength = 0

        for right in range(len(s)):
            while s[right] in charSet:
                charSet.remove(s[left])
                left += 1
            charSet.add(s[right])
            maxLength = max(maxLength, right - left + 1)

        return maxLength
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(k)   |


k = size of character set (bounded by 26 for lowercase or 128 for ASCII)

## 📌 Summary

- ✅ Efficient solution using sliding window + set
- ✅ Avoids re-checking previous characters unnecessarily
- 💡 Great pattern for window-based problems and frequency tracking
- 🔁 Extends into problems like:
   - Longest substring with at most K distinct characters
   - Longest substring with replacement
