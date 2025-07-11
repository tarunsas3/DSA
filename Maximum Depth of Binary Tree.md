<h1 align="center">✅ Maximum Depth of Binary Tree</h1>

<p align="center">
  <a href="https://leetcode.com/problems/maximum-depth-of-binary-tree/">
    <img src="https://img.shields.io/badge/LeetCode-Maximum%20Depth%20of%20Binary%20Tree-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Tree%2C%20DFS%2C%20BFS-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To find the **maximum depth** of a binary tree, we want to know the **longest path** from the root node down to a leaf.

We can do this using **Depth-First Search (DFS)** or **Breadth-First Search (BFS)**.


## 💡 Approach

### ✅ Recursive DFS

1. If node is `None`, return `0`.
2. Recursively compute the depth of the left and right subtrees.
3. The max depth of the current node is `1 + max(left, right)`.


## ❗ Edge Cases

- Empty tree → depth is 0
- Single-node tree → depth is 1


## 🔍 Example

```
Input: root = [3,9,20,null,null,15,7]

        3
       / \
      9  20
         / \
        15  7

Output: 3
```

## 🧾 Code

🔁 Recursive DFS

```
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```

🔁 Iterative BFS (Level-order traversal)

```
from collections import deque

class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        queue = deque([root])
        depth = 0

        while queue:
            for _ in range(len(queue)):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            depth += 1

        return depth
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |


## 📌 Summary

- ✅ Core binary tree recursion problem
- ✅ Use either DFS or BFS to solve
- 💡 Builds foundation for other tree height/balance/diameter problems
- 🔁 Simple but elegant — great warm-up question
