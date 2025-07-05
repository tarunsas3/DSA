<h1 align="center">✅ Valid Parentheses</h1>

<p align="center">
  <a href="https://leetcode.com/problems/valid-parentheses/">
    <img src="https://img.shields.io/badge/LeetCode-Valid%20Parentheses-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Easy-green?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Stack%2C%20String-blueviolet?style=flat-square" />
</p>


## 🧠 Intuition

To check if a sequence of parentheses is **valid**, we need to ensure:
- Every opening bracket has a matching closing bracket in the correct order.
- Use a **stack** to track the order of unmatched opening brackets.


## 💡 Approach

1. Create a mapping of opening → closing brackets.
2. Initialize an empty `stack`.
3. Traverse the string:
   - If character is an **opening bracket**, push the expected closing bracket onto the stack.
   - If character is a **closing bracket**, check if it matches the top of the stack.
     - If not, return `False`.
4. After traversal, return `True` if the stack is empty (all brackets matched).


## ❗ Edge Cases

- Empty string → valid
- Single unmatched bracket → invalid
- More closings than openings (or vice versa) → invalid


## 🔍 Example

```
Input: s = "()[]{}"
Output: True
```

```
Input: s = "([)]"
Output: False
```

```
Input: s = "{[]}"
Output: True
```

## 🧾 Code

```
class Solution:
    def isValid(self, s: str) -> bool:
        brackets = {'(': ')', '[': ']', '{': '}'}
        stack = []

        for char in s:
            if char in brackets:
                stack.append(brackets[char])
            else:
                if not stack or stack.pop() != char:
                    return False

        return not stack
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(n)   |
| 🗃️ Space    | O(n)   |


Worst-case all characters are opening brackets → stack size grows to n

## 📌 Summary

- ✅ Classic stack problem for balanced bracket matching
- ✅ Clean logic using expected closings simplifies implementation
- 💡 Foundational for problems involving nested structures and parsing
- 🔁 Related problems:
   - Minimum Add to Make Parentheses Valid
   - Remove Invalid Parentheses
