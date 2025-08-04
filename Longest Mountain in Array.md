<h1 align="center">⛰️ Longest Mountain in Array</h1>

<p align="center">
  <a href="https://leetcode.com/problems/longest-mountain-in-array/">
    <img src="https://img.shields.io/badge/LeetCode-Longest%20Mountain%20in%20Array-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Two%20Pointers%2C%20Array-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

A **mountain** is a subarray where:
- It **strictly increases**, reaches a **peak**, then **strictly decreases**.
- Length ≥ 3.

We need the **longest** such mountain.

The idea:
- Traverse the array and **detect peaks** (`arr[i-1] < arr[i] > arr[i+1]`).
- For each peak, **expand left** (while strictly increasing) and **expand right** (while strictly decreasing) to get the full mountain length.
- Track the maximum length.

## 💡 Approach

1. Initialize `max_len = 0`.  
2. Iterate from index `1` to `n-2`:
   - If `arr[i-1] < arr[i] > arr[i+1]`:
     - Set `left = i-1` and expand left while `arr[left-1] < arr[left]`.  
     - Set `right = i+1` and expand right while `arr[right] > arr[right+1]`.  
     - Update `max_len = max(max_len, right - left + 1)`.  
     - Skip to `right` to avoid reprocessing.  
3. Return `max_len`.

## ❗ Edge Cases

- Array length < 3 → no mountain.  
- Flat regions (no strict increase/decrease).  
- Multiple small mountains — only take the longest.  

## 🔍 Example

```
Input: arr = [2,1,4,7,3,2,5]
Output: 5
Explanation: The mountain is [1,4,7,3,2] with length 5.
```

## 🧾 Code

```
class Solution:
    def longestMountain(self, arr: List[int]) -> int:
        n = len(arr)
        max_len = 0
        i = 1
        
        while i < n - 1:
            # Check for peak
            if arr[i-1] < arr[i] > arr[i+1]:
                left = i - 1
                right = i + 1
                
                # Expand left
                while left > 0 and arr[left-1] < arr[left]:
                    left -= 1
                
                # Expand right
                while right < n - 1 and arr[right] > arr[right+1]:
                    right += 1
                
                max_len = max(max_len, right - left + 1)
                i = right  # Skip processed part
            else:
                i += 1
        
        return max_len
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(1)   |


## 📌 Summary

- ✅ Detect peaks, then expand outward for mountain length.
- 🚀 O(n) one-pass solution (skipping processed mountains).
- 🧠 Classic two-pointer expansion pattern.
