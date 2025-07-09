<h1 align="center">✅ Merge Two Sorted Lists</h1>

<p align="center">
  <a href="https://leetcode.com/problems/merge-two-sorted-lists/">
    <img src="https://img.shields.io/badge/LeetCode-Merge%20Two%20Sorted%20Lists-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Linked%20List%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We're given two sorted linked lists.  
We want to **merge them into a single sorted list** without using extra space for new nodes — just rearranging `.next` pointers.


## 💡 Approach

1. Use a **dummy node** to help build the new list.
2. Initialize a `current` pointer to track the end of the merged list.
3. While both lists are non-empty:
   - Compare `list1.val` and `list2.val`.
   - Append the smaller node to `current.next`.
   - Move the pointer forward in the list from which the node was taken.
4. After the loop, append the remaining non-empty list to the end.
5. Return `dummy.next` which points to the merged list's head.


## ❗ Edge Cases

- One or both input lists are empty
- All elements of one list are smaller than the other


## 🔍 Example

```
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

## 🧾 Code

```
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        current = dummy

        while list1 and list2:
            if list1.val <= list2.val:
                current.next = list1
                list1 = list1.next
            else:
                current.next = list2
                list2 = list2.next
            current = current.next

        # Append the remaining nodes
        current.next = list1 if list1 else list2
        return dummy.next
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n + m)   |
| 🗃️ Space    | O(1)   |

- n and m are the lengths of list1 and list2.
- No extra space used aside from pointers.

## 📌 Summary

- ✅ Classic two-pointer approach for linked lists
- ✅ In-place merging with O(1) space
- 🔁 Foundational pattern for recursive merge sort on linked lists
- 💡 Clean and efficient — perfect for interviews!
