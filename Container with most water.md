<h1 align="center">✅ Container With Most Water</h1>

<p align="center">
  <a href="https://leetcode.com/problems/container-with-most-water/">
    <img src="https://img.shields.io/badge/LeetCode-Container%20With%20Most%20Water-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Two%20Pointers%2C%20Greedy%2C%20Array-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To find the maximum area between two lines in the array:
- The area is determined by the **shorter** of the two lines and the **distance** between them.
- To maximize area, we need to move pointers smartly rather than checking every pair (brute force would be O(n²)).


## 💡 Approach

1. Use two pointers:
   - One starting at the beginning (`left`)
   - One at the end (`right`)
2. Calculate the area = `min(height[left], height[right]) * (right - left)`
3. Track the maximum area seen so far.
4. Move the pointer pointing to the **shorter** line inward (this may give a taller line and potentially a larger area).
5. Repeat until `left < right`


## ❗ Edge Cases

- All heights are the same → largest width gives max area.
- Very tall lines close together may give less area than moderate lines far apart.
- Array of size 2 → area is just `min(height[0], height[1]) * 1`


## 🔍 Example

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation:
- Max area is between lines at index 1 and 8 → min(8,7) * (8 - 1) = 7 * 7 = 49
```

##🧾 Code

```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height) - 1
        max_area = 0

        while left < right:
            h = min(height[left], height[right])
            w = right - left
            max_area = max(max_area, h * w)

            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return max_area
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |

Only two pointers and constant variables used

## 📌 Summary

- ✅ Uses the two pointers technique to optimize area checking.
- ✅ Avoids brute force by greedily moving the shorter line.
- 💡 Demonstrates how to combine geometry with array traversal efficiently.
- 🔁 Pattern often reused in "max difference" or "distance under constraint" problems.
