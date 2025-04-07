<h1 align="center">💡 Maximum Product Subarray 💡</h1>

---

## 🧩 Problem Statement

Given an array `arr[]` containing positive and negative integers (may contain 0 as well), find the maximum product that can be obtained from a contiguous subarray of `arr[]`.

Note: It is guaranteed that the output fits in a 32-bit integer.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
arr[] = [-2, 6, -3, -10, 0, 2]
```

**Output:**  
```
180
```

**Explanation:**  
The subarray with maximum product is `{6, -3, -10}` with product `6 * (-3) * (-10) = 180`.

---

### ✅ Example 2:
**Input:**  
```
arr[] = [-1, -3, -10, 0, 6]
```

**Output:**  
```
30
```

**Explanation:**  
The subarray with maximum product is `{-3, -10}` with product `(-3) * (-10) = 30`.

---

### ✅ Example 3:
**Input:**  
```
arr[] = [2, 3, 4]
```

**Output:**  
```
24
```

**Explanation:**  
For an array with all positive elements, the result is the product of all elements: `2 * 3 * 4 = 24`.

---

## 🧠 Approach

To solve this problem efficiently, we can use a dynamic programming approach where we maintain two variables:
- `max`: The maximum product subarray ending at the current element.
- `min`: The minimum product subarray ending at the current element.

This is because a negative number can turn a large negative product into a positive product, so we need to track both the maximum and minimum products at each step.

### Steps:
1. **Initialization**: 
   - Set `max` and `min` to the first element of the array.
   - Set `ans` to the first element of the array.
   
2. **Iterate through the array**: 
   - For each element `curr`:
     - If `curr` is negative, swap `max` and `min`.
     - Update `max` and `min` as the maximum and minimum of:
       - `curr`
       - `curr * max`
       - `curr * min`
   - Update `ans` with the maximum of `max` and `ans`.

3. **Return** the value of `ans`.

---

## ⏱️ Time & Space Complexity

| Complexity | Value             | Reason                         |
|------------|-------------------|--------------------------------|
| 🕒 Time     | `O(n)`             | We only loop through the array once. |
| 📦 Space    | `O(1)`             | We are using a constant amount of space. |

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10^6`
- `-10 ≤ arr[i] ≤ 10`

---

## 💻 Code

```java
class Solution {
    int maxProduct(int[] arr) {
        int max = arr[0], n = arr.length;
        int min = max, ans = max;
        for (int i = 1; i < n; i++) {
            int curr = arr[i];
            if (curr < 0) {
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
