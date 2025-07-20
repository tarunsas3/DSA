<h1 align="center">📚 Course Schedule</h1>

<p align="center">
  <a href="https://leetcode.com/problems/course-schedule/">
    <img src="https://img.shields.io/badge/LeetCode-Course%20Schedule-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Graph%2C%20Topological%20Sort%2C%20Cycle%20Detection-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We are asked whether it's possible to complete all courses given some prerequisites.  
This is equivalent to checking if a **directed graph** has a **cycle** — if it does, we can't finish all courses.

## 💡 Approach

Use **topological sort** via either:
- **DFS with cycle detection**, or  
- **BFS using Kahn's Algorithm (indegree-based)**

We’ll use the **DFS approach** here.

1. Build an **adjacency list** to represent course dependencies.
2. Use a `visited` array:
   - `0` = unvisited  
   - `1` = visiting  
   - `2` = visited  
3. During DFS:
   - If we reach a node that is currently being visited (`1`), a **cycle** exists → return False.
   - After visiting all children, mark the node as fully visited (`2`).
4. If no cycles are found, return True.

## ❗ Edge Cases

- No prerequisites → always return `True`  
- Circular dependency → return `False`  
- Empty course list → return `True`  

## 🔍 Example

```
Input: numCourses = 4, prerequisites = [[1,0],[2,1],[3,2]]
Output: True

Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: False (cycle: 0 → 1 → 0)
```

## 🧾 Code (DFS)

```
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        adj = {i: [] for i in range(numCourses)}
        for course, prereq in prerequisites:
            adj[course].append(prereq)

        visited = [0] * numCourses  # 0=unvisited, 1=visiting, 2=visited

        def dfs(course):
            if visited[course] == 1:
                return False  # cycle detected
            if visited[course] == 2:
                return True

            visited[course] = 1  # mark as visiting
            for neighbor in adj[course]:
                if not dfs(neighbor):
                    return False
            visited[course] = 2  # mark as fully visited
            return True

        for course in range(numCourses):
            if not dfs(course):
                return False

        return True
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(N + E)   |
| 🗃️ Space    | O(N + E)   |

- N = courses
- E = prerequisites

## 📌 Summary

- 🔁 Topological sort helps validate if course scheduling is possible.
- ⚠️ Cycle detection is key — cycles mean deadlocks in prerequisites.
- 🧠 DFS approach with visited states elegantly detects cycles.
- 📘 A foundational problem in graph theory with real-world implications.
