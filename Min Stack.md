<h1 align="center">✅ Min Stack</h1>

<p align="center">
  <a href="https://leetcode.com/problems/min-stack/">
    <img src="https://img.shields.io/badge/LeetCode-Min%20Stack-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Stack%2C%20Design-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

A normal stack gives us **O(1)** for push and pop.  
But how can we get the **minimum element in constant time** too?

We need a way to **track the minimum element at each point** in the stack without scanning the whole thing.


## 💡 Approach

1. Use a **custom node** that stores both the value and the **current minimum** when that value was pushed.
2. Maintain a single stack (or use a linked structure).
3. On `push`, compare the new value with the current minimum and store the smaller one.
4. On `getMin`, just return the top node’s `min` value.


## ❗ Edge Cases

- All elements are increasing/decreasing
- Stack with duplicate values
- Empty stack operations (invalid by constraint but good to consider)


## 🔍 Example

```
minStack = MinStack()
minStack.push(-2)
minStack.push(0)
minStack.push(-3)
minStack.getMin()    # ➞ -3
minStack.pop()
minStack.top()       # ➞ 0
minStack.getMin()    # ➞ -2
```

## 🧾 Code

```
class Node:

    def __init__(self, val: int, min_val: int):
        self.val = val
        self.min_val = min_val
        self.next = None

class MinStack:

    def __init__(self):
        self.head = None

    def push(self, val: int) -> None:
        if not self.head:
            min_val = val
        else:
            min_val = min(val, self.head.min_val)
        newNode = Node(val, min_val)
        if not self.head:
            self.head = newNode
        else:
            newNode.next = self.head
            self.head = newNode

    def pop(self) -> None:
        self.head = self.head.next

    def top(self) -> int:
        return self.head.val

    def getMin(self) -> int:
        return self.head.min_val
```


## 📈 Time and Space Complexity

| Operation   | Time Complexity | Space Complexity |
|-------------|------------------|------------------|
| `push`      | O(1)             | O(1)             |
| `pop`       | O(1)             | O(1)             |
| `top`       | O(1)             | O(1)             |
| `getMin`    | O(1)             | O(1)             |
| Total Space | —                | O(n)             |


# 📌 Summary

- ✅ Stack stores both value and current minimum
- ✅ All operations remain constant time
- 💡 Great example of stack with auxiliary data
- 🔁 Pattern generalizes to:
  - Max Stack
  - Stack with median/tracking aggregates
