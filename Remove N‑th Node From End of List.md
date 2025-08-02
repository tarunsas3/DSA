<h1 align="center">🗑️ Remove N‑th Node From End of List</h1>

<p align="center">
  <a href="https://leetcode.com/problems/remove-nth-node-from-end-of-list/">
    <img src="https://img.shields.io/badge/LeetCode-Remove%20Nth%20Node%20From%20End%20of%20List-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Linked%20List%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to remove the **n-th node from the end** of a singly linked list.  
A simple trick is to use **two pointers**:
- Move the first pointer `n` steps ahead.
- Then move both pointers together until the first reaches the end.
- The second pointer will now be at the **node before the one to remove**.

Using a **dummy node** simplifies edge cases (like removing the head).

## 💡 Approach

1. Create a **dummy node** pointing to `head`.  
2. Set two pointers `first` and `second` at `dummy`.  
3. Move `first` pointer `n+1` steps ahead.  
4. Move `first` and `second` together until `first` hits `None`.  
5. `second.next` now points to the node to remove — update it:  

   ```
   second.next = second.next.next
   ```
6. Return dummy.next (handles removing head gracefully).

## ❗ Edge Cases

- Removing the head (n = length of list).
- Single-node list (n = 1).
- n always valid per problem constraints.

## 🔍 Example

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
Explanation: The 2nd node from the end (4) is removed.
```

🧾 Code

```
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        first = second = dummy
        
        # Move first n+1 steps ahead
        for _ in range(n + 1):
            first = first.next
        
        # Move both pointers
        while first:
            first = first.next
            second = second.next
        
        # Remove target node
        second.next = second.next.next
        
        return dummy.next
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(L)   |
| 🗃️ Space    | O(1)   |

- L = length of the list

## 📌 Summary

- ✅ Two-pointer technique avoids computing list length.
- 💡 Dummy node makes edge cases easy.
- 🚀 Single-pass O(L) solution.
- 🧠 Pattern: "Fast-slow pointer for removing specific node."
