<h1 align="center">🏅 Kth Largest Element in an Array</h1>

<p align="center">
  <a href="https://leetcode.com/problems/kth-largest-element-in-an-array/">
    <img src="https://img.shields.io/badge/LeetCode-Kth%20Largest%20in%20an%20Array-orange?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Heap%2C%20Quickselect-blue?style=flat-square" />
</p>


## 🧠 Intuition

To find the `k`th largest element in an unsorted array:

- **Naive way**: Sort and return the `n - k`th index.
- **Optimized way**: Use a **min-heap** of size `k`.
- **Most optimal (in-place)**: Use **Quickselect** algorithm (average O(n)).


## 💡 Heap Approach

- Build a **min-heap** of size `k`.
- Traverse the array and maintain only the `k` largest elements in the heap.
- The root of the heap will be the `k`th largest.


## 🔍 Example

```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5

Input: nums = [1,1,1,1,1], k = 1
Output: 1
```

## 🧾 Code (Heap Approach)

```
import heapq

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        minHeap = []
        
        for num in nums:
            heapq.heappush(minHeap, num)
            if len(minHeap) > k:
                heapq.heappop(minHeap)
        
        return minHeap[0]
```

## 💡 Alternative: Quickselect (In-Place)

```
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        k = len(nums) - k  # kth largest is (n-k)th smallest
        
        def quickselect(l, r):
            pivot = nums[r]
            p = l
            
            for i in range(l, r):
                if nums[i] <= pivot:
                    nums[p], nums[i] = nums[i], nums[p]
                    p += 1
            
            nums[p], nums[r] = nums[r], nums[p]
            
            if p < k:
                return quickselect(p + 1, r)
            elif p > k:
                return quickselect(l, p - 1)
            else:
                return nums[p]
        
        return quickselect(0, len(nums) - 1)
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n log k)   |
| 🗃️ Space    | O(k)   |

## ✅ Summary

- Method	Time	Space	Notes
- Sorting	O(n log n)	O(1)	Simple but not optimal
- Min-Heap (k)	O(n log k)	O(k)	Efficient for small k
- Quickselect	O(n) avg	O(1)	Best for interviews / in-place
