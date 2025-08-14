<h1 align="center">🍊 Rotten Oranges 🍊</h1>

---

## 📝 Problem Statement
You are given a matrix `mat[][]` of size `n × m` representing a grid of oranges, where:  
- **0** → Empty cell  
- **1** → Fresh orange  
- **2** → Rotten orange  

A rotten orange at position `(i, j)` can rot its adjacent fresh oranges in **1 unit time**.  
Adjacent cells are **up, down, left, right** (no diagonals).  

Your task is to determine the **minimum time** required for all oranges to become rotten.  
If it is **impossible** to rot all oranges, return **-1**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
mat = [[0, 1, 2],
[0, 1, 2],
[2, 1, 1]]
```

**Output:**
```
1
```

**Explanation:**  
- Initially rotten: `(0,2), (1,2), (2,0)`  
- After 1 unit time: All fresh oranges are rotten.

---


### ✅ Example 2:

**Input:**
```
mat = [[2, 2, 0, 1]]
```

**Output:**
```
-1
```

**Explanation:**  
Orange at `(0,3)` can never rot because it is isolated from other rotten oranges.

---

### ✅ Example 3:

**Input:**
```
mat = [[2, 2, 2],
[0, 2, 0]]
```

**Output:**
```
0
```

**Explanation:**  
No fresh oranges exist, so time is 0.

---

## 🧠 Approach
1. **Count fresh oranges** and add all **rotten oranges** to a queue with initial time.
2. Perform **BFS** (multi-source) from all rotten oranges simultaneously:
   - For each rotten orange, try to rot its **4 neighbors**.
   - If a fresh orange becomes rotten, decrement fresh count and update time.
3. Continue BFS until no fresh oranges are left or the queue is empty.
4. If all fresh oranges are rotted, return the time taken; otherwise, return **-1**.

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Description |
|------------|-------|-------------|
| Time       | O(n × m) | Each cell is visited at most once |
| Space      | O(n × m) | BFS queue and visited state storage |

---

## 🎯 Constraints
- 1 ≤ n, m ≤ 500  
- `mat[i][j] ∈ {0, 1, 2}`  

---

## 💻 Code
```java
class Solution {
    public int orangesRotting(int[][] mat) {
        int n = mat.length, m = mat[0].length, one = 0, count = 0, ans = 0;
        int[][] directions = new int[][]{ {1, 0}, {-1, 0}, {0, 1}, {0, -1} };
        PriorityQueue<int[]> queue = new PriorityQueue<>((a, b) -> a[2] - b[2]);
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(mat[i][j] == 2){
                    queue.offer(new int[]{i, j, 1});
                } else if(mat[i][j] == 1){
                    one++;
                }
            }
        }
        if(one == 0){
            return 0;
        }
        while(count < one && !queue.isEmpty()){
            int[] a = queue.poll();
            for(int[] i: directions){
                int x = a[0] + i[0], y = a[1] + i[1];
                if(x >= 0 && x < n && y >= 0 && y < m && mat[x][y] == 1){
                    mat[x][y] = 2;
                    queue.offer(new int[]{ x, y, a[2] + 1});
                    count++;
                    ans = Math.max(ans, a[2]);
                }
            }
        }
        return count < one ? -1 : ans;
    }
}
```

---

## 📝 Explanation of Code

- **Multi-source BFS** starts from all initially rotten oranges.
- `queue` stores `(row, col, time)` for each rotten orange.
- Each fresh orange that gets rotted is counted, and `ans` is updated to reflect time taken.
- If at the end some fresh oranges are left, return `-1`.

---

> Made with ❤️ by Milan Haria
