<h1 align="center">✅ Product of Array Except Self</h1>

<p align="center">
  <a href="https://leetcode.com/problems/product-of-array-except-self/">
    <img src="https://img.shields.io/badge/LeetCode-Product%20of%20Array%20Except%20Self-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Array%2C%20Prefix%20Product%2C%20Suffix%20Product-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To compute the product of all elements **except the current one** without using division, we can:
- First calculate **prefix products** (left of each index)
- Then calculate **suffix products** (right of each index)
- Multiply them together to get the result

This ensures each element's product excludes itself, while avoiding the division operation entirely.


## 💡 Approach

1. Create a `result` array initialized to 1.
2. Traverse from left to right:
   - For each index `i`, set `result[i] *= left_product`
   - Update `left_product *= nums[i]`
3. Traverse from right to left:
   - For each index `i`, set `result[i] *= right_product`
   - Update `right_product *= nums[i]`
4. Return `result`


## ❗ Edge Cases

- Input contains `0`: all products except for the zero-index become 0  
- Negative numbers: the sign is handled automatically by multiplication  
- `[0, 0]` → entire output is `[0, 0]`  
- Length 2 arrays → simply reverse the pair


## 🔍 Example

```
Input:  nums = [1, 2, 4, 6]
Output: [48, 24, 12, 8]
```

Explanation:
- For index 0 → 2×4×6 = 48
- For index 1 → 1×4×6 = 24
- For index 2 → 1×2×6 = 12
- For index 3 → 1×2×4 = 8

## 🧾 Code

```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        result = [1] * len(nums)

        leftProd = 1
        for i in range(len(nums)):
            result[i] *= leftProd
            leftProd *= nums[i]

        rightProd = 1
        for i in range(len(nums) - 1, -1, -1):
            result[i] *= rightProd
            rightProd *= nums[i]

        return result
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |


## 📌 Summary

- ✅ Optimized for both time and space — no division used.
- ✅ Perfect example of the prefix/suffix product pattern.
- 🔁 Common follow-up is to reduce space usage to constant (excluding output).
- 💡 Very popular in interviews and a great test of array manipulation skills.
