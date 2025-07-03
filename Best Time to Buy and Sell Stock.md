<h1 align="center">✅ Best Time to Buy and Sell Stock</h1>

<p align="center">
  <a href="https://leetcode.com/problems/best-time-to-buy-and-sell-stock/">
    <img src="https://img.shields.io/badge/LeetCode-Best%20Time%20to%20Buy%20and%20Sell%20Stock-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Array%2C%20Greedy%2C%20Two%20Pointers-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We want to find the **maximum profit** from a single buy-sell transaction.  
Since we must **buy before we sell**, we can:
- Track the **minimum price so far**
- At each step, calculate profit if we sold at today’s price
- Keep updating the **maximum profit**


## 💡 Approach

1. Initialize:
   - `min_price = ∞`
   - `max_profit = 0`
2. Loop through each price:
   - If current price < `min_price`, update `min_price`
   - Else, calculate profit = `price - min_price` and update `max_profit` if it’s greater
3. Return `max_profit`


## ❗ Edge Cases

- Prices are strictly decreasing → no profit, return 0
- Only one price → not enough data to transact
- All prices are the same → no opportunity for profit


## 🔍 Example

```
Input: prices = [7, 1, 5, 3, 6, 4]
Output: 5
Explanation: Buy at 1, sell at 6 → profit = 6 - 1 = 5
```

## 🧾 Code

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = float('inf')
        max_profit = 0

        for price in prices:
            if price < min_price:
                min_price = price
            else:
                max_profit = max(max_profit, price - min_price)

        return max_profit
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |


## 📌 Summary

- ✅ Optimal solution using greedy + one-pass scan
- ✅ Very common in interviews — tests tracking min/max during traversal
- 💡 Helps build intuition for stock/interval/gain-loss problems
- 🔁 Foundation for harder variations like:
  - Best Time to Buy and Sell Stock II (multiple transactions)
  - With cooldown, transaction fees, or k transactions
