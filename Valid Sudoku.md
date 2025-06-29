<h1 align="center">✅ Valid Sudoku</h1>

<p align="center">
  <a href="https://leetcode.com/problems/valid-sudoku/">
    <img src="https://img.shields.io/badge/LeetCode-Valid%20Sudoku-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Array%2C%20Hashing%2C%20Matrix%2C%20Set-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To validate a Sudoku board:
- Each **row**, **column**, and **3×3 box** must contain unique digits (1–9).
- Use hash sets to efficiently track previously seen numbers for each constraint.
- If any duplicate is detected in a row, column, or box → the board is invalid.


## 💡 Approach

1. Use three hash maps of sets:
   - `rows[i]` for digits in row `i`
   - `cols[j]` for digits in column `j`
   - `boxes[(i//3, j//3)]` for digits in each 3×3 sub-box
2. Traverse the board:
   - Skip cells with `.`
   - Check if the current digit exists in the corresponding row, column, or box
   - If yes → return `False`
   - Else, add it to the corresponding sets
3. If traversal completes with no violations → return `True`


## ❗ Edge Cases

- Empty cells (`"."`) are ignored  
- Duplicates must be checked within:
  - The same row
  - The same column
  - The same 3×3 sub-box  
- The board doesn't need to be solvable — only **valid so far**


## 🔍 Example

```
Input: 
board = [
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: True
```

## 🧾 Code

```
from collections import defaultdict

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = defaultdict(set)
        cols = defaultdict(set)
        boxs = defaultdict(set)

        for i in range(9):
            for j in range(9):
                val = board[i][j]
                if val == ".":
                    continue
                if (val in rows[i] or 
                    val in cols[j] or 
                    val in boxs[(i // 3, j // 3)]):
                    return False
                rows[i].add(val)
                cols[j].add(val)
                boxs[(i // 3, j // 3)].add(val)
        return True
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n²)|
| 🗃️ Space    | O(n) |

## 📌 Summary

- ✅ Uses sets to enforce uniqueness in rows, columns, and boxes.
- ✅ Constant-time operations for lookup and insertion.
- 🔍 Common interview problem to test matrix traversal + hashing.
- 💡 Extendable to generalized n×n Sudoku boards.
