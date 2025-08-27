<h1 align="center">🌉 Floyd Warshall 🌉</h1>

---

## 📝 Problem Statement

You are given a **weighted directed graph**, represented by an **adjacency matrix** `dist[][]` of size `n x n`, where:
- `dist[i][j]` = weight of edge from node `i` → `j`.  
- If no edge exists, `dist[i][j] = 10⁸` (represents infinity).  
- Graph may contain **negative weights**, but **no negative cycles**.

Your task is to compute the **shortest distance between every pair of nodes** using the **Floyd-Warshall Algorithm**.  
The result must **update the matrix in place**.

---

## ✅ Examples

### ✅ Example 1

**Input:**
```
dist = [
 [0,   4,   108, 5,   108],
 [108, 0,   1,   108, 6],
 [2,   108, 0,   3,   108],
 [108, 108, 1,   0,   2],
 [1,   108, 108, 4,   0]
]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893245/Web/Other/blobid0_1744701272.jpg" width="540"> </img>

**Output:**
```
[
 [0, 4, 5, 5, 7],
 [3, 0, 1, 4, 6],
 [2, 6, 0, 3, 5],
 [3, 7, 1, 0, 2],
 [1, 5, 5, 4, 0]
]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893245/Web/Other/blobid1_1744701370.jpg" width="540"> </img>

**Explanation:**  
Shortest paths are updated by considering all intermediate nodes.

---

### ✅ Example 2

**Input:**
```
dist = [
 [0,  -1, 2],
 [1,   0, 108],
 [3,   1, 0]
]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893245/Web/Other/blobid2_1744701698.jpg" width="540"> </img>

**Output:**
```
[
 [0, -1, 2],
 [1,  0, 3],
 [2,  1, 0]
]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893245/Web/Other/blobid3_1744701713.jpg" width="540"> </img>

**Explanation:**  
- Shortest path `2 → 0 = 2` via `2 → 1 → 0`.  
- Shortest path `1 → 2 = 3` via `1 → 0 → 2`.  

---

## 🧠 Approach

### Floyd-Warshall

The **Floyd-Warshall Algorithm** is a **Dynamic Programming (DP)** approach for **All-Pairs Shortest Paths**.

1. **Initialize:** Start with given adjacency matrix `dist[][]`.  
2. **Iterate over all nodes `k`** as an intermediate point.  
3. For every pair `(i, j)`, update:  
   ```java
   dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
   ```
   if both paths are finite.  
4. After considering all intermediate nodes, `dist[i][j]` will hold the shortest path from `i → j`.  

---

## ⏱️ Time & Space Complexity
| Complexity | Value | Descripttion |
|------------|-------|-------------|
| Time       | O(n³) | Triple nested loop over all vertices |
| Space      | O(1) | In-place matrix update |

---

## 🎯 Constraints
- 1 ≤ `n` ≤ 100  
- -1000 ≤ `dist[i][j]` ≤ 1000  
- `dist[i][j] = 10⁸` means **infinity**  

---

## 💻 Code
```java
class Solution {
    public void floydWarshall(int[][] dist) {
        int n = dist.length;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                for(int k = 0; k < n; k++){
                    if(dist[j][i] != 100000000 && dist[i][k] != 100000000){
                        dist[j][k] = Math.min(dist[j][k], dist[j][i] + dist[i][k]);
                    }
                }
            }
        }
    }
}
```

---

## 📝 Explanation of Code
1. **Loop over all possible intermediate nodes `k`.**  
2. For each pair `(i, j)`, check if `i → k` and `k → j` are reachable.  
3. If yes, update shortest path `i → j`.  
4. After all iterations, `dist[i][j]` will represent the **shortest distance** from `i` to `j`.  

---

> Made with ❤️ by Milan Haria
