<h1 align="center">🔍 Word Search 🔍</h1>

---

## 📝 Problem Statement

You're given a 2D grid `mat[][]` of size `n x m` containing uppercase/lowercase English letters and a string `word`. Your task is to determine whether the word can be formed by traversing adjacent cells **horizontally or vertically** (not diagonally).

- You **cannot reuse a cell** more than once in a path.
- The same letter may appear multiple times on the grid.
- Return `true` if the word exists in the grid, else `false`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
mat = [['T', 'E', 'E'], 
       ['S', 'G', 'K'], 
       ['T', 'E', 'L']], 
word = "GEEK"
```
**Output:** 

```
true
```  

**Explanation:** 

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886266/Web/Other/blobid4_1737981964.png"> </img>

A valid path exists: G → E → E → K

---

### ✅ Example 2:

**Input:**  
```
mat = [['T', 'E', 'U'], 
       ['S', 'G', 'K'], 
       ['T', 'E', 'L']], 
word = "GEEK"
```

**Output:** 
```
false
```  

**Explanation:**

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886266/Web/Other/blobid5_1737981964.png"> </img>

 Cannot form "GEEK" with valid moves.

---

### ✅ Example 3:

**Input:**  
```
mat = [['A', 'B', 'A'], 
       ['B', 'A', 'B']], 
word = "AB"
```

**Output:** 
```
true
```  

**Explanation:** 

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886266/Web/Other/blobid6_1737981964.png"> </img>

Multiple valid paths to form "AB".

---

## 🧠 Approach

### Backtracking DFS

1. **Start Search** from each cell of the grid.
2. If cell value == `word[0]`, start a recursive DFS.
3. For each match:
   - Mark the cell as visited (temporarily).
   - Move in 4 directions: up, down, left, right.
   - Revert cell value after recursion.
4. If we reach the end of the word (i.e., `idx == word.length()`), return true.

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Description                          |
|------------|-------|--------------------------------------|
| Time       | O(N × M × 4^L) | Each cell starts DFS up to length L |
| Space      | O(L)   | Call stack for recursive DFS          |

---

## 🎯 Constraints

- `1 ≤ n, m ≤ 6`
- `1 ≤ L ≤ 15` (L is length of the word)
- `mat[i][j]` and `word[i]` are uppercase/lowercase English letters

---

## 💻 Code

```java
class Solution {
    static boolean findMatch(char[][] mat, String word, int x, int y, int idx){
        int len = word.length(), n = mat.length, m = mat[0].length;
        if(idx == len){
            return true;
        }
        if(x < 0 || y < 0 || x >= n || y >= m){
            return false;
        }
        if(mat[x][y] == word.charAt(idx)){
            char temp = mat[x][y];
            mat[x][y] = '#';
            boolean ans = findMatch(mat, word, x - 1, y, idx + 1) || findMatch(mat, word, x + 1, y, idx + 1) || findMatch(mat, word, x, y - 1, idx + 1) || findMatch(mat, word, x, y + 1, idx + 1);
            mat[x][y] = temp;
            return ans;
        }
        return false;
    }
    static public boolean isWordExist(char[][] mat, String word) {
        int len = word.length();
        int n = mat.length, m = mat[0].length;
        if(len > n * m){
            return false;
        }
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(mat[i][j] == word.charAt(0)){
                    if(findMatch(mat, word, i, j, 0)){
                        return true;
                    }
                }
            }
        }
        return false;
    }
}
```

---

## 📝 Explanation of Code

### 🔹 `isWordExist(...)`
- Scans the matrix to find all positions where the first character of the word appears.
- Calls `findMatch()` from each such position.

### 🔹 `findMatch(...)`
- Recursive DFS function that checks all four directions (up, down, left, right) from the current cell.
- If current cell matches the current character in the word:
  - Temporarily mark the cell as visited by replacing it with `'#'`.
  - Explore all 4 directions recursively.
  - Restore the cell back to its original character after exploring.
- Terminates early when the entire word is found.

---

> Made with ❤️ by Milan Haria
