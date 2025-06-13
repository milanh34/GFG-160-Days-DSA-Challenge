<h1 align="center">🧩 Solve the Sudoku 🧩</h1>

---

## 📝 Problem Statement

Given an incomplete Sudoku grid represented by a 9x9 matrix `mat[][]`, solve the Sudoku by filling in the missing numbers. The Sudoku solution must follow the rules:

- Each digit `1-9` must appear **exactly once** in every **row**.
- Each digit `1-9` must appear **exactly once** in every **column**.
- Each digit `1-9` must appear **exactly once** in every **3x3 subgrid**.

⚠️ The input is guaranteed to have exactly one valid solution.  
Zeros in the matrix represent blanks to be filled.

---

## ✅ Examples

### ✅ Example 1:

**Input:**

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/701375/Web/Other/blobid0_1738306620.png" width="480"> </img>

**Output:**  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/701375/Web/Other/blobid0_1738306722.png" width="480"> </img>

**Explanation:**
All rows, columns, and subgrids will have unique digits from 1 to 9 with no conflicts.

---

### ✅ Example 2:

**Input:**

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886267/Web/Other/blobid1_1738136756.png" width="480"> </img>

**Output:**  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/701375/Web/Other/blobid0_1738306722.png" width="480"> </img>

**Explanation:**
All rows, columns, and subgrids will have unique digits from 1 to 9 with no conflicts.

---

## 🧠 Approach

1. **Bitmask Optimization:**  
   Use bitmasks for:
   - `row[i]`: tracks digits used in row `i`
   - `col[j]`: tracks digits used in column `j`
   - `box[b]`: tracks digits used in 3×3 subgrid `b = (i / 3) * 3 + (j / 3)`

2. **Backtracking:**
   - Start from top-left and move cell by cell.
   - If a cell is pre-filled (non-zero), skip it.
   - Else try placing `1–9` in that cell.
     - Check if it’s **safe** using bitmasks.
     - If valid, place number and recurse.
     - If it leads to a dead-end, undo (backtrack).
   - Repeat until a valid configuration is found.

3. **Guaranteed Unique Solution:**  
   The function can return as soon as it finds the first valid configuration.

---

## ⏱️ Time and Space Complexity

| Complexity | Value     | Description                                  |
|------------|-----------|----------------------------------------------|
| Time       | O(9^k)    | Where `k` is the number of empty cells       |
| Space      | O(1)      | In-place solution with small constant space  |

---

## 🎯 Constraints

- `mat.length = 9`
- `mat[i].length = 9`
- `0 ≤ mat[i][j] ≤ 9`
- Exactly one valid solution is guaranteed.

---

## 💻 Code

```java
class Solution {
    static boolean isSafe(int[][] mat, int i, int j, int num, int[] row, int[] col, int[] box) {
        if((row[i] & (1 << num)) != 0 || (col[j] & (1 << num)) != 0 || (box[i / 3 * 3 + j / 3] & (1 << num)) != 0)
            return false;
        return true;
    }
    static boolean sudokuSolverRec(int[][] mat, int i, int j, int[] row, int[] col, int[] box){
        int n = mat.length;
        if(i == n - 1 && j == n){
            return true;
        }
        if(j == n){
            i++;
            j = 0;
        }
        if(mat[i][j] != 0){
            return sudokuSolverRec(mat, i, j + 1, row, col, box);
        }
        for(int num = 1; num <= n; num++){
            if(isSafe(mat, i, j, num, row, col, box)){
                mat[i][j] = num;
                row[i] |= (1 << num);
                col[j] |= (1 << num);
                box[i / 3 * 3 + j / 3] |= (1 << num);
                if(sudokuSolverRec(mat, i, j + 1, row, col, box)){
                    return true;
                }
                mat[i][j] = 0;
                row[i] &= ~(1 << num);
                col[j] &= ~(1 << num);
                box[i / 3 * 3 + j / 3] &= ~(1 << num);
            }
        }
        return false;
    }
    static void solveSudoku(int[][] mat) {
        int n = mat.length;
        int[] row = new int[n], col = new int[n], box = new int[n];
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                if(mat[i][j] != 0){
                    row[i] |= (1 << mat[i][j]);
                    col[j] |= (1 << mat[i][j]);
                    box[(i / 3) * 3 + j / 3] |= (1 << mat[i][j]);
                }
            }
        }
        sudokuSolverRec(mat, 0, 0, row, col, box);
    }
}
```

---

## 📝 Explanation of Code

### 🔹 `isSafe(...)`
- Checks whether placing a number at position `(i, j)` is safe.
- Uses bitmasking to check if the number is already present in the corresponding row, column, or 3x3 box.

### 🔹 `sudokuSolverRec(...)`
- A recursive function that tries to fill the board using backtracking:
  - If a cell is already filled, it moves forward.
  - Otherwise, it tries placing each digit from 1 to 9.
  - If the placement is valid (`isSafe` returns true), it sets the bitmask and proceeds recursively.
  - If it leads to a dead end, it **backtracks** by resetting the cell and clearing the bitmask.

### 🔹 `solveSudoku(...)`
- Initializes bitmasks for rows, columns, and boxes.
- Scans the board to set initial constraints (i.e., already-filled values).
- Calls the recursive function to solve the Sudoku.

---


> Made with ❤️ by Milan Haria
