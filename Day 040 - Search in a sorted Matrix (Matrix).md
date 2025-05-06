<h1 align="center">🔍 Search in a Sorted Matrix 🔍</h1>

---

## 📝 Problem Statement

Given a **strictly sorted** 2D matrix `mat[][]` of size `n x m` and a number `x`,  
find whether `x` is present in the matrix.

> A **strictly sorted matrix** means:
> - Each row is sorted in **strictly increasing** order.
> - The **first element** of row `i` is **greater** than the **last element** of row `i - 1`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
mat = [
  [1, 5, 9],
  [14, 20, 21],
  [30, 34, 43]
],
x = 14
```
**Output:**  
```
true
```
**Explanation:**  
14 is found at position `[1][0]`.

---

### ✅ Example 2:
**Input:**  
```
mat = [
  [1, 5, 9, 11],
  [14, 20, 21, 26],
  [30, 34, 43, 50]
],
x = 42
```
**Output:**  
```
false
```
**Explanation:**  
42 is not present in the matrix.

---

### ✅ Example 3:
**Input:**  
```
mat = [
  [87, 96, 99],
  [101, 103, 111]
],
x = 101
```
**Output:**  
```
true
```
**Explanation:**  
101 is found at `[1][0]`.

---

## 🧠 Approach

### Intuition:
Because the matrix is **strictly sorted**, we can visualize it as a **flattened 1D sorted array** and perform **binary search**.

However, the current solution does a **two-phase binary search**:
1. First binary search to find the possible **row** where `x` may be.
2. Second binary search **within that row**.

---

### Steps:

1. Check if `x` is **within bounds** of the matrix (first and last elements).
2. Perform binary search across the **last column** to identify the potential row.
3. Perform binary search within the **identified row** to find the element.

---

## ⏱️ Time & Space Complexity

| Complexity | Value        | Description                                  |
|------------|--------------|----------------------------------------------|
| Time       | O(log n + log m) | Two binary searches: one for row, one for column |
| Space      | O(1)         | Constant extra space used                   |

---

## 🔒 Constraints

- `1 ≤ n, m ≤ 1000`
- `1 ≤ mat[i][j] ≤ 10⁹`
- `1 ≤ x ≤ 10⁹`

---

## 💻 Code

```java
class Solution {
    public boolean searchMatrix(int[][] mat, int x) {
        int n = mat.length, m = mat[0].length;
        if(x < mat[0][0] || x > mat[n - 1][m - 1]){
            return false;
        }
        int beg = 0, end = n - 1, row = -1;
        while(beg <= end){
            int mid = (beg + end) / 2;
            if(mat[mid][m - 1] >= x){
                row = mid;
                end = mid - 1;
            } else{
                beg = mid + 1;
            }
        }
        beg = 0;
        end = m - 1;
        while(beg <= end){
            int mid = (beg + end) / 2;
            if(mat[row][mid] == x){
                return true;
            } else if(mat[row][mid] > x){
                end = mid - 1;
            } else{
                beg = mid + 1;
            }
        }
        return false;
    }
}
```

---

> Made with ❤️ by Milan Haria
