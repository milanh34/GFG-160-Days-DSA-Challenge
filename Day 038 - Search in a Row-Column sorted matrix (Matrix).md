<h1 align="center">🔍 Search in a Row-Column Sorted Matrix 🔍</h1>

---

## 📝 Problem Statement

Given a 2D **integer matrix** `mat[][]` of size `n x m`, where:

- Each **row is sorted** in increasing order from left to right.
- Each **column is sorted** in increasing order from top to bottom.

And given an integer `x`,  
determine whether the **element x is present** in the matrix.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
mat = [
  [3, 30, 38],
  [20, 52, 54],
  [35, 60, 69]
],
x = 62
```
**Output:**  
```
false
```
**Explanation:**  
Start from top-right: `38 → 54 → 69 → 60 → 35`.  
Since 62 is not found in the search path, return `false`.

---

### ✅ Example 2:
**Input:**  
```
mat = [
  [18, 21, 27],
  [38, 55, 67]
],
x = 55
```
**Output:**  
```
true
```
**Explanation:**  
Start from top-right `27`, move down to `67`, move left to `55`, and find `x`.

---

### ✅ Example 3:
**Input:**  
```
mat = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
],
x = 3
```
**Output:**  
```
true
```
**Explanation:**  
Starting from `3`, we directly find the element at the top-right.

---

## 🧠 Approach

### Intuition:
Take advantage of the matrix's sorted nature:

- Start at the **top-right corner** of the matrix.
- At any cell `mat[i][j]`, there are 3 possibilities:
  - If `mat[i][j] == x` → **Found**.
  - If `mat[i][j] > x` → Move **left** (as all elements below are even bigger).
  - If `mat[i][j] < x` → Move **down** (as all elements to the left are smaller).

### Steps:
1. Start at `(0, m-1)` — top-right corner.
2. While within bounds:
   - If element equals `x`, return `true`.
   - Else move left or down based on comparison.
3. If loop ends, return `false`.

---

## ⏱️ Time & Space Complexity

| Complexity | Value      | Description                                      |
|------------|------------|--------------------------------------------------|
| Time       | O(n + m)   | At most one pass down rows and across columns   |
| Space      | O(1)       | No extra space used                             |

---

## 🔒 Constraints

- `1 ≤ n, m ≤ 1000`
- `1 ≤ mat[i][j] ≤ 10⁹`
- `1 ≤ x ≤ 10⁹`

---

## 💻 Code

```java
class Solution {
    public static boolean matSearch(int mat[][], int x) {
        int n = mat.length, i = 0, j = mat[0].length - 1;
        while(i < n && j >= 0){
            if(mat[i][j] == x){
                return true;
            } else if(mat[i][j] < x){
                i++;
            } else{
                j--;
            }
        }
        return false;
    }
}
```

---

> Made with ❤️ by Milan Haria
