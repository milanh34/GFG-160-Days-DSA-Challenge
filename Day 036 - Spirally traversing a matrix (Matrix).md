<h1 align="center">🌀 Spirally Traversing a Matrix 🌀</h1>

---

## 📝 Problem Statement

Given a **rectangular matrix** `mat[][]` of size `n x m`,  
your task is to **return a list of integers** while traversing the matrix in **spiral form** (clockwise).

Start from the top-left corner and move in a spiral pattern (right → down → left → up → ...), collecting all elements.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
mat = [
  [1,  2,  3,  4],
  [5,  6,  7,  8],
  [9, 10, 11, 12],
  [13,14, 15, 16]
]
```
**Output:**  
```
[1, 2, 3, 4, 8, 12, 16, 15, 14, 13, 9, 5, 6, 7, 11, 10]
```
**Explanation:**  
Start from `1` → move right → `2 3 4`  
Go down → `8 12 16`  
Go left → `15 14 13`  
Go up → `9 5`  
Then go right again → `6 7`  
Down again → `11`  
Left again → `10`

---

### ✅ Example 2:
**Input:**  
```
mat = [
  [1, 2, 3, 4, 5, 6],
  [7, 8, 9,10,11,12],
  [13,14,15,16,17,18]
]
```
**Output:**  
```
[1, 2, 3, 4, 5, 6, 12, 18, 17, 16, 15, 14, 13, 7, 8, 9, 10, 11]
```
**Explanation:**  
Start from `1` → move right through top row → `2 3 4 5 6`  
Go down → `12 18`  
Go left → `17 16 15 14 13`  
Go up → `7`  
Go right again inside → `8 9 10 11`

---

### ✅ Example 3:
**Input:**  
```
mat = [
  [32, 44, 27, 23],
  [54, 28, 50, 62]
]
```
**Output:**  
```
[32, 44, 27, 23, 62, 50, 28, 54]
```
**Explanation:**  
Start from `32` → move right → `44 27 23`  
Go down → `62`  
Go left → `50 28`  
Go up → `54`

---

## 🧠 Approach

### Intuition:
To spiral traverse a matrix, we move in four directions cyclically:
- **Right →**
- **Down ↓**
- **Left ←**
- **Up ↑**

We maintain 4 boundaries (`top`, `bottom`, `left`, `right`) and shrink them after traversing in each direction.

### Steps:

1. Initialize direction vectors for right, down, left, and up.
2. Start at the top-left cell `(0, 0)` and add its value to the result list.
3. While there are unvisited boundaries:
   - Move in the current direction while staying within bounds.
   - Add each visited element to the result.
   - After completing one direction, update the boundary:
     - Right → shrink top
     - Down → shrink right
     - Left → shrink bottom
     - Up → shrink left
4. Repeat until all elements are visited.

---

## ⏱️ Time & Space Complexity

| Complexity | Value     | Description                          |
|------------|-----------|--------------------------------------|
| Time       | O(n * m)  | Each matrix element visited once     |
| Space      | O(n * m)  | Result list stores all elements      |

---

## 🔒 Constraints

- `1 <= n, m <= 1000`
- `0 <= mat[i][j] <= 100`

---

## 💻 Code

```java
class Solution {
    public ArrayList<Integer> spirallyTraverse(int mat[][]) {
        int[][] d = new int[][]{ {0, 1}, {1, 0}, {0, -1}, {-1, 0} };
        int n1 = 0, n2 = mat.length, m1 = 0, m2 = mat[0].length, x = 0, y = 0;
        ArrayList<Integer> ans = new ArrayList<>();
        ans.add(mat[x][y]);
        while(n1 < n2 || m1 < m2){
            boolean isGood = false;
            for(int i = 0; i < 4; i++){
                while(x + d[i][0] >= n1 && x + d[i][0] < n2 && y + d[i][1] >= m1 && y + d[i][1] < m2){
                    x += d[i][0];
                    y += d[i][1];
                    ans.add(mat[x][y]);
                    isGood = true;
                }
                if(i == 0){
                    n1++;
                } else if(i == 1){
                    m2--;
                } else if(i == 2){
                    n2--;
                } else{
                    m1++;
                }
            }
            if(!isGood){
                break;
            }
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
