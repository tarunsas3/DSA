<h1 align="center">✅ Valid Anagram</h1>

<p align="center">
  <a href="https://leetcode.com/problems/valid-anagram/">
    <img src="https://img.shields.io/badge/LeetCode-Valid%20Anagram-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Hashing%2C%20Frequency%20Count-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To determine if two strings are anagrams, we must ensure they have the **same characters** with the **same frequency**.

A common and efficient way to do this for lowercase letters is to use a **fixed-size array of length 26**, where each index represents a character from `'a'` to `'z'`.


## 💡 Approach

1. Create an integer array `count` of size 26.
2. Loop through `s` and increment count for each character.
3. Loop through `t` and decrement count for each character.
4. If any element in `count` is not zero, return `False`. Otherwise, return `True`.


## ❗ Edge Cases

- `s = ""`, `t = ""` → return `True` (empty strings are trivially anagrams)  
- `s = "a"`, `t = "a"` → return `True`  
- `s = "ab"`, `t = "a"` → return `False` (length mismatch)  
- Unicode inputs require a different approach (see follow-up below)


## 🔍 Example

```
Input: s = "anagram", t = "nagaram"
Output: True
Explanation: All letters match in count and composition.
```

### 🧾 Code

```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        count = [0] * 26
        for x in s:
            count[ord(x) - ord('a')] += 1
        for x in t:
            count[ord(x) - ord('a')] -= 1
        for val in count:
            if val != 0:
                return False
        return True
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

### 🔄 Follow-Up: Unicode Support

If s and t contain Unicode characters, the fixed-size array won't work.
Instead, use a defaultdict(int) to count frequencies dynamically.

```
from collections import defaultdict

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        count = defaultdict(int)
        for x in s:
            count[x] += 1
        for x in t:
            count[x] -= 1
        for val in count.values():
            if val != 0:
                return False
        return True
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(k)   |

### 📌 Summary
- ✅ Efficient frequency counting using array or hashmap.
- 🧩 Works well for both fixed-size char sets and Unicode.
- 💡 Classic hashing technique for string matching problems.
