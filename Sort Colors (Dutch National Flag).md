<h1 align="center">🎨 Sort Colors (Dutch National Flag)</h1>

<p align="center">
  <a href="https://leetcode.com/problems/sort-colors/">
    <img src="https://img.shields.io/badge/LeetCode-Sort%20Colors-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Array%2C%20Two%20Pointers%2C%20Sorting-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We are given an array of `0s`, `1s`, and `2s` representing colors.  
The goal is to **sort them in-place** without using built-in sort.  

This is a classic **Dutch National Flag** problem:
- `0` → Red (left)
- `1` → White (middle)
- `2` → Blue (right)  

We can use **three pointers** to arrange the values in a single pass.


## 💡 Approach

1. Use three pointers:
   - `low` → Position where next `0` should go.
   - `mid` → Current element being processed.
   - `high` → Position where next `2` should go.
2. Loop while `mid <= high`:
   - If `nums[mid] == 0`: Swap with `nums[low]`, move both `low` & `mid` forward.
   - If `nums[mid] == 1`: Just move `mid` forward.
   - If `nums[mid] == 2`: Swap with `nums[high]` and move `high` backward.
3. Continue until all numbers are sorted in-place.


## ❗ Edge Cases

- Already sorted array → Should handle without extra swaps.  
- Reverse sorted array → Should rearrange correctly in one pass.  
- Single-element or empty array → Works trivially.  


## 🔍 Example

```
Input: nums = [2, 0, 2, 1, 1, 0]
Output: [0, 0, 1, 1, 2, 2]
Explanation: Colors sorted in order 0 → 1 → 2.
```

## 🧾 Code

```
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        low, mid, high = 0, 0, len(nums) - 1
        while mid <= high:
            if nums[mid] == 0:
                nums[low], nums[mid] = nums[mid], nums[low]
                low += 1
                mid += 1
            elif nums[mid] == 1:
                mid += 1
            else:  # nums[mid] == 2
                nums[mid], nums[high] = nums[high], nums[mid]
                high -= 1
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |


## 📌 Summary

- ✅ Single-pass, in-place solution (no extra space).
- ✅ Three-pointer technique → Very efficient.
- 💡 Pattern often used in partitioning problems.
