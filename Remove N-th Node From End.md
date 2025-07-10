<h1 align="center">✅ Remove N-th Node From End of List</h1>

<p align="center">
  <a href="https://leetcode.com/problems/remove-nth-node-from-end-of-list/">
    <img src="https://img.shields.io/badge/LeetCode-Remove%20Nth%20Node%20From%20End%20of%20List-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Linked%20List%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To remove the k-th node from the end of a singly linked list, we can’t go backward.  
But if we **move one pointer `k` nodes ahead**, and then move another pointer from the head, they’ll stay `k` apart.

When the lead pointer hits the end, the trailing pointer is just before the node to delete.


## 💡 Approach

1. Use a **dummy node** to handle edge cases (like deleting the head).
2. Initialize two pointers: `fast` and `slow` at the dummy.
3. Move `fast` forward by `n` steps.
4. Then move both `fast` and `slow` until `fast` reaches the end.
5. `slow.next` is now the node to delete → skip it with `slow.next = slow.next.next`.


## ❗ Edge Cases

- Removing the head (`n == length`)
- List has only one node
- `n` is guaranteed to be valid as per constraints


## 🔍 Example

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
Explanation: The 2nd node from the end is 4, which gets removed.
```


## 🧾 Code

```
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        fast = dummy
        slow = dummy

        # Move fast n steps ahead
        for _ in range(n):
            fast = fast.next

        # Move both until fast reaches the end
        while fast.next:
            fast = fast.next
            slow = slow.next

        # Skip the target node
        slow.next = slow.next.next

        return dummy.next
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Efficient one-pass solution with two pointers
- ✅ Dummy node simplifies edge-case handling
- 💡 Reusable pattern for many "from end of list" problems
- 🔁 Also useful for deleting K-th elements in more advanced variations
