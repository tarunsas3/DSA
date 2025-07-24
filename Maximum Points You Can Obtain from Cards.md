<h1 align="center">🃏 Maximum Points You Can Obtain from Cards</h1>

<p align="center">
  <a href="https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/">
    <img src="https://img.shields.io/badge/LeetCode-Maximum%20Points%20You%20Can%20Obtain%20from%20Cards-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Sliding%20Window%2C%20Array-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We can take **k cards from either the start or end** of the array.  
Instead of directly simulating all choices, flip the thinking:
- Picking `k` cards from the ends is equivalent to **leaving `n - k` cards unpicked in the middle**.
- So: **maximize sum of k picked cards = total sum - minimum sum of (n - k) consecutive cards**.

This becomes a **sliding window problem** for the smallest subarray of length `n - k`.

## 💡 Approach

1. Compute `total_sum` of all cards.  
2. If `k == len(cards)`, return `total_sum`.  
3. Use a sliding window of size `n - k` to find the **minimum sum subarray**.  
4. Subtract this minimum sum from `total_sum` to get the maximum score.  

## ❗ Edge Cases

- `k = len(cards)` → take all cards.  
- `k = 0` → score = 0.  
- All card values same → any combination gives the same score.  

## 🔍 Example

```
Input: cardPoints = [1,2,3,4,5,6,1], k = 3
Output: 12
Explanation: Take [1,2,3] from left or [6,1,5] from right → max = 12.
```

##🧾 Code

```
class Solution:
    def maxScore(self, cardPoints: List[int], k: int) -> int:
        n = len(cardPoints)
        total = sum(cardPoints)
        if k == n:
            return total

        window_size = n - k
        curr = sum(cardPoints[:window_size])
        min_sum = curr

        for i in range(window_size, n):
            curr += cardPoints[i] - cardPoints[i - window_size]
            min_sum = min(min_sum, curr)

        return total - min_sum
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Flip the problem: maximize picked = total - minimize unpicked.
- 🔁 Use a sliding window for the smallest subarray sum of size n - k.
- 🚀 Runs in O(n), efficient for large inputs.
- 🧠 Great trick: reframe “take from both ends” into a single contiguous segment problem.