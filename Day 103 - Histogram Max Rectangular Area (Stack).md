<h1 align="center">📊 Histogram Max Rectangular Area 📊</h1>

---

## 📝 Problem Statement

Given an array `arr[]` representing heights of bars in a histogram (each bar has width `1`), **find the area of the largest rectangle** that can be formed using contiguous bars.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr[] = [60, 20, 50, 40, 10, 50, 60]
```

<img src = "https://media.geeksforgeeks.org/wp-content/uploads/20240924161857/Largest-Rectangular-Area-in-a-Histogram.webp"> </img>

**Output:**  
```
100
```

**Explanation:**  
- The maximum area is `100` using bars `[50, 60]` → height `50` × width `2` = `100`.

---

### ✅ Example 2:
**Input:**  
```
arr[] = [3, 5, 1, 7, 5, 9]
```

**Output:**  
```
15
```

**Explanation:**  
- Pick bars `[7, 5, 9]` → minimum height `5` × width `3` = `15`.

---

### ✅ Example 3:
**Input:**  
```
arr[] = [3]
```

**Output:**  
```
3
```

**Explanation:**  
- Only one bar, area is `3`.

---

## 🧠 Approach

### Observation:
- For each bar, you need to find:
  1. **Nearest smaller bar to the left**
  2. **Nearest smaller bar to the right**

- The bar can extend between these smaller bars → width is `right - left - 1`.

- The area is `height × width`.

- Use a **stack** to find the nearest smaller bars in one pass.

### Steps:
1. Use a stack to keep track of indices with increasing bar heights.
2. When a lower bar is found, pop the stack:
   - For popped bar:
     - Compute `height = arr[top]`
     - Compute `width` using current index and stack's new top.
     - Update maximum area.
3. Repeat until all bars processed.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                        |
|------------|-------|------------------------------------|
| Time       | O(n)  | Each bar pushed/popped once        |
| Space      | O(n)  | Stack for indices                  |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`
- `0 ≤ arr[i] ≤ 10⁴`

---

## 💻 Code

```java
class Solution {
    public static int getMaxArea(int arr[]) {
        int n = arr.length, ans = 0;
        Stack<Integer> stack = new Stack<>();
        for(int i = 0; i <= n; i++){
            while(!stack.isEmpty() && (i == n || arr[stack.peek()] >= arr[i])){
                int height = arr[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                ans = Math.max(ans, height * width);
            }
            stack.push(i);
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- Loop through all bars and a dummy bar at the end.
- Maintain a stack of indices with increasing heights.
- If a lower bar is found:
   - Pop the stack → Calculate area:
      - height = popped bar
      - width = distance to current bar minus stack top minus 1.
- Keep track of maximum area found.
- Return the maximum area.

---

> Made with ❤️ by Milan Haria
