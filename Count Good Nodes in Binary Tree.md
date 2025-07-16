<h1 align="center">✅ Count Good Nodes in Binary Tree</h1>

<p align="center">
  <a href="https://leetcode.com/problems/count-good-nodes-in-binary-tree/">
    <img src="https://img.shields.io/badge/LeetCode-Good%20Nodes%20in%20Binary%20Tree-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Tree%2C%20DFS-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

A node in the binary tree is **"good"** if **no node on the path from the root to that node has a value greater than it**.

We can use **DFS traversal** while carrying the max value seen so far.


## 💡 Approach

1. Start a **DFS** from the root node.
2. For each node:
   - Compare its value to the max value along the current path.
   - If the node's value is **greater than or equal to** this max, count it as a good node.
   - Update the max for the next recursive calls.
3. Recurse left and right, accumulating the count.


## ❗ Edge Cases

- Tree with all equal values → all nodes are good.
- Tree with decreasing values from root → only root is good.
- Empty tree → 0 good nodes.


## 🔍 Example

```
Input: root = [3,1,4,3,null,1,5]

        3
       / \
      1   4
     /   / \
    3   1   5

Output: 4
Good nodes are: 3 (root), 3 (left-left), 4, 5
```

## 🧾 Code

```
class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        def dfs(node, max_so_far):
            if not node:
                return 0

            count = 1 if node.val >= max_so_far else 0
            max_so_far = max(max_so_far, node.val)

            count += dfs(node.left, max_so_far)
            count += dfs(node.right, max_so_far)

            return count

        return dfs(root, root.val)
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(h)   |

- n = number of nodes
- h = height of the tree (recursion stack)

## 📌 Summary

- ✅ DFS with running max
- ✅ Intuition-based traversal with simple value comparison
- 💡 Helps reinforce parameter-passing in recursion
- 🔁 Common pattern in prefix/path-based tree problems
