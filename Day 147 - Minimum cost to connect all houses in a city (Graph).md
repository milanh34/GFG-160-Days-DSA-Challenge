<h1 align="center">🏠 Minimum Cost to Connect All Houses in a City 🏠</h1>

---

## 📝 Problem Statement
We are given `n` houses in a city, each represented by its 2D coordinates `{x, y}`.  
We need to **connect all houses** with the **minimum possible cost**.  

📌 **Cost of connecting two houses** = Manhattan Distance  
For two houses at `(xi, yi)` and `(xj, yj)`,
```
Cost = |xi - xj| + |yi - yj|
```
We must connect all houses such that the **total cost is minimized**.

---


## ✅ Examples

### ✅ Example 1:

**Input:**  
```
n = 5
houses = [[0, 7], [0, 9], [20, 7], [30, 7], [40, 70]]
```

**Output:**
```
105
```

**Explanation:**  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/892720/Web/Other/blobid0_1744176520.jpg"> </img>

- Connect house (0,7) ↔ (0,9) → cost = 2  
- Connect house (0,7) ↔ (20,7) → cost = 20  
- Connect house (20,7) ↔ (30,7) → cost = 10  
- Connect house (30,7) ↔ (40,70) → cost = 73  
Total = 2 + 20 + 10 + 73 = **105**


---


### ✅ Example 2:

**Input:**
```
n = 4
houses = [[0, 0], [1, 1], [1, 3], [3, 0]]
```

**Output:**
```
7
```

**Explanation:**  
- Connect (0,0) ↔ (1,1) → cost = 2  
- Connect (1,1) ↔ (1,3) → cost = 2  
- Connect (0,0) ↔ (3,0) → cost = 3  
Total = 2 + 2 + 3 = **7**

---

## 🧠 Approach
This is a **Minimum Spanning Tree (MST)** problem, where:
- Houses = Nodes
- Edge cost = Manhattan Distance between houses

We can solve it using **Prim’s Algorithm**:
1. Start with an arbitrary house (say index `0`).
2. Maintain a `distances[]` array to store the minimum cost required to connect each house to the MST.
3. At each step:
   - Pick the unvisited house with the minimum connection cost.
   - Add its cost to the result.
   - Update distances of all unvisited houses with the minimum of their existing cost or the new edge cost.
4. Continue until all houses are connected.

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(n²) | For each of n houses, we check distances to all others |
| Space      | O(n)  | Arrays for `visited[]` and `distances[]` |

---

## 🎯 Constraints
- 1 ≤ `n` ≤ 10³  
- 0 ≤ `houses[i][j]` ≤ 10³  

---

## 💻 Code
```java
class Solution {
    public int minCost(int[][] houses) {
        int n = houses.length, ans = 0;
        boolean[] visited = new boolean[n];
        int[] distances = new int[n];
        Arrays.fill(distances, Integer.MAX_VALUE);
        distances[0] = 0;
        for(int i = 0; i < n; i++){
            int max = Integer.MAX_VALUE, node = -1;
            for(int j = 0; j < n; j++){
                if(!visited[j] && max > distances[j]){
                    max = distances[j];
                    node = j;
                }
            }
            visited[node] = true;
            ans += max;
            for(int j = 0; j < n; j++){
                if(!visited[j]){
                    distances[j] = Math.min(distances[j], Math.abs(houses[node][0] - houses[j][0]) + Math.abs(houses[node][1] - houses[j][1]));
                }
            }
        }
        return ans;
    }
}

```

---

## 📝 Explanation of Code

1. **Initialization**
- `visited[]` keeps track of which houses are already connected.
- `distances[]` stores the minimum cost to connect each house.
2. **Building MST**
- Start from house `0` with cost `0`.
- Repeatedly pick the next house with the smallest connection cost.
3. **Updating Costs**
- Each time a new house joins the MST, we update the `distances[]` of all remaining houses using Manhattan distance.
4. **Final Answer**
- `ans` accumulates the total cost of connecting all houses.

---

> Made with ❤️ by Milan Haria
