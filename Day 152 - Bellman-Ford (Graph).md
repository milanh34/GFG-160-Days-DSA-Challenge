<h1 align="center">🔔 Bellman Ford 🔔</h1>

---

## 📝 Problem Statement
You are given a **weighted directed graph** with `V` vertices numbered from `0` to `V-1` and `E` edges.  
Each edge is represented as `edges[i] = [u, v, w]` meaning there is a directed edge from `u` to `v` with weight `w`.  

You are also given a **source vertex `src`**.  
Your task is to compute the **shortest distances** from the source to all vertices using the **Bellman-Ford Algorithm**.

- If a vertex is **unreachable**, mark its distance as `10⁸`.  
- If the graph contains a **negative weight cycle**, return `[-1]`.  

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
V = 5
edges = [[1, 3, 2], [4, 3, -1], [2, 4, 1], [1, 2, 1], [0, 1, 5]]
src = 0
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893096/Web/Other/blobid0_1744455175.jpg"> </img>

**Output:**
```
[0, 5, 6, 6, 7]
```

**Explanation:**  
- Distance from 0 → 1 = 5 (via [0 → 1])  
- Distance from 0 → 2 = 6 (via [0 → 1 → 2])  
- Distance from 0 → 3 = 6 (via [0 → 1 → 2 → 4 → 3])  
- Distance from 0 → 4 = 7 (via [0 → 1 → 2 → 4])  

---

### ✅ Example 2:
**Input:**
```
V = 4
edges = [[0, 1, 4], [1, 2, -6], [2, 3, 5], [3, 1, -2]]
src = 0
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893096/Web/Other/blobid1_1744455218.jpg"> </img>

**Output:**
```
[-1]
```

**Explanation:**  
The graph contains a **negative cycle**: `1 → 2 → 3 → 1` with total weight -3.  
Shortest paths cannot be computed reliably.

---

## 🧠 Approach

### Bellman-Ford Algorithm

1. **Initialization**:  
   - Distance array `dist[]` initialized with `10⁸` (infinity).  
   - `dist[src] = 0`.

2. **Relax edges (V-1 times)**:  
   - For each edge `(u, v, w)`, update if `dist[u] + w < dist[v]`.  
   - Repeat `V-1` times (because shortest path in graph with V nodes can have at most V-1 edges).

3. **Negative Cycle Check**:  
   - Perform one more relaxation step.  
   - If any edge can still be relaxed, graph contains a **negative cycle** → return `[-1]`.

4. **Return distances**:  
   - If no negative cycle, return computed distances.  

---

## ⏱️ Time & Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(V × E) | Each of V-1 iterations relaxes all E edges |
| Space      | O(V) | Distance array |

---

## 🎯 Constraints
- 1 ≤ `V` ≤ 100  
- 1 ≤ `E` ≤ `V × (V - 1)`  
- -1000 ≤ `w` ≤ 1000  
- 0 ≤ `src` < `V`  

---

## 💻 Code
```java
class Solution {
    public int[] bellmanFord(int V, int[][] edges, int src) {
        int n = edges.length;
        int[] ans = new int[V];
        Arrays.fill(ans, 100000000);
        ans[src] = 0;
        for(int i = 0; i < V - 1; i++){
            for(int[] j: edges){
                if(ans[j[0]] < 100000000 && ans[j[0]] + j[2] < ans[j[1]]){
                    ans[j[1]] = ans[j[0]] + j[2];
                }
            }
        }
        for(int[] i: edges){
            if(ans[i[0]] < 100000000 && ans[i[0]] + i[2] < ans[i[1]]){
                return new int[]{ -1 };
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. Initialize distances with infinity (`10⁸`), except `src = 0`.  
2. Loop `V-1` times → relax all edges.  
3. For each edge `(u, v, w)`, update `dist[v] = dist[u] + w` if smaller.  
4. After V-1 relaxations, run one extra check:  
   - If an update is still possible → **negative cycle exists** → return `[-1]`.  
5. Otherwise, return the `dist[]` array with shortest paths.

---

> Made with ❤️ by Milan Haria
