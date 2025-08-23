<h1 align="center">🎨 Flood Fill Algorithm 🎨</h1>

---

## 📝 Problem Statement
You are given a **2D grid `image[][]`** of size `n * m`, where each `image[i][j]` represents the **color of a pixel** in the image.  
You are also given a **starting pixel** `(sr, sc)` and a **new color value** `newColor`.

Perform a **Flood Fill** starting from `(sr, sc)`, changing its color to `newColor`, along with all **4-directionally connected pixels** having the same original color.

- Pixels are connected **horizontally or vertically** (not diagonally).
- If the starting pixel is already `newColor`, return the image as it is.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
image = [[1, 1, 1, 0],
[0, 1, 1, 1],
[1, 0, 1, 1]]
sr = 1, sc = 2, newColor = 2
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/705720/Web/Other/blobid0_1744378665.jpg"> </img>

**Output:**
```
[[2, 2, 2, 0],
[0, 2, 2, 2],
[1, 0, 2, 2]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/705720/Web/Other/blobid1_1744378699.jpg"> </img>

**Explanation:**  

Starting from `(1,2)`, all connected `1`s are filled with `2`.  

---

### ✅ Example 2:

**Input:**
```
image = [[1, 1, 1],
[1, 1, 0],
[1, 0, 1]]
sr = 1, sc = 1, newColor = 2
```

**Output:**
```
[[2, 2, 2],
[2, 2, 0],
[2, 0, 1]]
```

**Explanation:**  

Connected component around `(1,1)` is changed to `2`. The bottom-right `1` is not connected, so remains unchanged.

---

### ✅ Example 3:

**Input:**
```
image = [[0, 1, 0],
[0, 1, 0]]
sr = 0, sc = 1, newColor = 0
```

**Output:**
```
[[0, 0, 0],
[0, 0, 0]]
```

**Explanation:**  

All connected `1`s are filled with `0`.

---

## 🧠 Approach
We solve this problem using **BFS (Breadth-First Search)**:

1. Get the **original color** of `(sr, sc)`.  
   If it already equals `newColor`, return the image directly.
2. Use a **queue** to perform BFS:
   - Start with `(sr, sc)` and change its color.
   - For each pixel, check its **4 neighbors** (up, down, left, right).
   - If a neighbor has the same **original color**, push it into the queue.
3. Continue until all reachable same-colored pixels are filled.

---

## ⏱️ Time & Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(n * m) | Each pixel is visited at most once |
| Space      | O(n * m) | Queue may store all pixels in the worst case |

---

## 🎯 Constraints
- 1 ≤ `n`, `m` ≤ 500  
- 0 ≤ `image[i][j]` ≤ 10  
- 0 ≤ `newColor` ≤ 10  
- 0 ≤ `sr` < `n`, 0 ≤ `sc` < `m`  

---

## 💻 Code
```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        int n = image.length, m = image[0].length, color = image[sr][sc];
        if(color == newColor){
            return image;
        }
        int[][] directions = new int[][]{ {0, 1}, {0, -1}, {1, 0}, {-1, 0} };
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{ sr, sc });
        while(!queue.isEmpty()){
            int[] a = queue.poll();
            image[a[0]][a[1]] = newColor;
            for(int[] d: directions){
                int x = a[0] + d[0], y = a[1] + d[1];
                if(x >= 0 && x < n && y >= 0 && y < m && image[x][y] == color){
                    queue.offer(new int[]{ x, y });
                }
            }
        }
        return image;
    }
}
```

---

## 📝 Explanation of Code

1. **Base Case**: If the pixel already has the new color, return immediately.
2. **Queue Setup**: Start BFS from `(sr, sc)`.
3. **Flood Fill Process**:
    - Change the color of the current pixel.
    - For each neighbor in **4 directions**, if it has the original color, push it into the queue.
4. **Loop Ends**: Continue until no more connected pixels remain.
5. Return the updated image.

---

> Made with ❤️ by Milan Haria
