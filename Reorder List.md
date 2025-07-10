<h1 align="center">✅ Reorder List</h1>

<p align="center">
  <a href="https://leetcode.com/problems/reorder-list/">
    <img src="https://img.shields.io/badge/LeetCode-Reorder%20List-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Linked%20List%2C%20Two%20Pointers%2C%20Stack-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

Given a linked list `L0 → L1 → … → Ln-1 → Ln`, we want to reorder it as:

```
L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → …
```

To achieve this, we split the list into two halves, reverse the second half, and merge the two parts alternately.


## 💡 Approach

1. **Find the middle** of the list using fast & slow pointers.
2. **Reverse** the second half of the list.
3. **Merge** the two halves:
   - First half: `L0 → L1 → L2`
   - Reversed second half: `Ln → Ln-1 → Ln-2`
4. Interleave the two halves.


## ❗ Edge Cases

- Empty list or a list with one node — no reordering needed.
- Odd/even number of nodes both work with this logic.


## 🔍 Example

```
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]

Explanation:
- Original: 1 → 2 → 3 → 4 → 5
- Reversed second half: 5 → 4
- Merged: 1 → 5 → 2 → 4 → 3
```

## 🧾 Code

```
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        if not head or not head.next:
            return

        # Step 1: Find middle
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # Step 2: Reverse second half
        prev = None
        curr = slow.next
        slow.next = None  # Split the list into two
        while curr:
            next_temp = curr.next
            curr.next = prev
            prev = curr
            curr = next_temp

        # Step 3: Merge two halves
        first, second = head, prev
        while second:
            tmp1, tmp2 = first.next, second.next
            first.next = second
            second.next = tmp1
            first = tmp1
            second = tmp2
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

- One pass to find the middle, one pass to reverse, one pass to merge.
- Constant extra space used (no stack or array).

## 📌 Summary

- ✅ Three-step approach: split, reverse, merge
- ✅ In-place operation, modifies list without extra memory
- 🔁 Strong example of linked list pattern composition
- 💡 Good test of pointer manipulation and careful ordering
