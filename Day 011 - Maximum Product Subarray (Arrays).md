<h1 align="center">🔥 Maximum Product Subarray 🔥</h1>

---

## 🧩 Problem Statement

Given an array `arr[]` that contains **positive**, **negative**, and **zero** values, find the **maximum product** that can be obtained from a **contiguous subarray** of `arr`.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
arr = [-2, 6, -3, -10, 0, 2]
```

**Output:**  
```
180
```

**Explanation:**  
The subarray `[6, -3, -10]` has the highest product:  
`6 * (-3) * (-10) = 180`

---

### ✅ Example 2:
**Input:**  
```
arr = [-1, -3, -10, 0, 6]
```

**Output:**  
```
30
```

**Explanation:**  
The subarray `[-3, -10]` has the highest product:  
`(-3) * (-10) = 30`

---

### ✅ Example 3:
**Input:**  
```
arr = [2, 3, 4]
```

**Output:**  
```
24
```

**Explanation:**  
All elements are positive. Product of entire array:  
`2 * 3 * 4 = 24`

---

## 🧠 Approach

### 🔄 Dynamic Programming with Tracking of Min/Max

Unlike sum-based problems, **multiplying negatives can flip signs**, so we track both:

- `maxProductEndingHere`: the maximum product ending at current index.
- `minProductEndingHere`: the minimum product ending at current index (important for handling negatives).
- Swap max and min if the current element is negative.

### 🚀 Steps:

1. Initialize `maxSoFar`, `maxEndingHere`, and `minEndingHere` with the first element.
2. Iterate through array from index 1:
   - If `arr[i]` is negative → swap `maxEndingHere` and `minEndingHere`.
   - Update `maxEndingHere = max(arr[i], maxEndingHere * arr[i])`
   - Update `minEndingHere = min(arr[i], minEndingHere * arr[i])`
   - Update `maxSoFar = max(maxSoFar, maxEndingHere)`
3. Return `maxSoFar`

---

## ⏱️ Time & Space Complexity

| Complexity       | Value   | Description                          |
|------------------|---------|--------------------------------------|
| 🕒 Time           | `O(n)`  | Single pass over the array           |
| 📦 Space          | `O(1)`  | No extra space except variables      |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁶`
- `-10 ≤ arr[i] ≤ 10`
- Result fits in a 32-bit integer

---

## 💻 Code

```java
class Solution {
    int maxProduct(int[] arr) {
        int max = arr[0], n = arr.length;
        int min = max, ans = max;
        for(int i = 1; i < n; i++){
            int curr = arr[i];
            if(curr < 0){
                int t = max;
                max = min;
                min = t;
            }
            max = Math.max(max * curr, curr);
            min = Math.min(min * curr, curr);
            ans = Math.max(max, ans);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
