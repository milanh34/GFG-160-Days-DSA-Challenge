<h1 align="center">🔄 Rotate by 90 degree 🔄</h1>

---

## 📝 Problem Statement

Given a **square matrix** `mat[][]` of size `n x n`,  
rotate the matrix by **90 degrees in an anti-clockwise direction**,  
**in-place** (i.e., without using extra space).

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
mat = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
```
**Output:**  
```
[3, 6, 9]
[2, 5, 8]
[1, 4, 7]
```
**Explanation:**  
Rotate each layer anti-clockwise:
- `1 → 3 → 9 → 7 → 1`
- `2 → 6 → 8 → 4 → 2`
- `5` stays in place (center of odd-sized matrix)

---

### ✅ Example 2:
**Input:**  
```
mat = [
  [1, 2],
  [3, 4]
]
```
**Output:**  
```
[2, 4]
[1, 3]
```
**Explanation:**  
- Top left `1` goes to bottom left  
- Top right `2` goes to top left  
- Bottom right `4` goes to top right  
- Bottom left `3` goes to bottom right

---

## 🧠 Approach

### Intuition:
Each square "layer" of the matrix can be rotated individually.  
For every element in a layer, we move 4 elements in a cycle:
```
top → right → bottom → left → top
```

### Steps:

1. Loop over each **layer** from outer to inner.
2. For each layer, rotate elements 4-way using a temporary variable.
3. Swap:
   - Top → Right  
   - Right → Bottom  
   - Bottom → Left  
   - Left → Top

This allows rotation **without using extra space**.

---

## ⏱️ Time & Space Complexity

| Complexity | Value     | Description                                |
|------------|-----------|--------------------------------------------|
| Time       | O(n²)     | Every element is visited once              |
| Space      | O(1)      | Rotation is done in-place (no extra space) |

---

## 🔒 Constraints

- `1 ≤ n ≤ 100`
- `0 ≤ mat[i][j] ≤ 10³`

---

## 💻 Code

```java
class Solution {
    static void rotateby90(int mat[][]) {
        int n = mat.length, ptr = 0;
        while(ptr < n / 2){
            for(int i = ptr; i < n - ptr - 1; i++){
                int temp = mat[ptr][i];
                mat[ptr][i] = mat[i][n - ptr - 1];
                mat[i][n - ptr - 1] = mat[n - ptr - 1][n - i - 1];
                mat[n - ptr - 1][n - i - 1] = mat[n - i - 1][ptr];
                mat[n - i - 1][ptr] = temp;
            }
            ptr++;
        }
    }
}
```

---

> Made with ❤️ by Milan Haria
