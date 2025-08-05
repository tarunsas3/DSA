<h1 align="center">😡 Grumpy Bookstore Owner</h1>

<p align="center">
  <a href="https://leetcode.com/problems/grumpy-bookstore-owner/">
    <img src="https://img.shields.io/badge/LeetCode-Grumpy%20Bookstore%20Owner-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Array-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

The bookstore owner is sometimes **grumpy** (loses customers), but they can use a special trick for `minutes` to **not be grumpy**, maximizing satisfaction.  

We can split the problem:
- **Always satisfied**: Customers during non-grumpy minutes.
- **Extra satisfied**: Customers during grumpy minutes in a chosen `minutes` window.

We need to **find the best window of length `minutes`** where converting grumpy to calm gives the **maximum extra customers**.

## 💡 Approach

1. Compute `base_satisfied` = sum of customers when `grumpy[i] == 0`.  
2. Use a **sliding window** of size `minutes` to compute extra customers from grumpy periods:
   - Add `customers[i]` to `extra` if `grumpy[i] == 1`.  
   - Slide the window, subtracting outgoing and adding incoming grumpy contributions.
   - Track `max_extra`.  
3. Final answer = `base_satisfied + max_extra`.

## ❗ Edge Cases

- `minutes >= n` → owner can be calm for all customers.  
- All `grumpy = 0` → no need for the trick.  
- All `grumpy = 1` → best window is simply the largest sum of `minutes` customers.  

## 🔍 Example

```
Input: customers = [1,0,1,2,1,1,7,5], grumpy = [0,1,0,1,0,1,0,1], minutes = 3
Output: 16
Explanation: Owner stays calm for [1,1,7] → 16 total.
```

## 🧾 Code

```
class Solution:
    def maxSatisfied(self, customers: List[int], grumpy: List[int], minutes: int) -> int:
        base_satisfied = 0
        for i in range(len(customers)):
            if grumpy[i] == 0:
                base_satisfied += customers[i]
        
        extra = 0
        max_extra = 0
        
        # Initial window
        for i in range(minutes):
            if grumpy[i] == 1:
                extra += customers[i]
        max_extra = extra
        
        # Slide window
        for i in range(minutes, len(customers)):
            if grumpy[i] == 1:
                extra += customers[i]
            if grumpy[i - minutes] == 1:
                extra -= customers[i - minutes]
            max_extra = max(max_extra, extra)
        
        return base_satisfied + max_extra
```
## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Split into always satisfied + max window extra satisfied.
- 🚀 Sliding window to optimize for minutes.
- 🧠 A clean separation of baseline + maximization using a fixed-length window.
