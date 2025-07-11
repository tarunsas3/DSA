<h1 align="center">✅ Invert Binary Tree</h1>

<p align="center">
  <a href="https://leetcode.com/problems/invert-binary-tree/">
    <img src="https://img.shields.io/badge/LeetCode-Invert%20Binary%20Tree-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Tree%2C%20DFS%2C%20BFS-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

This problem is a classic tree problem:  
**Swap the left and right children** of every node in the binary tree.

This is essentially a **mirror transformation** of the tree.


## 💡 Approach

We can use **Depth-First Search (DFS)** or **Breadth-First Search (BFS)** to traverse the tree and swap child nodes.

### ✅ DFS (Recursive):

1. If node is `None`, return.
2. Recursively invert left and right subtrees.
3. Swap left and right children.


## ❗ Edge Cases

- Empty tree → return `None`
- Single node → already inverted
- Deep or unbalanced tree → recursion still handles it correctly


## 🔍 Example

```
Input:       4
           /   \
          2     7
         / \   / \
        1   3 6   9

Output:      4
           /   \
          7     2
         / \   / \
        9   6 3   1
```

## 🧾 Code

🔁 Recursive DFS

```
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None
        
        # Swap left and right
        root.left, root.right = self.invertTree(root.right), self.invertTree(root.left)
        return root
```

🔁 Iterative BFS (Alternative)

```
from collections import deque

class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return None
        
        queue = deque([root])

        while queue:
            node = queue.popleft()
            node.left, node.right = node.right, node.left

            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

        return root
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |


n = number of nodes

## 📌 Summary

- ✅ Easy and elegant recursive tree problem
- ✅ Classic use of DFS / BFS to traverse and modify nodes
- 💡 Useful to test your understanding of tree traversal and recursion
