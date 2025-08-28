<h1 align="center">🔄 Minimum Weight Cycle 🔄</h1>

---

## 📝 Problem Statement

You are given an **undirected weighted graph** with `V` vertices (0 to V-1) and `E` edges.  
Each edge is represented as `edges[i] = [u, v, w]`, meaning there is an edge between node `u` and `v` with weight `w`.

Your task is to find the **minimum weight cycle** in this graph.  
If no cycle exists, return `-1`.

---

## ✅ Examples

### ✅ Example 1

**Input:**
```
V = 5
edges = [[0, 1, 2], [1, 2, 2], [1, 3, 1], [1, 4, 1], [0, 4, 3], [2, 3, 4]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893268/Web/Other/blobid6_1744811506.jpg" width="540"> </img>

**Output:**
```
6
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893268/Web/Other/blobid7_1744811516.jpg" width="540"> </img>

The minimum cycle is:  
`0 → 1 → 4 → 0`  
Weight = `2 + 1 + 3 = 6`

---

### ✅ Example 2

**Input:**
```
V = 5
edges = [[0, 1, 3], [1, 2, 2], [0, 4, 1], [1, 4, 2], [1, 3, 1], [3, 4, 2], [2, 3, 3]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893268/Web/Other/blobid4_1744804067.jpg" width="540"> </img>

**Output:**
```
5
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893268/Web/Other/blobid8_1744811585.jpg" width="540"> </img>

The minimum cycle is:  
`1 → 3 → 4 → 1`  
Weight = `1 + 2 + 2 = 5`

---

## 🧠 Approach

We use **Dijkstra’s Algorithm** with a clever twist:  

1. **Build adjacency list** for the graph.  
2. For each vertex `i`:
   - Run **Dijkstra’s algorithm** to compute shortest paths from `i` to all other nodes.  
   - While relaxing edges, check if using an **already visited edge** can form a **cycle**.  
   - Update `minCycle` if a smaller cycle is found.  
3. Return the **minimum cycle weight**, or `-1` if no cycle exists.

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Descripttion |
|------------|-------|-------------|
| Time       | O(V * (E log V)) | Run Dijkstra from each node |
| Space      | O(V + E) | Adjacency list + distance + prev arrays |

---

## 🎯 Constraints
- 1 ≤ `V` ≤ 100  
- 1 ≤ `E` ≤ 1000  
- 1 ≤ `w` ≤ 100  

---

## 💻 Code
```java
class Solution {
    public int findMinCycle(int V, int[][] edges) {
        List<List<int[]>> adj = new ArrayList<>();
        for(int i = 0; i < V; i++){
            adj.add(new ArrayList<>());
        }
        for(int[] i: edges){
            adj.get(i[0]).add(new int[]{ i[1], i[2] });
        }
        int min = Integer.MAX_VALUE;
        for(int i = 0; i < V; i++){
            int[] dist = new int[V], prev = new int[V];
            Arrays.fill(dist, 1000000000);
            Arrays.fill(prev, -1);
            dist[i] = 0;
            PriorityQueue<int[]> queue = new PriorityQueue<>((a, b) -> a[0] - b[0]);
            queue.offer(new int[]{ 0, i });
            while(!queue.isEmpty()){
                int[] a = queue.poll();
                int d = a[0], node = a[1];
                for(int[] j: adj.get(node)){
                    int b = j[0], w = j[1];
                    if(dist[b] > d + w){
                        dist[b] = d + w;
                        prev[b] = node;
                        queue.offer(new int[]{ dist[b], b });
                    } else if(prev[node] != b && prev[b] != node){
                        min = Math.min(min, dist[node] + dist[b] + w);
                    }
                }
            }
        }
        return min == Integer.MAX_VALUE ? -1 : min;
    }
};
```

---

## 📝 Explanation of Code

1. **Adjacency List** built for efficient traversal.  
2. For each source `src`, run **Dijkstra** to compute shortest paths.  
3. If we encounter an edge `(u, v)` that connects two already discovered paths (`prev[u] != v && prev[v] != u`), then a **cycle exists**.  
   - Update cycle weight as `dist[u] + dist[v] + w`.  
4. Track the **minimum cycle weight** over all runs.  
5. Return `-1` if no cycle exists.  

---

> Made with ❤️ by Milan Haria
