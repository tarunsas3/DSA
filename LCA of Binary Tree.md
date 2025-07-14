<h1 align="center">✅ Lowest Common Ancestor of a Binary Search Tree</h1>

<p align="center">
  <a href="https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/">
    <img src="https://img.shields.io/badge/LeetCode-LCA%20of%20BST-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-BST%2C%20Tree%2C%20DFS-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

In a **Binary Search Tree**, for any node:
- All nodes in the **left subtree** are smaller
- All nodes in the **right subtree** are larger

To find the **Lowest Common Ancestor (LCA)** of nodes `p` and `q`:
- If both `p` and `q` are smaller than current node → move **left**
- If both are greater → move **right**
- If they split directions → current node is the **LCA**


## 💡 Approach

1. Start at the root.
2. Compare `p.val` and `q.val` with the current node:
   - If both less than current → go left.
   - If both greater → go right.
   - Else → we found the split point, return the current node.

This works because of the **BST property**.


## ❗ Edge Cases

- If `p == q`, return that node.
- `p` or `q` could be the ancestor of the other → still valid.


## 🔍 Example

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8

        6
       / \
      2   8
     / \ / \
    0  4 7  9

Output: 6 (LCA of 2 and 8)

Another: p = 2, q = 4 → LCA = 2
```

## 🧾 Code

✅ Recursive

```
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if p.val < root.val and q.val < root.val:
            return self.lowestCommonAncestor(root.left, p, q)
        elif p.val > root.val and q.val > root.val:
            return self.lowestCommonAncestor(root.right, p, q)
        else:
            return root
```

🔁 Iterative (Optional)

```
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        while root:
            if p.val < root.val and q.val < root.val:
                root = root.left
            elif p.val > root.val and q.val > root.val:
                root = root.right
            else:
                return root
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(h)   |
| 🗃️ Space    | O(h)   |

- h = height of the tree
- (O(log n) for balanced BST, O(n) for skewed tree)

## 📌 Summary

- ✅ Efficient thanks to BST ordering
- ✅ Clean recursion or iteration
- 💡 Highlights binary tree traversal with logical constraints
- 🔁 Common interview pattern for ancestor problems
