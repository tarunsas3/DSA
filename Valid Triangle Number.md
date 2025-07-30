<h1 align="center">🔺 Valid Triangle Number</h1>

<p align="center">
  <a href="https://leetcode.com/problems/valid-triangle-number/">
    <img src="https://img.shields.io/badge/LeetCode-Valid%20Triangle%20Number-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Array%2C%20Two%20Pointers%2C%20Sorting-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To form a valid triangle with sides `a ≤ b ≤ c`, the triangle inequality must hold:  
**a + b > c**.  

If we **sort the array**, then for any fixed `c` (largest side), the pair `(a, b)` must satisfy `a + b > c`.  
This allows us to use a **two-pointer approach** to count all valid combinations efficiently.


## 💡 Approach

1. **Sort** the array.  
2. Iterate `k` from `len(nums)-1` down to `2` (choosing the largest side `c`).  
3. Use two pointers:
   - `i = 0` (start)
   - `j = k-1` (just before `k`)
4. While `i < j`:
   - If `nums[i] + nums[j] > nums[k]`:  
     - All pairs from `i` to `j` form valid triangles with `k`.  
     - Add `(j - i)` to count and move `j` left.  
   - Else, move `i` right.  
5. Return the total count.


## ❗ Edge Cases

- Array with fewer than 3 elements → Return `0`.  
- All zeros → No valid triangle.  
- Large values → Still works with sorting + two pointers.  


## 🔍 Example

```
Input: nums = [2, 2, 3, 4]
Output: 3
Explanation: Valid triangles are (2,3,4), (2,3,4), (2,2,3)
```

## 🧾 Code

```
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        nums.sort()
        count = 0
        n = len(nums)
        for k in range(n - 1, 1, -1):
            i, j = 0, k - 1
            while i < j:
                if nums[i] + nums[j] > nums[k]:
                    count += (j - i)
                    j -= 1
                else:
                    i += 1
        return count
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n²)   |
| 🗃️ Space    | O(n)   |

## 📌 Summary

- ✅ Sorting + Two Pointers avoids brute force O(n³).
- ✅ Efficient counting by grouping valid pairs at once.
- 💡 Common pattern for "sum constraints" problems.
