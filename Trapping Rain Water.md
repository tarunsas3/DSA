<h1 align="center">💧 Trapping Rain Water</h1>

<p align="center">
  <a href="https://leetcode.com/problems/trapping-rain-water/">
    <img src="https://img.shields.io/badge/LeetCode-Trapping%20Rain%20Water-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Hard-red?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Two%20Pointers%2C%20Stack%2C%20Dynamic%20Programming-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

Water can only be trapped **between taller bars**.  
For each index, the trapped water depends on:

```
min(max_left, max_right) - height[i]
```

We need to know the tallest bars on **both sides**.  

Instead of precomputing arrays, we can optimize with **two pointers**:
- Use `left` and `right` pointers.
- Keep track of `max_left` and `max_right`.
- Move the pointer with the **smaller height**, updating trapped water.

## 💡 Approach

1. Initialize `left = 0`, `right = n-1`, `max_left = 0`, `max_right = 0`, `water = 0`.  
2. While `left < right`:
   - If `height[left] < height[right]`:
     - If `height[left] >= max_left`, update `max_left`.  
     - Else, add `max_left - height[left]` to `water`.  
     - Move `left` forward.  
   - Else:
     - If `height[right] >= max_right`, update `max_right`.  
     - Else, add `max_right - height[right]` to `water`.  
     - Move `right` backward.  
3. Return `water`.

## ❗ Edge Cases

- Empty array → 0 water.  
- Monotonic increasing/decreasing heights → no water.  
- Only 1 or 2 bars → no water can be trapped.  

## 🔍 Example

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation:
Water trapped: 1 + 1 + 2 + 1 + 1 = 6
```

## 🧾 Code

```
class Solution:
    def trap(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        max_left, max_right = 0, 0
        water = 0

        while left < right:
            if height[left] < height[right]:
                if height[left] >= max_left:
                    max_left = height[left]
                else:
                    water += max_left - height[left]
                left += 1
            else:
                if height[right] >= max_right:
                    max_right = height[right]
                else:
                    water += max_right - height[right]
                right -= 1

        return water
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

## 📌 Summary

- ✅ Two-pointer approach avoids extra memory.
- 💡 Always move the pointer with the smaller height.
- 🚀 O(n) solution, much better than naive O(n²).
- 🧠 Pattern: "trap water" = min(max_left, max_right) - height.
