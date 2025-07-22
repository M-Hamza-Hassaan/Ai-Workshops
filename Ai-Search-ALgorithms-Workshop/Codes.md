# 🧠 AI Search Algorithms Workshop

Here **Uninformed**, **Informed**, and **Adversarial** search algorithms, explained with code.

---

### 🔍 1. Breadth-First Search (BFS)
**Type**: Uninformed Search  
**Best for**: Finding the shortest path in unweighted graphs

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])

    while queue:
        node = queue.popleft()
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            queue.extend(neighbor for neighbor in graph[node] if neighbor not in visited)
# First, explores all nodes at the current depth before moving to the next.
```


### 🌲 2. Depth-First Search (DFS)
**Type**: Uninformed Search
**Best** for: Exploring all paths, can go deep quickly

```python
def dfs(graph, node, visited=None):
    if visited is None:
        visited = set()
    if node not in visited:
        print(node, end=" ")
        visited.add(node)
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited)
# Uses recursion (or a stack) to dive deep into the graph/tree.
```


### 🎯 3. Greedy Best First Search (GBFS)
**Type**: Informed Search
**Best** for: Fast but not always optimal

```python
import heapq

def greedy_bfs(graph, start, goal, heuristic):
    open_list = [(heuristic[start], start)]
    visited = set()

    while open_list:
        _, current = heapq.heappop(open_list)
        if current == goal:
            return True
        if current not in visited:
            visited.add(current)
            for neighbor in graph[current]:
                if neighbor not in visited:
                    heapq.heappush(open_list, (heuristic[neighbor], neighbor))
    return False
# Selects the next node based on the lowest heuristic value (greedy choice).
```


### ⭐ 4. A* Search Algorithm
**Type**: Informed Search
**Best** for: Optimal pathfinding in weighted graphs

```python
import heapq

def a_star(graph, start, goal, heuristic):
    open_list = [(0 + heuristic[start], 0, start)]
    visited = set()

    while open_list:
        est_cost, cost, current = heapq.heappop(open_list)
        if current == goal:
            return True
        if current not in visited:
            visited.add(current)
            for neighbor, weight in graph[current]:
                if neighbor not in visited:
                    new_cost = cost + weight
                    priority = new_cost + heuristic[neighbor]
                    heapq.heappush(open_list, (priority, new_cost, neighbor))
    return False
# Combines actual cost (g(n)) + heuristic (h(n)) for balanced, optimal search.
```


### 🎮 5. Minimax Algorithm
**Type**: Adversarial Search
**Best** for: Two-player games (Tic Tac Toe, Chess)

```python
def minimax(depth, node_index, is_max, values, target_depth):
    if depth == target_depth:
        return values[node_index]

    if is_max:
        return max(
            minimax(depth + 1, node_index * 2, False, values, target_depth),
            minimax(depth + 1, node_index * 2 + 1, False, values, target_depth)
        )
    else:
        return min(
            minimax(depth + 1, node_index * 2, True, values, target_depth),
            minimax(depth + 1, node_index * 2 + 1, True, values, target_depth)
        )
# Simulates both players trying to maximize/minimize the outcome.
```


### ⚡ 6. Alpha-Beta Pruning
**Type**: Adversarial Search (Optimized Minimax)
**Best** for: Reducing unnecessary calculations in games

```python
def alphabeta(depth, node_index, is_max, values, alpha, beta, target_depth):
    if depth == target_depth:
        return values[node_index]

    if is_max:
        max_eval = float('-inf')
        for i in range(2):
            eval = alphabeta(depth + 1, node_index * 2 + i, False, values, alpha, beta, target_depth)
            max_eval = max(max_eval, eval)
            alpha = max(alpha, eval)
            if beta <= alpha:
                break
        return max_eval
    else:
        min_eval = float('inf')
        for i in range(2):
            eval = alphabeta(depth + 1, node_index * 2 + i, True, values, alpha, beta, target_depth)
            min_eval = min(min_eval, eval)
            beta = min(beta, eval)
            if beta <= alpha:
                break
        return min_eval
#Improves efficiency by cutting branches that don’t affect the result.
```


📌 Use Cases
Algorithm	Use Case

BFS / DFS	Web crawling, puzzle solvers

A* / Greedy BFS	Maps, GPS routing, robot pathfinding

Minimax / Alpha-Beta	Chess, Tic Tac Toe, Game AI


🙋‍♂️ Instructor: M. Hamza Hassaan
💬 damn.code.hamza@gmail.com
🌐 LinkedIn

⭐ Star this repo if you'd like more workshops like this!