<h1 align="center">📅 Interval List Intersections</h1>

<p align="center">
  <a href="https://leetcode.com/problems/interval-list-intersections/">
    <img src="https://img.shields.io/badge/LeetCode-Interval%20List%20Intersections-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Two%20Pointers%2C%20Intervals-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need the **intersection** of two sorted, non-overlapping interval lists.  

A natural approach:
- Use **two pointers** (`i` for list A, `j` for list B).  
- For each pair `A[i], B[j]`, find the **overlap**:
start = max(A[i].start, B[j].start)
end = min(A[i].end, B[j].end)

sql
Copy
Edit
If `start <= end`, it’s a valid intersection.
- Move the pointer that ends first (to explore the next possible overlap).

## 💡 Approach

1. Initialize `i = 0, j = 0`, `result = []`.  
2. While both pointers are in range:
 - Compute `start = max(A[i][0], B[j][0])`.  
 - Compute `end = min(A[i][1], B[j][1])`.  
 - If `start <= end`, add `[start, end]` to result.  
 - Move the pointer where the interval ends first:
   - If `A[i][1] < B[j][1]`: increment `i`.  
   - Else: increment `j`.  
3. Return `result`.

## ❗ Edge Cases

- One or both lists are empty → return `[]`.  
- No intersections at all → return `[]`.  
- Fully nested intervals (one inside the other).  

## 🔍 Example

```
Input: A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
```

## 🧾 Code

```
class Solution:
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        i, j = 0, 0
        result = []
        
        while i < len(firstList) and j < len(secondList):
            start = max(firstList[i][0], secondList[j][0])
            end = min(firstList[i][1], secondList[j][1])
            
            if start <= end:
                result.append([start, end])
            
            if firstList[i][1] < secondList[j][1]:
                i += 1
            else:
                j += 1
        
        return result
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(m + n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Use two pointers to efficiently find intersections.
- 🚀 Each list is traversed at most once.
- 🧠 Pattern: “merge-style two-pointer” for sorted intervals.
