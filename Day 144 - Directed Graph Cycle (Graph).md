<h1 align="center">🔁 Directed Graph Cycle 🔁</h1>

---

## 📝 Problem Statement
You are given a **Directed Graph** with `V` vertices (0 to V-1) and `E` edges.  
Each edge is represented as `edges[i] = [u, v]` meaning there is a directed edge from `u → v`.  

Your task is to determine **whether the graph contains a cycle or not**.

---


## ✅ Examples

### ✅ Example 1:

**Input:**  
```
V = 4
edges = [[0, 1], [0, 2], [1, 2], [2, 0], [2, 3]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700218/Web/Other/blobid0_1744197297.jpg"> </img>

**Output:**
```
true
```

**Explanation:**  
The graph contains a cycle: `0 → 2 → 0`.

---


### ✅ Example 2:

**Input:**
```
V = 4
edges = [[0, 1], [0, 2], [1, 2], [2, 3]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700218/Web/Other/blobid1_1744197327.jpg"> </img>

**Output:**
```
false
```

**Explanation:**  
There is no cycle in the graph.

---

## 🧠 Approach 

### Kahn’s Algorithm – Topological Sort
1. **Build adjacency list** and compute **in-degree** of each vertex.  
2. Add all vertices with `inDegree = 0` into a **queue**.  
3. Perform a BFS-like traversal:
   - Remove a node from the queue.  
   - Reduce the in-degree of its neighbors.  
   - If a neighbor’s in-degree becomes `0`, add it to the queue.  
4. Count how many nodes are processed.  
5. If **count < V**, it means some nodes were not processed (due to a cycle). Hence, the graph contains a cycle.

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(V + E) | Each vertex and edge is processed once |
| Space      | O(V + E) | For adjacency list + in-degree array + queue |

---

## 🎯 Constraints
- 1 ≤ `V, E` ≤ 10⁵  
- No self-loops (`u ≠ v`)  

---

## 💻 Code
```java
class Solution {
    public boolean isCyclic(int V, int[][] edges) {
        List<Integer>[] adj = new ArrayList[V];
        int[] inDegree = new int[V];
        int count = 0;
        Queue<Integer> queue = new LinkedList<>();
        for(int i = 0; i < V; i++){
            adj[i] = new ArrayList<>();
        }
        for(int[] i: edges){
            adj[i[0]].add(i[1]);
            inDegree[i[1]]++;
        }
        for(int i = 0; i < V; i++){
            if(inDegree[i] == 0){
                queue.offer(i);
            }
        }
        while(!queue.isEmpty()){
            int a = queue.poll();
            count++;
            for(int i: adj[a]){
                inDegree[i]--;
                if(inDegree[i] == 0){
                    queue.add(i);
                }
            }
        }
        return count != V;
    }
}
```

---

## 📝 Explanation of Code

- **`adj[]`** → adjacency list to store graph.
- **`inDegree[]`** → number of incoming edges for each vertex.
- **`queue`** → stores vertices with no incoming edges.
- If after traversal, all nodes are processed (`count == V`), graph has **no cycle**. Otherwise, **cycle exists**.

---

> Made with ❤️ by Milan Haria
