<h1 align="center">✅ Diameter of Binary Tree</h1>

<p align="center">
  <a href="https://leetcode.com/problems/diameter-of-binary-tree/">
    <img src="https://img.shields.io/badge/LeetCode-Diameter%20of%20Binary%20Tree-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Tree%2C%20DFS%2C%20Recursion-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

The **diameter** of a binary tree is the length of the longest path between any two nodes.  
This path **may or may not** pass through the root.

At each node, we want to consider:
- The **depth of the left subtree**
- The **depth of the right subtree**

The sum of these two depths is the diameter at that node.


## 💡 Approach

1. Use **DFS post-order traversal** to calculate the depth of left and right subtrees.
2. At each node, compute `leftDepth + rightDepth` and update a global `maxDiameter`.
3. Return the height of the tree as usual: `1 + max(left, right)`.


## ❗ Edge Cases

- Empty tree → diameter is 0
- Single-node tree → diameter is 0 (no edges)


## 🔍 Example

```
Input: root = [1,2,3,4,5]

        1
       / \
      2   3
     / \
    4   5

Output: 3

Explanation: The longest path is [4,2,1,3] or [5,2,1,3] → 3 edges
```

## 🧾 Code

```
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        self.diameter = 0

        def dfs(node):
            if not node:
                return 0
            left = dfs(node.left)
            right = dfs(node.right)

            # Update diameter at each node
            self.diameter = max(self.diameter, left + right)

            return 1 + max(left, right)

        dfs(root)
        return self.diameter
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(h)   |

- h = height of the tree (DFS recursion depth)

## 📌 Summary

- ✅ Compute the diameter via depths from left and right subtrees
- ✅ Clean DFS recursion with global state
- 💡 Builds understanding of tree height and dynamic properties
- 🔁 Common subroutine in tree-based interview problems
