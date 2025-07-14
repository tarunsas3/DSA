<h1 align="center">✅ Subtree of Another Tree</h1>

<p align="center">
  <a href="https://leetcode.com/problems/subtree-of-another-tree/">
    <img src="https://img.shields.io/badge/LeetCode-Subtree%20of%20Another%20Tree-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Tree%2C%20DFS%2C%20Recursion-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We want to check if tree `subRoot` is a **subtree** of tree `root`.

That means there exists a node in `root` such that the subtree rooted at that node is **identical** to `subRoot`.


## 💡 Approach

1. Use a **recursive DFS** to traverse the main `root` tree.
2. At each node, call a helper `isSameTree()` to check if current subtree is structurally and value-wise the same as `subRoot`.
3. If any such subtree matches, return `True`.


## ❗ Edge Cases

- `subRoot` is `None` → always a subtree.
- `root` is `None` but `subRoot` isn’t → cannot be a subtree.
- Identical trees → valid subtree.


## 🔍 Example

```
Input: 
root = [3,4,5,1,2], subRoot = [4,1,2]

        3
       / \
      4   5
     / \
    1   2

Output: True

Explanation: The subtree rooted at node 4 matches `subRoot`.
```

## 🧾 Code

```
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not root:
            return False
        if self.isSameTree(root, subRoot):
            return True
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)

    def isSameTree(self, s: Optional[TreeNode], t: Optional[TreeNode]) -> bool:
        if not s and not t:
            return True
        if not s or not t or s.val != t.val:
            return False
        return self.isSameTree(s.left, t.left) and self.isSameTree(s.right, t.right)
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(m * n)   |
| 🗃️ Space    | O(h)   |

- m = number of nodes in root
- n = number of nodes in subRoot
- h = height of the tree (due to recursion)

In the worst case, for every node in root, we call isSameTree.

## 📌 Summary

- ✅ Leverages the Same Tree logic
- ✅ Recursive DFS traversal and comparison
- 💡 Classic "tree in tree" pattern problem
- 🔁 Good for practicing tree traversal with conditions
