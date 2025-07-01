<h1 align="center">📍 K Closest Points to Origin 📍</h1>

---

## 📝 Problem Statement

Given an array of points where each point is represented as `points[i] = [xi, yi]` on the X-Y plane, and an integer `k`, return the **k closest points** to the origin `(0, 0)`.

The distance is the **Euclidean distance**:
```
distance = sqrt((x2 - x1)² + (y2 - y1)²)
```

> You can return the k closest points in any order

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
k = 2, points = [[1, 3], [-2, 2], [5, 8], [0, 1]]
```

**Output:**  
```
[[-2, 2], [0, 1]]
```

**Explanation:**  
Distances:  
- (1, 3) → √10  
- (-2, 2) → √8  
- (5, 8) → √89  
- (0, 1) → √1

Closest two: **[-2, 2]** and **[0, 1]**

---

### ✅ Example 2

**Input:**  
```
k = 1, points = [[2, 4], [-1, -1], [0, 0]]
```

**Output:**  
```
[[0, 0]]
```

**Explanation:**  
Distances:  
- (2, 4) → √20  
- (-1, -1) → √2  
- (0, 0) → √0  

Closest one: **[0, 0]**

---

## 🧠 Approach

- Use a **Min Heap** to sort distances.
- Store each point’s **distance squared** (to avoid sqrt) with its index.
- Poll the smallest `k` distances and collect the points.

---

## ⏱️ Time and Space Complexity

| Complexity | Value               | Description                                                     |
|------------|---------------------|-----------------------------------------------------------------|
| Time       | O(n log n)          |Insert all n points into the heap, each insertion takes O(log n) |
| Space      | O(n)                |Stores all n distances and their indexes in the heap             |

---

## 🎯 Constraints

- `1 ≤ k ≤ points.size() ≤ 10⁵`
- `-10⁴ ≤ xi, yi ≤ 10⁴`

---

## 💻 Java Code

```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        PriorityQueue<int[]> queue = new PriorityQueue<>((a, b) -> a[0] - b[0]);
        int n = points.length, c = 0;
        for(int i = 0; i < n; i++){
            int d = (int)Math.pow(points[i][0], 2) + (int)Math.pow(points[i][1], 2);
            queue.offer(new int[]{ d, i });
        }
        int[][] ans = new int[k][];
        while(k > 0){
            int[] a = queue.poll();
            ans[c] = points[a[1]];
            c++;
            k--;
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
