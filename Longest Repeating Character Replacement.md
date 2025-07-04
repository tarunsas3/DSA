<h1 align="center">✅ Longest Repeating Character Replacement</h1>

<p align="center">
  <a href="https://leetcode.com/problems/longest-repeating-character-replacement/">
    <img src="https://img.shields.io/badge/LeetCode-Longest%20Repeating%20Character%20Replacement-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Hashing%2C%20String-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We want to find the **length of the longest substring** we can obtain by replacing at most `k` characters to make all characters in the substring the same.

The trick is:
- Track the **most frequent character** in the current window.
- If the rest of the characters (i.e. `window_size - max_freq`) are ≤ `k`, it's a valid window.
- If not, shrink the window from the left.


## 💡 Approach

1. Use a hash map or array to track character counts in the current window.
2. Initialize two pointers: `left` and `right`.
3. At each step:
   - Expand the window by moving `right`
   - Update the count of `s[right]`
   - Calculate the `max_freq` in the window
   - If `window_size - max_freq > k`, shrink the window from the left
4. Track and return the max window length observed.


## ❗ Edge Cases

- `k = 0` → window must be strictly uniform
- All characters the same → full length is valid
- String of distinct characters → only length `k + 1` can be valid


## 🔍 Example

```
Input: s = "AABABBA", k = 1
Output: 4
Explanation:
- Replace the second 'B' → "AABABBA" → "AABAAAA" or "AAAABBA"
- Longest substring with all repeating characters = 4
```

## 🧾 Code

```
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count = [0] * 26
        left = 0
        max_len = 0
        max_count = 0

        for right in range(len(s)):
            count[ord(s[right]) - ord('A')] += 1
            max_count = max(max_count, count[ord(s[right]) - ord('A')])

            while (right - left + 1) - max_count > k:
                count[ord(s[left]) - ord('A')] -= 1
                left += 1

            max_len = max(max_len, right - left + 1)

        return max_len
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

Space: Fixed-size array for 26 uppercase letters

## 📌 Summary

- ✅ Sliding window with greedy shrinking based on the most frequent char
- ✅ Elegant balance of window size vs. replaceable characters
- 💡 Core pattern for problems involving “at most k replacements”
- 🔁 Useful stepping stone to harder problems like:
   - Longest substring with at most two distinct characters
   - Replace characters to make substrings meet certain frequency rules
