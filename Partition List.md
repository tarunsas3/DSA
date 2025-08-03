<h1 align="center">📑 Partition List</h1>

<p align="center">
  <a href="https://leetcode.com/problems/partition-list/">
    <img src="https://img.shields.io/badge/LeetCode-Partition%20List-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Linked%20List%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to rearrange the list so that:
- All nodes **less than `x`** appear before nodes **greater than or equal to `x`**.
- **Preserve the original relative order** within each partition.

This can be done using **two separate lists**:
- One for nodes `< x` (**before list**).
- One for nodes `>= x` (**after list**).  
Finally, **merge** them.

## 💡 Approach

1. Create two dummy heads: `before_head` and `after_head`.  
2. Iterate through the list:
   - If `node.val < x`, append it to the `before` list.
   - Else, append it to the `after` list.
3. Connect `before` list to `after` list.
4. Set `after.next = None` to avoid cycles.
5. Return `before_head.next`.

## ❗ Edge Cases

- All nodes less than `x` → after list is empty.  
- All nodes greater or equal to `x` → before list is empty.  
- Single-node list.  

## 🔍 Example

```
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
```

## 🧾 Code

```
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        before_head = before = ListNode(0)
        after_head = after = ListNode(0)
        
        while head:
            if head.val < x:
                before.next = head
                before = before.next
            else:
                after.next = head
                after = after.next
            head = head.next
        
        after.next = None
        before.next = after_head.next
        
        return before_head.next
```
| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Separate into before and after lists, then merge.
- 🚀 Preserves original order in each partition.
- 🧠 Common linked list partitioning trick using dummy nodes.
