<h1 align="center">🌊 Number of Islands</h1>

<p align="center">
  <a href="https://leetcode.com/problems/number-of-islands/">
    <img src="https://img.shields.io/badge/LeetCode-Number%20of%20Islands-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Graph%2C%20BFS%2C%20DFS%2C%20Matrix-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We can think of the 2D grid as a graph where each `'1'` is land and `'0'` is water.  
To find the number of islands, we traverse the grid and perform **BFS or DFS** whenever we encounter land, marking all connected land as visited.

## 💡 Approach

1. Traverse the entire grid.
2. When you find a `'1'`, perform a BFS or DFS to mark the entire island as visited.
3. Increment the island count.
4. Return the total island count at the end.

We modify the grid or use a visited set to ensure we don’t revisit land we've already counted.

## ❗ Edge Cases

- Empty grid → return 0  
- All water → return 0  
- One big island → return 1  
- Diagonals don’t count as connected (only 4 directions)

## 🔍 Example

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]

Output: 3
Explanation: There are 3 separate islands.
```

## 🧾 Code

```
from collections import deque

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid:
            return 0

        rows, cols = len(grid), len(grid[0])
        islands = 0

        def bfs(r, c):
            queue = deque()
            queue.append((r, c))
            grid[r][c] = "0"

            while queue:
                row, col = queue.popleft()
                for dr, dc in [(-1,0),(1,0),(0,-1),(0,1)]:
                    nr, nc = row + dr, col + dc
                    if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == "1":
                        queue.append((nr, nc))
                        grid[nr][nc] = "0"

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == "1":
                    bfs(r, c)
                    islands += 1

        return islands
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(m * n)   |
| 🗃️ Space    | O(m * n)   |

## 📌 Summary

- ✅ View the grid as a graph.
- ✅ Use BFS or DFS to explore connected lands.
- 🔁 Avoid revisiting with marking or visited tracking.
- 🧩 A classic flood fill / connected components problem.
