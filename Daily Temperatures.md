<h1 align="center">✅ Daily Temperatures</h1>

<p align="center">
  <a href="="https://leetcode.com/problems/daily-temperatures/">
    <img src="https://img.shields.io/badge/LeetCode-Daily%20Temperatures-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Monotonic%20Stack%2C%20Array-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We're given a list of temperatures and need to find **how many days** it will take to get a **warmer temperature**.

Instead of checking future temperatures one by one (which is brute force), we can use a **monotonic decreasing stack** to keep track of unresolved days while moving forward.


## 💡 Approach

1. Initialize a stack to store indices of days with **unresolved warmer temperatures**.
2. Loop through the array:
   - While the current temperature is **warmer** than the temperature at the top of the stack:
     - Pop the index from the stack and calculate the number of days waited.
   - Push the current day's index onto the stack.
3. Return the result array.


## ❗ Edge Cases

- No future warmer day → answer is 0
- Multiple same-temperature days before a warmer one → wait continues
- Last day always has 0 (no future)


## 🔍 Example

```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```

Explanation:
- Day 0: wait 1 day for 74
- Day 2: wait 4 days for 76
- Day 6: no warmer day → 0

## 🧾 Code

```
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        
        res = [0] * len(temperatures)
        stack = []

        for index, value in enumerate(temperatures):
            while stack and value > stack[-1][1]:
                prevIndex, _ = stack.pop()
                res[prevIndex] = index - prevIndex
            stack.append((index, value))
        
        return res
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |

Each index is pushed and popped at most once → linear time

Stack stores at most n indices in worst case

## 📌 Summary

- ✅ Uses a monotonic stack for optimal future-value queries
- ✅ Efficient and elegant compared to brute force O(n²)
- 💡 Monotonic stacks appear in:
  - Next Greater Element
  - Largest Rectangle in Histogram
  - Daily Stock Span
