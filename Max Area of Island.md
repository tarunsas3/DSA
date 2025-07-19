<h1 align="center">🧱 Max Area of Island</h1>

<p align="center">
  <a href="https://leetcode.com/problems/max-area-of-island/">
    <img src="https://img.shields.io/badge/LeetCode-Max%20Area%20of%20Island-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Graph%2C%20DFS%2C%20Matrix-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

Similar to **Number of Islands**, but instead of **counting islands**, we want the **maximum area** (number of connected `'1'`s) for any island.  
We explore each island using DFS and compute its area by counting connected land.

## 💡 Approach

1. Traverse the grid.
2. On encountering `'1'`, run a DFS to explore the entire island and count its area.
3. Track the maximum area found during traversal.
4. Return the maximum area at the end.

Mark visited land as `'0'` to avoid revisiting.

## ❗ Edge Cases

- All `0`s → return 0  
- All `1`s → return total area of the grid  
- Disconnected islands of varying sizes  

## 🔍 Example

```
Input: grid = [
  [0,0,1,0,0,0,0,1,0,0,0,0,0],
  [0,0,0,0,0,0,0,1,1,1,0,0,0],
  [0,1,1,0,1,0,0,0,0,0,0,0,0],
  [0,1,0,0,1,1,0,0,1,0,1,0,0],
  [0,1,0,0,1,1,0,0,1,1,1,0,0],
  [0,0,0,0,0,0,0,0,0,0,1,0,0],
  [0,0,0,0,0,0,0,1,1,1,0,0,0],
  [0,0,0,0,0,0,0,1,1,0,0,0,0]
]

Output: 6
Explanation: The largest island has an area of 6.
```

## 🧾 Code

```
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        max_area = 0

        def dfs(r, c):
            if r < 0 or r >= rows or c < 0 or c >= cols or grid[r][c] == 0:
                return 0
            grid[r][c] = 0
            area = 1
            for dr, dc in [(-1,0), (1,0), (0,-1), (0,1)]:
                area += dfs(r + dr, c + dc)
            return area

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 1:
                    max_area = max(max_area, dfs(r, c))

        return max_area
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(m * n)   |
| 🗃️ Space    | O(m * n)   |

## 📌 Summary

- ✅ DFS used to calculate area of each island.
- 📈 Maintain running max while exploring islands.
- 🧭 Only 4-directional connectivity is considered.
🔁 Flood fill variation focused on area, not count.
