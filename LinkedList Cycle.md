<h1 align="center">✅ Linked List Cycle</h1>

<p align="center">
  <a href="https://leetcode.com/problems/linked-list-cycle/">
    <img src="https://img.shields.io/badge/LeetCode-Linked%20List%20Cycle-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Linked%20List%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To detect a cycle in a linked list, we use the **Floyd’s Tortoise and Hare** algorithm:
- A slow pointer moves one step at a time.
- A fast pointer moves two steps at a time.

If there is a cycle, the fast pointer will eventually meet the slow pointer inside the loop.


## 💡 Approach

1. Initialize two pointers: `slow = head`, `fast = head`.
2. Loop while `fast` and `fast.next` exist:
   - Move `slow` by 1 step
   - Move `fast` by 2 steps
   - If `slow == fast`, a cycle exists → return `True`
3. If loop ends, return `False` (no cycle)


## ❗ Edge Cases

- Empty list (`head = None`) → no cycle
- Single node without a cycle
- Cycle of only two nodes


## 🔍 Example

```
Input: head = [3,2,0,-4], pos = 1
Output: True
```

Explanation: There is a cycle where the tail connects to the second node.

## 🧾 Code

```
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = head
        fast = head

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


No extra space is used — just two pointers.

## 📌 Summary

- ✅ Uses two pointers (fast and slow) to detect cycles efficiently
- ✅ No need for extra memory like a set
- 💡 Floyd’s algorithm is used in many advanced linked list cycle problems
