<h1 align="center">🕸️ Articulation Point - II 🕸️</h1>

---

## 📝 Problem Statement
You are given an **undirected graph** with `V` vertices and `E` edges, represented by a 2D array `edges[][]`, where each element `edges[i] = [u, v]` indicates an edge between vertices `u` and `v`.

Your task is to return all the **articulation points** (or cut vertices) in the graph.  
📌 An **articulation point** is a vertex whose removal (along with its edges) increases the number of connected components in the graph.

- If no such vertex exists, return `{-1}`.
- The graph may be disconnected.

---


## ✅ Examples

### ✅ Example 1:

**Input:**  
```
V = 5
edges = [[0, 1], [1, 4], [4, 3], [4, 2], [2, 3]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/892595/Web/Other/blobid3_1744109134.png"> </img>

**Output:**
```
[1, 4]
```

**Explanation:**  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/892595/Web/Other/blobid4_1744109133.png"> </img>
<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/892595/Web/Other/blobid5_1744109133.png"> </img>

- Removing vertex `1` disconnects the graph.  
- Removing vertex `4` also disconnects the graph.  
Thus, articulation points = `[1, 4]`.

---


### ✅ Example 2:

**Input:**
```
V = 3
edges = [[0, 1], [0, 2]]
```

**Output:**
```
[0]
```

**Explanation:**  
Removing vertex `0` disconnects the graph into three components.  
Hence, `0` is an articulation point.

---

## 🧠 Approach
We use **Tarjan’s Algorithm** (DFS-based) to find articulation points:

1. Maintain two arrays:
   - `disc[i]`: Discovery time of vertex `i` during DFS.  
   - `low[i]`: The lowest discovery time reachable from vertex `i`.
2. For each unvisited vertex, perform DFS:
   - Track the number of children of each node in DFS tree.  
   - If the root has more than 1 child → it is an articulation point.  
   - For non-root nodes: If `low[child] >= disc[parent]`, then `parent` is an articulation point.
3. Collect all articulation points. If none are found, return `{-1}`.

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(V + E) | DFS visits each vertex and edge once |
| Space      | O(V + E) | Adjacency list, recursion stack, and helper arrays |

---

## 🎯 Constraints
- 1 ≤ `V`, `E` ≤ 10⁴  

---

## 💻 Code
```java
class Solution {
    static void dfs(int i, int prev, List<Integer>[] adj, int[] disc, int[] low, boolean[] visited, boolean[] ap, int[] time){
        visited[i] = true;
        ++time[0];
        disc[i] = time[0];
        low[i] = time[0];
        int count = 0;
        for(int j: adj[i]){
            if(!visited[j]){
                count++;
                dfs(j, i, adj, disc, low, visited, ap, time);
                low[i] = Math.min(low[i], low[j]);
                if(prev != -1 && low[j] >= disc[i]){
                    ap[i] = true;
                } 
            } else if(j != prev){
                low[i] = Math.min(low[i], disc[j]);
            }
        }
        if(prev == -1 && count > 1){
            ap[i] = true;
        }
    }
    static ArrayList<Integer> articulationPoints(int V, int[][] edges) {
        List<Integer>[] adj = new ArrayList[V];
        ArrayList<Integer> ans = new ArrayList<>();
        for(int i = 0; i < V; i++){
            adj[i] = new ArrayList<>();
        }
        for(int[] i: edges){
            adj[i[0]].add(i[1]);
            adj[i[1]].add(i[0]);
        }
        boolean[] visited = new boolean[V], ap = new boolean[V];
        int[] disc = new int[V], low = new int[V], time = {0};
        for(int i = 0; i < V; i++){
            if(!visited[i]){
                dfs(i, -1, adj, disc, low, visited, ap, time);
            }
        }
        for(int i = 0; i < V; i++){
            if(ap[i]){
                ans.add(i);
            }
        }
        if(ans.isEmpty()){
            ans.add(-1);
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. **Graph Representation**
- The graph is stored in an adjacency list.
- Each vertex keeps track of its neighbors.
2. **DFS Traversal**
- We start DFS from each unvisited vertex.
- Each node gets a discovery time when first visited.
- Each node also keeps a `low` value → the earliest discovered ancestor reachable from its subtree.
3. **Updating Low Values**
- When DFS goes deeper, each child tries to connect back (via back edges).
- If no back edge exists, removing the parent disconnects that child’s subtree → parent is an articulation point.
4. **Root Special Case**
- If the root has more than 1 child, removing it disconnects the graph.
5. **Marking Articulation Points**
- `ap[u] = true` if `u` is found to be an articulation point.
- Finally, we collect all such vertices.

---

> Made with ❤️ by Milan Haria
