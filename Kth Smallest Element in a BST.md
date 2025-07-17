<h1 align="center">🔢 Kth Smallest Element in a BST</h1>

<p align="center">
  <a href="https://leetcode.com/problems/kth-smallest-element-in-a-bst/">
    <img src="https://img.shields.io/badge/LeetCode-Kth%20Smallest%20in%20BST-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-BST%2C%20DFS%2C%20Inorder-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

In a **Binary Search Tree**, an **in-order traversal** visits nodes in **sorted (ascending)** order.  
So the `k`th node visited during an in-order traversal will be the `k`th smallest element.


## 💡 Approach

- Perform an in-order DFS traversal.
- Use a counter to track how many nodes have been visited.
- Once `k` nodes are visited, **return the value immediately**.


## ❗ Edge Cases

- `k == 1`: Return the minimum node (leftmost).
- Unbalanced trees: Still works as traversal order remains correct.
- Early return optimization avoids unnecessary traversal.


## 🔍 Example

```
Input: root = [3,1,4,null,2], k = 1

    3
   / \
  1   4
   \
    2

Output: 1

Input: root = [5,3,6,2,4,null,null,1], k = 3

        5
       / \
      3   6
     / \
    2   4
   /
  1

Output: 3
```

## 🧾 Code

```
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        self.k = k
        self.result = None

        def inorder(node):
            if not node or self.result is not None:
                return

            inorder(node.left)

            self.k -= 1
            if self.k == 0:
                self.result = node.val
                return

            inorder(node.right)

        inorder(root)
        return self.result
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(h + k)   |
| 🗃️ Space    | O(h)   |

- h = height of tree (for recursion)
- Best-case: Early return after k elements

## 📌 Summary

- ✅ Uses BST's sorted in-order traversal
- ✅ Efficiently finds kth smallest without sorting
- 🚀 Optimized with early return once found
- 🌳 Pattern useful for tree-based selection problems
