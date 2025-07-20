<h1 align="center">🌀 Surrounded Regions</h1>

<p align="center">
  <a href="https://leetcode.com/problems/surrounded-regions/">
    <img src="https://img.shields.io/badge/LeetCode-Surrounded%20Regions-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Graph%2C%20DFS%2C%20Matrix-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We want to **flip all `'O'` regions that are completely surrounded by `'X'`**.  
Any `'O'` **connected to a border** must *not* be flipped.  
So, we mark all border-connected `'O'`s first, then flip the remaining `'O'`s to `'X'`.

## 💡 Approach

1. Traverse all the **border cells**:
   - If an `'O'` is found, perform DFS/BFS from there and mark all connected `'O'`s as safe (e.g., mark as `'T'`).
2. After marking, go through the entire board:
   - Convert all remaining `'O'`s to `'X'` (they’re surrounded).
   - Convert `'T'`s back to `'O'`.

## ❗ Edge Cases

- All `'X'` → no changes  
- Single `'O'` on the border → not flipped  
- All `'O'`s connected to the edge → no flip  
- Empty board → return as is

## 🔍 Example

```
Input:
board = [
  ["X","X","X","X"],
  ["X","O","O","X"],
  ["X","X","O","X"],
  ["X","O","X","X"]
]

Output:
[
  ["X","X","X","X"],
  ["X","X","X","X"],
  ["X","X","X","X"],
  ["X","O","X","X"]
]
```

## 🧾 Code

```
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        if not board or not board[0]:
            return

        rows, cols = len(board), len(board[0])

        def dfs(r, c):
            if (
                r < 0 or r >= rows or
                c < 0 or c >= cols or
                board[r][c] != 'O'
            ):
                return
            board[r][c] = 'T'
            for dr, dc in [(-1,0), (1,0), (0,-1), (0,1)]:
                dfs(r + dr, c + dc)

        # Start DFS from 'O's on the border
        for r in range(rows):
            dfs(r, 0)
            dfs(r, cols - 1)
        for c in range(cols):
            dfs(0, c)
            dfs(rows - 1, c)

        # Post-process the board
        for r in range(rows):
            for c in range(cols):
                if board[r][c] == 'O':
                    board[r][c] = 'X'
                elif board[r][c] == 'T':
                    board[r][c] = 'O'
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(m * n)   |
| 🗃️ Space    | O(m * n)   |

## 📌 Summary

- ✅ Flip only completely surrounded 'O' regions.
- 🔁 Mark safe 'O's starting from the border.
- ✂️ Flip the rest to 'X', revert safe ones to 'O'.
- 🧠 Very elegant application of flood fill.
