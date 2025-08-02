<h1 align="center">🔄 Linked List Cycle (Floyd’s Algorithm)</h1>

<p align="center">
  <a href="https://leetcode.com/problems/linked-list-cycle/">
    <img src="https://img.shields.io/badge/LeetCode-Linked%20List%20Cycle-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Linked%20List%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to check if a linked list contains a **cycle**.  

**Naive approach**: Use a set to store visited nodes. If we revisit a node, there’s a cycle (O(n) space).  

**Optimized approach**: Use **Floyd’s Cycle Detection (Tortoise and Hare)**:
- Two pointers:  
  - **Slow** moves 1 step.  
  - **Fast** moves 2 steps.  
- If the list has a cycle, `fast` will eventually meet `slow`.  
- If `fast` reaches `None`, no cycle exists.

## 💡 Approach

1. Initialize `slow = head` and `fast = head`.  
2. While `fast` and `fast.next` exist:
   - Move `slow` by 1 step, `fast` by 2 steps.  
   - If `slow == fast`, return `True` (cycle detected).  
3. If loop ends, return `False` (no cycle).  

## ❗ Edge Cases

- Empty list (`head = None`).  
- Single node with no cycle.  
- Single node pointing to itself (cycle).  

## 🔍 Example

```
Input: head = [3,2,0,-4], pos = 1
Output: True
Explanation: There is a cycle linking last node back to index 1.
```

## 🧾 Code

```
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Floyd’s Algorithm gives O(1) space solution.
- 🚀 Detects cycles without modifying the list.
- 🧠 Common pattern: fast & slow pointers for cycle detection.
