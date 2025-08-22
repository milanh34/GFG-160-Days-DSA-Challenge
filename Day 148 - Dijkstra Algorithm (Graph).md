<h1 align="center">🚦 Dijkstra's Algorithm 🚦</h1>

---

## 📝 Problem Statement
We are given an **undirected weighted graph** with `V` vertices (0 to V-1) and `E` edges.  
Each edge `edges[i] = [u, v, w]` means an edge between nodes `u` and `v` with weight `w`.

We need to find the **shortest distance** from the **source vertex `src`** to every other vertex in the graph.

Return an array `distances[]` where `distances[i]` = shortest distance from `src` to vertex `i`.

> Note:
> - Graph is connected.
> - Edge weights are **non-negative**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
V = 3
edges = [[0, 1, 1], [1, 2, 3], [0, 2, 6]]
src = 2
```

**Output:**
```
[4, 3, 0]
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/892538/Web/Other/blobid0_1744201836.jpg"> </img>

- Distance(2 → 0) = 2 → 1 → 0 = 3 + 1 = 4  
- Distance(2 → 1) = 3  
- Distance(2 → 2) = 0  

---

### ✅ Example 2:

**Input:**
```
V = 5
edges = [[0, 1, 4], [0, 2, 8], [1, 4, 6], [2, 3, 2], [3, 4, 10]]
src = 0
```

**Output:**
```
[0, 4, 8, 10, 10]
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/892538/Web/Other/blobid1_1744202046.jpg"> </img>

- Distance(0 → 1) = 4  
- Distance(0 → 2) = 8  
- Distance(0 → 3) = 0 → 2 → 3 = 10  
- Distance(0 → 4) = 0 → 1 → 4 = 10  

---

## 🧠 Approach
We use **Dijkstra’s Algorithm** with a **Min-Heap PriorityQueue**:
1. Create an adjacency list `adj[]` storing `{neighbor, weight}` for each vertex.
2. Maintain an array `distances[]` initialized with **∞** except `src = 0`.
3. Use a **priority queue** `(distance, node)` to always expand the **shortest distance node**.
4. For each neighbor:
   - If `current_distance + weight < distances[neighbor]` → update it.
   - Push `(new_distance, neighbor)` into the queue.
5. Continue until all shortest distances are finalized.

---

## ⏱️ Complexity
| Complexity | Value | Description |
|------------|-------|-------------|
| Time       | O((V + E) log V) | Each vertex and edge is processed, and updates in the priority queue take `log V`. |
| Space      | O(V + E) | Adjacency list stores all edges, plus arrays for `distances[]`, `visited[]`, and the priority queue. |

---

## 🎯 Constraints
- 1 ≤ `V` ≤ 10⁵  
- 1 ≤ `E` ≤ 10⁵  
- 0 ≤ `edges[i][j]` ≤ 10⁴  
- 0 ≤ `src` < `V`  

---

## 💻 Code
```java
class Solution {
    public int[] dijkstra(int V, int[][] edges, int src) {
        List<List<int[]>> adj = new ArrayList<>();
        for(int i = 0; i < V; i++){
            adj.add(new ArrayList<>());
        }
        for(int[] i: edges){
            adj.get(i[0]).add(new int[]{ i[1], i[2] });
        }
        int[] distances = new int[V];
        PriorityQueue<int[]> queue = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        Arrays.fill(distances, Integer.MAX_VALUE);
        distances[src] = 0;
        queue.offer(new int[]{ 0, src });
        while(!queue.isEmpty()){
            int[] a = queue.poll();
            if(a[0] <= distances[a[1]]){
                for(int[] i: adj.get(a[1])){
                    if(a[0] + i[1] < distances[i[0]]){
                        distances[i[0]] = a[0] + i[1];
                        queue.offer(new int[]{ distances[i[0]], i[0] });
                    }
                }
            }
        }
        return distances;
    }
}
```

---

## 📝 Explanation of Code

1. Build adjacency list from `edges`.
2. Initialize all distances as `∞` except `src = 0`.
3. Use priority queue to always pick the node with the smallest distance.
4. Relax edges → if a better distance is found, update and push into the queue.
5. Continue until all vertices are processed.
6. Return `distances[]`.

---

> Made with ❤️ by Milan Haria
