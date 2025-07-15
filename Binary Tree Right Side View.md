<h1 align="center">✅ Binary Tree Right Side View</h1>

<p align="center">
  <a href="https://leetcode.com/problems/binary-tree-right-side-view/">
    <img src="https://img.shields.io/badge/LeetCode-Right%20Side%20View-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Tree%2C%20BFS%2C%20DFS-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We want to return the **rightmost node** at each level of the binary tree — as if you are viewing the tree from the right side.

Both **BFS** and **DFS** can be used effectively to solve this.


## 💡 Approach (BFS)

1. Use a **queue** to perform level-order traversal (BFS).
2. For each level, add the **last node's value** to the result.
3. Enqueue children (left first, then right — order doesn't matter here).


## ❗ Edge Cases

- Empty tree → return `[]`
- Tree with only left children → only leftmost values at each level will be visible
- Tree with only right children → full path will be visible


## 🔍 Example

```
Input: root = [1,2,3,null,5,null,4]

        1
       / \
      2   3
       \    \
        5    4

Output: [1,3,4]
```

## 🧾 Code (BFS)

```
from collections import deque

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []

        result = []
        queue = deque([root])

        while queue:
            level_size = len(queue)
            for i in range(level_size):
                node = queue.popleft()

                if i == level_size - 1:
                    result.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

        return result
```

## 🧾 Code (DFS Alternative)

```
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        result = []

        def dfs(node, depth):
            if not node:
                return

            if depth == len(result):
                result.append(node.val)

            dfs(node.right, depth + 1)
            dfs(node.left, depth + 1)

        dfs(root, 0)
        return result
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

n = number of nodes

## 📌 Summary

- ✅ Either BFS (level-by-level) or DFS (right-first) works well
- ✅ Capture the last node seen at each level
- 💡 Great problem for mastering view-based tree traversal
- 🔁 Reusable pattern for left view, top view, and bottom view
