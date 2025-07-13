<h1 align="center">✅ Balanced Binary Tree</h1>

<p align="center">
  <a href="https://leetcode.com/problems/balanced-binary-tree/">
    <img src="https://img.shields.io/badge/LeetCode-Balanced%20Binary%20Tree-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Tree%2C%20DFS-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

A binary tree is considered **balanced** if the heights of the left and right subtrees of *every* node differ by **no more than 1**.

We can use a **bottom-up DFS approach** to calculate the height of each subtree and simultaneously check balance.


## 💡 Approach

1. Perform a **post-order traversal** (DFS).
2. For each node:
   - Recursively compute the height of the left and right subtrees.
   - If the difference is greater than 1, return `-1` as a signal that it’s unbalanced.
3. If any subtree returns `-1`, propagate it up.
4. If root is balanced, return `True`, else `False`.


## ❗ Edge Cases

- An empty tree is balanced by definition.
- Tree with one or two nodes is always balanced.


## 🔍 Example

```
Input: root = [3,9,20,null,null,15,7]
Output: True

Input: root = [1,2,2,3,3,null,null,4,4]
Output: False
```

## 🧾 Code

```
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def dfs(node):
            if not node:
                return 0

            left = dfs(node.left)
            if left == -1:
                return -1

            right = dfs(node.right)
            if right == -1:
                return -1

            if abs(left - right) > 1:
                return -1

            return 1 + max(left, right)

        return dfs(root) != -1
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(h)   |

- n = number of nodes
- h = height of tree (due to recursion)

## 📌 Summary

- ✅ Clean and efficient DFS solution
- ✅ Uses -1 as an early termination signal to avoid extra computation
- 💡 Very common interview question — good practice for recursion + tree depth
- 🔁 Reusable logic for other height-balanced tree problems
