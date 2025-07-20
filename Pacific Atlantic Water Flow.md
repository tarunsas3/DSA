<h1 align="center">🌊 Pacific Atlantic Water Flow</h1>

<p align="center">
  <a href="https://leetcode.com/problems/pacific-atlantic-water-flow/">
    <img src="https://img.shields.io/badge/LeetCode-Pacific%20Atlantic%20Water%20Flow-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Graph%2C%20DFS%2C%20Matrix-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

Each cell can potentially flow to either the **Pacific** or **Atlantic Ocean** depending on height.  
Instead of checking from each cell **where the water goes**, we reverse the thinking:  
We **start from the oceans** and perform DFS/BFS **inward**, tracking cells that can reach the oceans.

## 💡 Approach

1. Initialize two boolean matrices: `pacific_reachable` and `atlantic_reachable`.
2. Start DFS from:
   - All cells on the top and left edges for **Pacific**.
   - All cells on the bottom and right edges for **Atlantic**.
3. During DFS, only move to neighbors with height **greater than or equal** (water can only flow downhill or stay level).
4. The final result includes all cells that are reachable from **both** oceans.

## ❗ Edge Cases

- Empty grid → return `[]`  
- Flat grid → all cells flow to both oceans  
- Steep slopes → only border cells flow to oceans  

## 🔍 Example

```
Input: heights = [
  [1, 2, 2, 3, 5],
  [3, 2, 3, 4, 4],
  [2, 4, 5, 3, 1],
  [6, 7, 1, 4, 5],
  [5, 1, 1, 2, 4]
]

Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
```

## 🧾 Code

```
class Solution:
    def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
        if not heights or not heights[0]:
            return []

        rows, cols = len(heights), len(heights[0])
        pacific = set()
        atlantic = set()

        def dfs(r, c, visited, prev_height):
            if (
                r < 0 or r >= rows or
                c < 0 or c >= cols or
                (r, c) in visited or
                heights[r][c] < prev_height
            ):
                return
            visited.add((r, c))
            for dr, dc in [(-1,0), (1,0), (0,-1), (0,1)]:
                dfs(r + dr, c + dc, visited, heights[r][c])

        for c in range(cols):
            dfs(0, c, pacific, heights[0][c])        # Top edge
            dfs(rows - 1, c, atlantic, heights[rows - 1][c])  # Bottom edge

        for r in range(rows):
            dfs(r, 0, pacific, heights[r][0])         # Left edge
            dfs(r, cols - 1, atlantic, heights[r][cols - 1])  # Right edge

        return list(pacific & atlantic)
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(m * n)   |
| 🗃️ Space    | O(m * n)   |

- m = rows
- n = cols

## 📌 Summary

- 🔁 Reverse the simulation: flow from the oceans, not to them.
- ✅ Track cells reachable from both oceans with DFS/BFS.
- 🌊 Excellent matrix + graph traversal problem.
- 🧠 Key idea: intersection of Pacific and Atlantic reachable areas.
