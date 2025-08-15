<h1 align="center">🔄 Undirected Graph Cycle 🔄</h1>

---

## 📝 Problem Statement
You are given an **undirected graph** with `V` vertices and `E` edges represented as a 2D array `edges[][]`.  
Each `edges[i] = [u, v]` denotes an edge between vertices `u` and `v`.  

Your task is to determine whether the graph contains a **cycle** or not.  
The graph can have multiple components.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
V = 4, E = 4
edges = [[0, 1], [0, 2], [1, 2], [2, 3]]
```

**Output:**
```
true
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/891735/Web/Other/blobid1_1743510240.jpg"> </img>

Cycle exists: `0 → 1 → 2 → 0`.

---


### ✅ Example 2:

**Input:**
```
V = 4, E = 3
edges = [[0, 1], [1, 2], [2, 3]]
```

**Output:**
```
false
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/891735/Web/Other/blobid2_1743510254.jpg"> </img>

Graph is a straight chain, so no cycle exists.

---

## 🧠 Approach
We use **BFS (Breadth First Search)** with **parent tracking**:
1. Convert edges into an **adjacency list**.
2. For each unvisited node, run BFS:
   - Keep track of `(node, parent)` in queue.
   - If a visited neighbor is found that is **not the parent**, a cycle exists.
3. If no such condition is found, return `false`.

This works for **all components** of the graph.

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(V + E) | Traverse all vertices and edges once |
| Space      | O(V + E) | Adjacency list and visited array |

---

## 🎯 Constraints
- 1 ≤ `V` ≤ 10⁵  
- 1 ≤ `E` ≤ 10⁵  

---

## 💻 Code
```java
class Solution {
    public boolean cycle(int beg, List<List<Integer>> adj, boolean[] visited){
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{ beg, -1 });
        visited[beg] = true;
        while(!queue.isEmpty()){
            int[] a = queue.poll();
            int node = a[0], prev = a[1];
            for(int i: adj.get(node)){
                if(!visited[i]){
                    visited[i] = true;
                    queue.offer(new int[]{ i, node });
                } else if(i != prev){
                    return true;
                }
            }
        }
        return false;
    }
    public boolean isCycle(int V, int[][] edges) {
        boolean[] visited = new boolean[V];
        List<List<Integer>> adj = new ArrayList<>();
        for(int i = 0; i < V; i++){
            adj.add(new ArrayList<>());
        }
        for(int[] i: edges){
            adj.get(i[0]).add(i[1]);
            adj.get(i[1]).add(i[0]);
        }
        for(int i = 0; i < V; i++){
            if(!visited[i]){
                if(cycle(i, adj, visited)){
                    return true;
                }
            }
        }
        return false;
    }
}
```

---

## 📝 Explanation of Code

- **`cycle()`** → BFS helper that checks if a cycle exists in a connected component.
- **`isCycle()`** → Builds adjacency list and checks all components.
- If a visited neighbor is found that is **not the parent**, a cycle exists.

---

> Made with ❤️ by Milan Haria
