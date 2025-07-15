<h1 align="center">✅ Binary Tree Level Order Traversal</h1>

<p align="center">
  <a href="https://leetcode.com/problems/binary-tree-level-order-traversal/">
    <img src="https://img.shields.io/badge/LeetCode-Binary%20Tree%20Level%20Order%20Traversal-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Tree%2C%20BFS-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We want to return a list of values **level-by-level** from top to bottom in a binary tree.

This is a classic **Breadth-First Search (BFS)** problem, where we use a queue to traverse level by level.


## 💡 Approach

1. Use a **queue** (`collections.deque`) and start by enqueueing the root.
2. While the queue is not empty:
   - For each level, track the number of nodes (`len(queue)`).
   - Pop each node, collect its value into the current level list.
   - Enqueue left and right children if they exist.
3. Append the level list to the result.


## ❗ Edge Cases

- Empty tree → return `[]`
- Tree with only one node → return `[[val]]`


## 🔍 Example

```
Input: root = [3,9,20,null,null,15,7]

        3
       / \
      9  20
         / \
        15  7

Output: [[3],[9,20],[15,7]]
```

## 🧾 Code

```
from collections import deque

class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []

        result = []
        queue = deque([root])

        while queue:
            level = []
            for _ in range(len(queue)):
                node = queue.popleft()
                level.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            result.append(level)

        return result
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

## 📌 Summary

- ✅ Straightforward BFS pattern
- ✅ Level-wise separation using for _ in range(len(queue))
- 💡 Fundamental tree traversal technique
- 🔁 Useful in problems like zigzag traversal, right-side view, averages by level
