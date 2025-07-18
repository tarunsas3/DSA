<h1 align="center">🪨 Last Stone Weight</h1>

<p align="center">
  <a href="https://leetcode.com/problems/last-stone-weight/">
    <img src="https://img.shields.io/badge/LeetCode-Last%20Stone%20Weight-orange?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-brightgreen?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Heap-blue?style=flat-square" />
</p>


## 🧠 Intuition

You are given stones with weights. Every turn, take the two heaviest stones and smash them:

- If equal → both destroyed.
- If different → heavier becomes `heavier - lighter`.

Continue until one or no stone remains. Return the last weight (or 0).

This is a **max-heap** problem:
- Python has a **min-heap**, so we store **negative weights**.


## 🔍 Example

```
Input: stones = [2,7,4,1,8,1]
Output: 1

Process:
- 8 and 7 -> smash -> 1 (new stone)
- heap: [4,2,1,1,1] → repeat...
```

## 🧾 Code (Max-Heap via Min-Heap Trick)

```
import heapq

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        # Max-heap by negating all values
        stones = [-s for s in stones]
        heapq.heapify(stones)
        
        while len(stones) > 1:
            first = -heapq.heappop(stones)
            second = -heapq.heappop(stones)
            
            if first != second:
                heapq.heappush(stones, -(first - second))
        
        return -stones[0] if stones else 0
```
## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n log n)   |
| 🗃️ Space    | O(n)   |


## ✅ Summary

- Approach	Time	Space	Notes
- Max-Heap	O(n log n)	O(n)	Clean and optimal
- Sort each time	O(n²)	O(1)	Too slow for large inputs
