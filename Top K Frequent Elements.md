<h1 align="center">✅ Top K Frequent Elements</h1>

<p align="center">
  <a href="https://leetcode.com/problems/top-k-frequent-elements/">
    <img src="https://img.shields.io/badge/LeetCode-Top%20K%20Frequent%20Elements-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Hashing%2C%20Bucket%20Sort%2C%20Frequency-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We want to find the `k` most frequent elements in the array.  
Rather than sorting or using a heap (which gives `O(n log n)` or `O(n log k)`), we can **bucket the numbers by their frequency** using a frequency map and a reverse-indexed list.


## 💡 Approach

1. Count the frequency of each element using a dictionary.
2. Create a list of buckets where index `i` holds all numbers that appeared exactly `i` times.
3. Iterate through the bucket list in reverse (from highest frequency to lowest), collecting elements until we've picked `k` of them.


## ❗ Edge Cases

- All elements have the same frequency → return any `k`
- Only one unique number → return that number
- Array contains negative numbers or large ranges — still valid
- Input may have up to 10⁴ elements → must avoid sorting-based solutions for efficiency


## 🔍 Example

```
Input: nums = [1,2,2,3,3,3], k = 2
Output: [2,3]
Explanation: 3 appears 3 times, 2 appears 2 times.
```

## 🧾 Code

```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        freq = [[] for _ in range(len(nums) + 1)]

        for num in nums:
            count[num] = count.get(num, 0) + 1
        
        for num, occ in count.items():
            freq[occ].append(num)
        
        res = []
        for i in range(len(freq) - 1, -1, -1):
            for num in freq[i]:
                res.append(num)
                if len(res) == k:
                    return res
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |


## 📌 Summary

- ✅ Uses bucket sort to avoid sorting or using a heap.
- ✅ Truly linear time: optimal for large inputs.
- 💡 Ideal approach for “Top K” problems where k is small or varies.
- 🔁 Pattern applies to frequency-based grouping, histogram problems, etc.
