<h1 align="center">🧩 Group Anagrams</h1>

<p align="center">
  <a href="https://leetcode.com/problems/group-anagrams/">
    <img src="https://img.shields.io/badge/LeetCode-Group%20Anagrams-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Hashing%2C%20Array%2C%20Frequency%20Map-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

Two strings are anagrams if they have the **exact same character counts**, regardless of order.  
So if we can represent each string by a unique frequency "signature", all anagrams will share the same signature.


## 💡 Approach

1. Use a **hashmap** (`defaultdict`) to group strings by their character frequency.
2. For each word:
   - Build a **26-length array** representing the count of each character (`a` to `z`).
   - Convert that array into a **tuple** (to make it hashable).
   - Use that tuple as the key in our hashmap to group anagrams.
3. Return all values of the hashmap as grouped anagram lists.


## ❗ Edge Cases

- `[""]` → Group with empty string key  
- `["x"]` → Single letter should return as a single group  
- All unique strings → Each goes in its own group  
- All anagrams → One large group


## 🔍 Example

```
Input: strs = ["act","pots","tops","cat","stop","hat"]
Output: [["act","cat"],["pots","tops","stop"],["hat"]]
```

## 🧾 Code

```
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        groups = defaultdict(list)
        for word in strs:
            count = [0] * 26  # Frequency array for a-z
            for char in word:
                count[ord(char) - ord('a')] += 1
            key = tuple(count)
            groups[key].append(word)
        return list(groups.values()
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n * k)   |
| 🗃️ Space    | O(n * k)   |

## 📌 Summary

- ✅ Uses frequency-based hashing to avoid sorting.
- ✅ Efficient for long strings compared to sort-based approaches.
- 🔁 Core technique in grouping or classification problems.
- 💡 A staple interview question that tests deep understanding of hashing and data modeling.
