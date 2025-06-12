<h1 align="center">♛ N-Queen Problem ♛</h1>

---

## 📝 Problem Statement

The **N-Queen problem** involves placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Two queens attack each other if they are on:
- The same row,
- The same column,
- Or the same diagonal.

Return all distinct board configurations.  
Each solution is represented as a permutation of `[1, 2, 3, ..., n]` where the number in the *i<sup>th</sup>* position denotes the **row** where the queen is placed in the *i<sup>th</sup>* column.

<img src = "https://contribute.geeksforgeeks.org/wp-content/uploads/ratinmaze_filled11-1.png"> </img>

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
n = 1
```

**Output:**  
```
[[1]]
```

**Explanation:**  
- Only one cell to place the queen.

---

### ✅ Example 2:

**Input:**  
```
n = 4
```

**Output:**  
```
[[2, 4, 1, 3], [3, 1, 4, 2]]
```

**Explanation:**  
- Two valid placements exist for `n = 4` where no two queens threaten each other.

---

### ✅ Example 3:

**Input:**  
```
n = 2
```

**Output:**  
```
[]
```

**Explanation:**  
- It's impossible to place 2 queens without conflict on a 2x2 board.

---

## 🧠 Approach

- Use **Backtracking** to try all placements column-wise.
- For each column, attempt to place a queen in every row.
- Use **bitmasks** for efficient conflict checks:
  - `rows`: Bitmask to track used rows.
  - `beg`: Bitmask for `/` diagonals (`i + j`).
  - `end`: Bitmask for `\` diagonals (`j - i + n`).
- If a position is safe, place the queen and move to the next column.
- When all columns are filled, store the current configuration.

---

## ⏱️ Time and Space Complexity

| Complexity | Value                     | Description                                      |
|------------|---------------------------|--------------------------------------------------|
| Time       | O(n!)                     | Backtracking through permutations                |
| Space      | O(n) recursion + O(k × n) | Where `k` = number of valid solutions            |

---

## 🎯 Constraints

- `1 ≤ n ≤ 10`

---

## 💻 Code

```java
class Solution {
    public boolean isGood(int i, int j, int beg, int end, int n, int rows){
        return !(((rows >> j) & 1) == 1) && !(((beg >> (i + j)) & 1) == 1) && !(((end >> (j - i + n)) & 1) == 1);
    }
    public void solve(ArrayList<Integer> board, ArrayList<ArrayList<Integer>> ans, int n, int rows, int beg, int end, int i){
        if(i > n){
            ans.add(new ArrayList<>(board));
            return;
        }
        for(int j = 1; j <= n; j++){
            if(isGood(i, j, beg, end, n, rows)){
                board.add(j);
                solve(board, ans, n, rows | (1 << j), (beg | (1 << (i + j))), (end | (1 << (j - i + n))), i + 1);
                board.remove(board.size() - 1);
            }
        }
    }
    public ArrayList<ArrayList<Integer>> nQueen(int n) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
        ArrayList<Integer> board = new ArrayList<>();
        solve(board, ans, n, 0, 0, 0, 1);
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
