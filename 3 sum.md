<h1 align="center">✅ 3Sum</h1>

<p align="center">
  <a href="https://leetcode.com/problems/3sum/">
    <img src="https://img.shields.io/badge/LeetCode-3Sum-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Two%20Pointers%2C%20Sorting%2C%20Array-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

We are looking for **three numbers that sum to zero**.  
A brute-force approach would take `O(n³)` time, which is too slow.  
We can reduce this to `O(n²)` using the **two-pointer technique** after **sorting** the array.


## 💡 Approach

1. **Sort** the array first.
2. Loop through each element `nums[i]`:
   - Skip duplicates to avoid repeated triplets.
   - Set up two pointers:
     - `left = i + 1`
     - `right = len(nums) - 1`
   - While `left < right`:
     - Calculate the current sum = `nums[i] + nums[left] + nums[right]`
     - If sum is zero → save triplet, skip duplicates, move both pointers.
     - If sum < 0 → increment `left`
     - If sum > 0 → decrement `right`


## ❗ Edge Cases

- Multiple duplicate values → avoid repeating triplets
- Fewer than 3 elements → return empty list
- All zeros → return one `[0, 0, 0]`


## 🔍 Example

```
Input: nums = [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]
Explanation:
- The two unique triplets that sum to 0 are: [-1,-1,2] and [-1,0,1]
```

## 🧾 Code

```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = []

        for i in range(len(nums) - 2):
            if i > 0 and nums[i] == nums[i - 1]:
                continue  # Skip duplicates for the first element

            left, right = i + 1, len(nums) - 1

            while left < right:
                total = nums[i] + nums[left] + nums[right]
                if total == 0:
                    res.append([nums[i], nums[left], nums[right]])
                    left += 1
                    right -= 1
                    while left < right and nums[left] == nums[left - 1]:
                        left += 1  # Skip duplicates
                    while left < right and nums[right] == nums[right + 1]:
                        right -= 1
                elif total < 0:
                    left += 1
                else:
                    right -= 1

        return res
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n²)   |
| 🗃️ Space    | O(n)   |

- Sorting takes O(n log n)
- For each element, we do a two-pointer scan → O(n²) total
- Result list grows based on unique triplets

## 📌 Summary

- ✅ Combines sorting and two-pointers to solve efficiently
- ✅ Avoids duplicates with careful checks
- 💡 Classic example of reducing complexity with sorted input
- 🔁 Template extends to 4Sum, kSum, and similar problems
