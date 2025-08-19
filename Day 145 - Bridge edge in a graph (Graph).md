<h1 align="center">🌉 Bridge Edge in a Graph 🌉</h1>

---

## 📝 Problem Statement
You are given an **undirected graph** with `V` vertices (0 to V-1) and `E` edges.  
Each edge is represented as `edges[i] = [u, v]`.  

Your task is to determine if a specific edge `(c, d)` is a **bridge**.  

📌 **Definition:**  
An edge is called a **bridge** if removing it increases the number of connected components in the graph.  
In other words, if `(c, d)` is the **only path** between vertices `c` and `d`, then it is a bridge.

---


## ✅ Examples

### ✅ Example 1:

**Input:**  
```
V = 4
edges = [[0, 1], [1, 2], [2, 3]]
c = 1, d = 2
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700463/Web/Other/blobid1_1744198886.jpg"> </img>

**Output:**
```
true
```

**Explanation:**  
Removing edge `(1, 2)` disconnects the graph into two parts → it is a bridge.

---


### ✅ Example 2:

**Input:**
```
V = 5
edges = [[0, 1], [0, 3], [1, 2], [2, 0], [3, 4]]
c = 0, d = 2
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700463/Web/Other/blobid2_1744199181.jpg"> </img>

**Output:**
```
false
```

**Explanation:**  
Even after removing `(0, 2)`, there still exists another path between `0` and `2` through `(0 → 1 → 2)`.  
Hence, `(0, 2)` is **not** a bridge.

---

## 🧠 Approach
1. **Build adjacency list** of the graph while skipping the given edge `(c, d)`.  
2. **DFS Traversal**:
   - Start DFS from node `c`.  
   - If we cannot reach `d` without edge `(c, d)`, then `(c, d)` is a **bridge**.  
3. If `d` is still reachable, then the edge is **not** a bridge.  

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(V + E) | DFS traversal visits each vertex and edge once |
| Space      | O(V + E) | Adjacency list + visited array |

---

## 🎯 Constraints
- 1 ≤ `V`, `E` ≤ 10⁵  
- 0 ≤ `c`, `d` ≤ V-1  

---

## 💻 Code
```java
class Solution {
    public void dfs(List<List<Integer>> adj, boolean[] visited, int c){
        visited[c] = true;
        for(int i: adj.get(c)){
            if(!visited[i]){
                dfs(adj, visited, i);
            }
        }
    }
    public boolean isBridge(int V, int[][] edges, int c, int d) {
        List<List<Integer>> adj = new ArrayList<>();
        boolean[] visited = new boolean[V];
        for(int i = 0; i < V; i++){
            adj.add(new ArrayList<>());
        }
        for(int[] i: edges){
            if(!((i[0] == c && i[1] == d) || (i[0] == d && i[1] == c))){
                adj.get(i[0]).add(i[1]);
                adj.get(i[1]).add(i[0]);
            }
        }
        dfs(adj, visited, c);
        return !visited[d];
    }
}
```

---

## 📝 Explanation of Code

- **Step 1**: Build adjacency list excluding the given edge `(c, d)`.
- **Step 2**: Run DFS from `c`.
- **Step 3**: If after DFS, `visited[d] == false`, then removing `(c, d)` disconnects the graph → Bridge.
- Otherwise, `(c, d)` is **not a bridge**.

---

> Made with ❤️ by Milan Haria
