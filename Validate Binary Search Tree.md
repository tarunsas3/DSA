<h1 align="center">✅ Validate Binary Search Tree</h1>

<p align="center">
  <a href="https://leetcode.com/problems/validate-binary-search-tree/">
    <img src="https://img.shields.io/badge/LeetCode-Validate%20BST-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-BST%2C%20DFS%2C%20Recursion-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

A valid **Binary Search Tree (BST)** must satisfy the following condition for every node:

- All values in the **left subtree** are **less than** the current node's value.
- All values in the **right subtree** are **greater than** the current node's value.
- Both left and right subtrees must also be valid BSTs.

This property must hold **recursively**, not just between parent and children.


## 💡 Approach

We perform a **DFS** traversal, passing down the allowed **min and max bounds** for each node:

1. Start at the root with `(-∞, +∞)` bounds.
2. For each node:
   - Check if its value is within the allowed range.
   - Recur left with updated max bound = `node.val`
   - Recur right with updated min bound = `node.val`
3. If all nodes satisfy the range, it's a valid BST.


## ❗ Edge Cases

- Duplicates: Not allowed in classic BSTs (strict inequality).
- Leaf nodes should still obey the ancestor constraints.
- An empty tree is considered valid.


## 🔍 Example

```
Input: root = [2,1,3]

    2
   / \
  1   3

Output: True

Input: root = [5,1,4,null,null,3,6]

    5
   / \
  1   4
     / \
    3   6

Output: False
Reason: 3 is in the right subtree of 5, but is less than 5.
```

## 🧾 Code

```
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def dfs(node, low, high):
            if not node:
                return True
            if not (low < node.val < high):
                return False
            return dfs(node.left, low, node.val) and dfs(node.right, node.val, high)

        return dfs(root, float('-inf'), float('inf'))
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(h)   |

- n = number of nodes
- h = height of tree (recursion stack)

## 📌 Summary

- ✅ Recursively enforce BST constraints via min/max bounds
- ✅ Avoids incorrect assumptions from just checking children
- 💡 Fundamental DFS pattern for validating tree structure
- 🔁 Great base for tree serialization & subtree checks
