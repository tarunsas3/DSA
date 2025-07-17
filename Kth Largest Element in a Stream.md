<h1 align="center">📶 Kth Largest Element in a Stream</h1>

<p align="center">
  <a href="https://leetcode.com/problems/kth-largest-element-in-a-stream/">
    <img src="https://img.shields.io/badge/LeetCode-Kth%20Largest%20in%20a%20Stream-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Heap%2C%20Priority%20Queue-blue?style=flat-square" />
</p>


## 🧠 Intuition

To efficiently keep track of the `k` largest elements from a stream of numbers, we can use a **min-heap of size `k`**.

- The smallest among the top `k` largest elements will always be at the top of the heap.
- When a new number comes in:
  - If the heap has fewer than `k` elements → add it.
  - If the new number is larger than the smallest in the heap → replace it.

The root of the heap always gives the **`k`th largest element**.


## 💡 Approach

- Use `heapq` (Python's min-heap).
- Maintain a heap of size `k` with the largest `k` elements seen so far.
- `add(val)` pushes a new number into the stream and adjusts the heap.


## 🔍 Example

```
Input: 
k = 3, nums = [4, 5, 8, 2]
KthLargest.add(3)   → returns 4
KthLargest.add(5)   → returns 5
KthLargest.add(10)  → returns 5
KthLargest.add(9)   → returns 8
KthLargest.add(4)   → returns 8
```

## 🧾 Code

```
import heapq

class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        self.minHeap = nums
        self.k = k
        heapq.heapify(self.minHeap)
        
        while len(self.minHeap) > k:
            heapq.heappop(self.minHeap)

    def add(self, val: int) -> int:
        heapq.heappush(self.minHeap, val)
        
        if len(self.minHeap) > self.k:
            heapq.heappop(self.minHeap)
        
        return self.minHeap[0]
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n log k)   |
| 🗃️ Space    | O(k)   |

- Efficient for large streams where only k top elements are of interest.

## ✅ Summary

- Maintains top k largest values using a min-heap.
- Returns kth largest in O(log k) per update.
- Ideal for streaming data problems.
