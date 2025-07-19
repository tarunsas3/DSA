<h1 align="center">🧬 Clone Graph</h1>

<p align="center">
  <a href="https://leetcode.com/problems/clone-graph/">
    <img src="https://img.shields.io/badge/LeetCode-Clone%20Graph-brightgreen?logo=leetcode&style=flat-square" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Medium-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Category-Graph%2C%20DFS%2C%20BFS%2C%20HashMap-blueviolet?style=flat-square" />
</p>

## 🧠 Intuition

We need to **create a deep copy** of a connected undirected graph.  
Each node should be cloned exactly once, and its neighbors should also be properly connected in the new graph.

This is a classic use case for **DFS or BFS with a hashmap** to track already-cloned nodes.

## 💡 Approach

1. Use a **dictionary (`visited`)** to store cloned nodes (key: original node, value: clone).
2. Traverse the graph (DFS or BFS).
3. For each node:
   - If already cloned, return the clone from the map.
   - Else, create a clone and recursively clone all its neighbors.
4. Return the clone of the starting node.

## ❗ Edge Cases

- Empty graph (`node = None`) → return `None`  
- Single node with no neighbors  
- Graph with cycles → ensure no infinite recursion by using `visited` map

## 🔍 Example

```
Input:
  1 -- 2
  |    |
  4 -- 3

Output:

A deep clone with the same structure.
```

## 🧾 Code (DFS)

```
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []

class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        if not node:
            return None

        visited = {}

        def dfs(curr):
            if curr in visited:
                return visited[curr]

            clone = Node(curr.val)
            visited[curr] = clone

            for neighbor in curr.neighbors:
                clone.neighbors.append(dfs(neighbor))

            return clone

        return dfs(node)
```

## 📈 Time and Space Complexity

| Complexity | Value |
|------------|--------|
| 🕒 Time     | O(N + E)   |
| 🗃️ Space    | O(N)   |

- N = number of nodes
- E = number of edges

## 📌 Summary

- ✅ Use a hashmap to avoid revisiting/cloning the same node.
- 🔄 DFS (or BFS) to traverse all connected nodes.
- 💥 Be careful with cycles to avoid infinite loops.
- 🔗 Great example of cloning graphs using recursion or queues.
