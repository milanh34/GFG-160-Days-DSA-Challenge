<h1 align="center">🏝️ Find the Number of Islands 🏝️</h1>

---

## 📝 Problem Statement
You are given a grid of size `n x m` consisting of characters:
- `'W'` → Water  
- `'L'` → Land  

Your task is to **find the number of islands**.  
An island is formed by connecting adjacent lands **horizontally, vertically, or diagonally** (8 directions).  

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
grid = [
['L', 'L', 'W', 'W', 'W'],
['W', 'L', 'W', 'W', 'L'],
['L', 'W', 'W', 'L', 'L'],
['W', 'W', 'W', 'W', 'W'],
['L', 'W', 'L', 'L', 'W']
]
```

**Output:**
```
4
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/891756/Web/Other/blobid1_1743509451.jpg"> </img>

There are **4 islands** formed by connected `'L'`.

---


### ✅ Example 2:

**Input:**
```
grid = [
['W', 'L', 'L', 'L', 'W', 'W', 'W'],
['W', 'W', 'L', 'L', 'W', 'L', 'W']
]
```

**Output:**
```
2
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/891756/Web/Other/blobid2_1743509488.jpg"> </img>

Two distinct islands exist in this grid.

---

## 🧠 Approach
We use **Depth First Search (DFS)**:
1. Traverse the entire grid.  
2. When a `'L'` is found:
   - Count it as a new island.  
   - Run DFS in all **8 directions** to mark all connected land as visited (convert to `'W'`).  
3. Continue until all land cells are processed.  

This ensures we count each island **only once**.

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(n × m) | Each cell is visited at most once |
| Space      | O(n × m) (worst case recursion stack) | DFS may go deep if all land |

---

## 🎯 Constraints
- 1 ≤ `n`, `m` ≤ 500  
- `grid[i][j]` ∈ { 'L', 'W' }  

---

## 💻 Code
```java
class Solution {
    public void dfs(char[][] grid, int x, int y, int n, int m){
        if(x >= 0 && x < n && y >= 0 && y < m && grid[x][y] == 'L'){
            grid[x][y] = 'W';
            for(int i = -1; i <= 1; i++){
                for(int j = -1; j <= 1; j++){
                    dfs(grid, x + i, y + j, n, m);
                }
            }
        }
    }
    public int countIslands(char[][] grid) {
        int n = grid.length, m = grid[0].length, ans = 0;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(grid[i][j] == 'L'){
                    ans++;
                    dfs(grid, i, j, n, m);
                }
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **`dfs()`** → Marks all connected land cells from `(x, y)` as water (`'W'`) so they are not recounted.
- **`countIslands()`** → Loops through grid, whenever an `'L'` is found, increments island count and triggers DFS.
- Works in all 8 directions ensuring diagonal connections are considered.

---

> Made with ❤️ by Milan Haria
