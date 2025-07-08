<h1 align="center">✅ Reverse Linked List</h1>

<p align="center">
  <a href="https://leetcode.com/problems/reverse-linked-list/">
    <img src="https://img.shields.io/badge/LeetCode-Reverse%20Linked%20List-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Linked%20List%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We’re asked to **reverse a singly linked list** in-place.

This means changing the `next` pointers of each node to point to its previous node instead of the next.


## 💡 Approach

1. Initialize two pointers:
   - `prev = None` (this will eventually be the new head)
   - `curr = head` (used to traverse the list)
2. Iterate through the list:
   - Store `curr.next` temporarily
   - Reverse the link → `curr.next = prev`
   - Move `prev` and `curr` one step forward
3. When `curr` becomes `None`, return `prev` as the new head.


## ❗ Edge Cases

- Empty list → return `None`
- List with only one node → return the node itself


## 🔍 Example

```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

```
Input: head = [1]
Output: [1]
```

```
Input: head = []
Output: []
```

## 🧾 Code

```
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        curr = head

        while curr:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt

        return prev
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

Constant space since we’re only using pointers

## 📌 Summary

- ✅ Classic two-pointer problem
- ✅ In-place with no extra space
- 💡 Foundational for:
  - Palindrome Linked List
  - Reversing in K-groups
  - Recursive vs iterative reversal variations
