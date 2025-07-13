<h1 align="center">✅ Same Tree</h1>

<p align="center">
  <a href="https://leetcode.com/problems/same-tree/">
    <img src="https://img.shields.io/badge/LeetCode-Same%20Tree-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Tree%2C%20DFS%2C%20Recursion-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To check if two binary trees are **the same**, we compare:

- Their root values,
- Their left subtrees, and
- Their right subtrees.

If all of these match **recursively**, the trees are identical.


## 💡 Approach

Use a **recursive DFS** strategy:

1. If both nodes are `None`, return `True`.
2. If one is `None` and the other isn’t, return `False`.
3. If the values of the nodes are different, return `False`.
4. Recursively compare left and right children.


## ❗ Edge Cases

- Both trees are `None` → return `True`.
- Trees with identical structure but different values → return `False`.
- One tree is shorter/deeper than the other → return `False`.


## 🔍 Example

```
Input: p = [1,2,3], q = [1,2,3]
Output: True

Input: p = [1,2], q = [1,null,2]
Output: False
```

## 🧾 Code

```
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if not p and not q:
            return True
        if not p or not q or p.val != q.val:
            return False
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(h)   |

- n = total number of nodes
- h = height of the tree (due to recursion stack)

## 📌 Summary

- ✅ Simple and elegant recursive solution
- ✅ Great warm-up tree question
- 💡 Reinforces structural recursion and base case thinking
- 🔁 Useful foundation for comparing tree shapes or mirrors later
