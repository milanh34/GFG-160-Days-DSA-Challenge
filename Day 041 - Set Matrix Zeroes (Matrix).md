<h1 align="center">🧮 Set Matrix Zeroes 🧮</h1>

---

## 📝 Problem Statement

Given a 2D matrix `mat[][]` of size `n x m`, modify the matrix **in-place** such that:
- If `mat[i][j] == 0`, then set all elements in the `i-th` row and `j-th` column to `0`.

⚠️ **Constraint**: Do this in **constant space complexity (O(1))**.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
mat = [
  [1, -1, 1],
  [-1, 0, 1],
  [1, -1, 1]
]
```
**Output:**
```
[
  [1,  0, 1],
  [0,  0, 0],
  [1,  0, 1]
]
```
**Explanation:**  
The cell (1,1) is 0, so all elements in row 1 and column 1 become 0.

---

### ✅ Example 2:
**Input:**
```
mat = [
  [0, 1, 2, 0],
  [3, 4, 5, 2],
  [1, 3, 1, 5]
]
```
**Output:**
```
[
  [0, 0, 0, 0],
  [0, 4, 5, 0],
  [0, 3, 1, 0]
]
```
**Explanation:**  
The cells (0,0) and (0,3) are 0, so entire row 0, column 0, and column 3 are set to 0.

---

## 🧠 Approach

### ⚙️ Strategy:
1. Use **first row and first column as markers**.
2. Track if the **first row** and **first column** should be zeroed separately.
3. Traverse the matrix to **mark** the zero rows and columns using `mat[0][j]` and `mat[i][0]`.
4. Traverse again to **zero out** relevant cells.
5. Lastly, zero out the **first row/column** if needed.

---

### ✍️ Steps:

- Use `mat[0][0]` to mark both first row and column.  
- Use extra booleans: `firstRow`, `firstCol` to keep track if they should be zeroed.

---

## ⏱️ Time & Space Complexity

| Type       | Complexity | Description                                                                 |
|------------|------------|-----------------------------------------------------------------------------|
| Time       | O(n × m)   | Every cell is visited at most twice.                                        |
| Space      | O(1)       | No additional matrix or array used. Only a few variables are maintained.    |

---

## 🔒 Constraints

- `1 ≤ n, m ≤ 500`
- `−2³¹ ≤ mat[i][j] ≤ 2³¹ − 1`

---

## 💻 Code

```java
class Solution {
    public void setMatrixZeroes(int[][] mat) {
        int n = mat.length, m = mat[0].length;
        boolean firstRow = false, firstCol = false;
        if(mat[0][0] == 0){
            firstRow = true;
            firstCol = true;
        }
        if(!firstRow){
            for(int i = 1; i < m; i++){
                if(mat[0][i] == 0){
                    firstRow = true;
                    break;
                }
            }
        }
        for(int i = 1; i < n; i++){
            if(!firstCol && mat[i][0] == 0){
                firstCol = true;
            }
            for(int j = 1; j < m; j++){
                if(mat[i][j] == 0){
                    mat[i][0] = 0;
                    mat[0][j] = 0;
                }
            }
        }
        for(int i = 1; i < n; i++){
            for(int j = 1; j < m; j++){
                if(mat[i][0] == 0 || mat[0][j] == 0){
                    mat[i][j] = 0;
                }
            }
        }
        if(firstCol){
            for(int i = 0; i < n; i++){
                mat[i][0] = 0;
            }
        }
        if(firstRow){
            for(int i = 0; i < m; i++){
                mat[0][i] = 0;
            }
        }
    }
}
```

---

## 📝 Explanation of Code

- First, we scan the **first row** and **first column** separately to see if they need to be zeroed at the end.
- Then, we traverse the rest of the matrix. If any cell is 0, we **mark** its corresponding row and column using the first cell of that row and column.
- Next, we scan the matrix again (excluding the first row/column) and set a cell to 0 if its row or column was marked.
- Finally, if the **first row or column originally had a 0**, we zero them out separately.

This ensures that we never use extra space beyond a few boolean variables, while correctly applying the zeroing logic.

---

> Made with ❤️ by Milan Haria
