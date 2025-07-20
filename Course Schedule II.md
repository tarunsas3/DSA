<h1 align="center">📝 Course Schedule II</h1>

<p align="center">
  <a href="https://leetcode.com/problems/course-schedule-ii/">
    <img src="https://img.shields.io/badge/LeetCode-Course%20Schedule%20II-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Graph%2C%20Topological%20Sort%2C%20Cycle%20Detection-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

This is a follow-up to **Course Schedule I**.  
Instead of just checking if you can finish all courses, now we need to **return the actual order** in which you can take them.

This is a classic **topological sorting** problem on a **directed graph**.

## 💡 Approach

Use **Kahn’s Algorithm (BFS Topological Sort)**:

1. Build an **adjacency list** from the prerequisites.
2. Track the **indegree** of each course.
3. Add all courses with `indegree == 0` (no prerequisites) to a queue.
4. Process the queue:
   - Pop a course, add it to the result.
   - Reduce indegree of its neighbors.
   - If any neighbor's indegree becomes 0, add it to the queue.
5. If we processed all courses, return the result.  
   If a cycle exists (not all nodes processed), return an empty list.

## ❗ Edge Cases

- No prerequisites → return any order `[0, 1, 2, ...]`  
- Cycle in graph → return `[]`  
- Disconnected components → still valid if no cycles

## 🔍 Example

```
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]

Output: [0,1,2,3] or [0,2,1,3]

Explanation: Both are valid topological orderings.
```

## 🧾 Code (BFS - Kahn’s Algorithm)

```
from collections import defaultdict, deque

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        adj = defaultdict(list)
        indegree = [0] * numCourses

        for course, prereq in prerequisites:
            adj[prereq].append(course)
            indegree[course] += 1

        queue = deque([i for i in range(numCourses) if indegree[i] == 0])
        res = []

        while queue:
            curr = queue.popleft()
            res.append(curr)
            for neighbor in adj[curr]:
                indegree[neighbor] -= 1
                if indegree[neighbor] == 0:
                    queue.append(neighbor)

        return res if len(res) == numCourses else []
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(N + E)   |
| 🗃️ Space    | O(N + E)   |

- N = courses
- E = prerequisites

## 📌 Summary

- ✅ Topological sorting gives valid course order.
- 📥 Use indegrees to find courses with no remaining prerequisites.
- 🔁 Process and reduce dependency levels.
- ❌ Cycle → not all courses can be scheduled → return [].
