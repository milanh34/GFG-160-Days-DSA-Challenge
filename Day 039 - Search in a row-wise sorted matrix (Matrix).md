<h1 align="center">🔍 Search in a Row-Wise Sorted Matrix 🔍</h1>

---

## 📝 Problem Statement

Given a **row-wise sorted 2D matrix** `mat[][]` of size `n x m` and an integer `x`,  
determine whether the **element x is present** in the matrix.

> Note: Each row is sorted independently in increasing order.  
> That is, for any row `i`: `mat[i][j] <= mat[i][j+1]`

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
mat = [
  [3, 4, 9],
  [2, 5, 6],
  [9, 25, 27]
], x = 9
```
**Output:**  
```
true
```
**Explanation:**  
9 is present in the first and third rows. A binary search finds it in one of them.

---

### ✅ Example 2:
**Input:**  
```
mat = [
  [19, 22, 27, 38, 55, 67]
], x = 56
```
**Output:**  
```
false
```
**Explanation:**  
56 is not present in the matrix. Binary search confirms its absence.

---

### ✅ Example 3:
**Input:**  
```
mat = [
  [1, 2, 9],
  [65, 69, 75]
], x = 91
```
**Output:**  
```
false
```
**Explanation:**  
91 is greater than all values in the matrix. Hence, it’s not found.

---

## 🧠 Approach

### Intuition:
Since **each row** is sorted, we can perform a **binary search** on every row instead of a full scan.

### Steps:

1. Loop through each row of the matrix.
2. For each row, perform binary search for `x`.
3. If found in any row → return `true`.
4. If all rows are searched and `x` is not found → return `false`.

---

## ⏱️ Time & Space Complexity

| Complexity | Value        | Description                                  |
|------------|--------------|----------------------------------------------|
| Time       | O(n × log m) | Perform binary search for `x` in each row   |
| Space      | O(1)         | Constant extra space used                   |

---

## 🔒 Constraints

- `1 ≤ n, m ≤ 1000`
- `1 ≤ mat[i][j] ≤ 10⁵`
- `1 ≤ x ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public boolean binarySearch(int[] arr, int end, int x){
        int beg = 0;
        while(beg <= end){
            int mid = (beg + end) / 2;
            if(arr[mid] == x){
                return true;
            } else if(arr[mid] > x){
                end = mid - 1;
            } else{
                beg = mid + 1;
            }
        }
        return false;
    }
    public boolean searchRowMatrix(int[][] mat, int x) {
        int n = mat.length, m = mat[0].length;
        for(int i = 0; i < n; i++){
            if(binarySearch(mat[i], m - 1, x)){
                return true;
            }
        }
        return false;
    }
}
```

---

> Made with ❤️ by Milan Haria
