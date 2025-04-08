<h1 align="center">🔁 Max Circular Subarray Sum 🔁</h1>

---

## 🧩 Problem Statement

Given an array of integers `arr[]` arranged in a **circular fashion**, the task is to find the **maximum subarray sum** possible.

A circular array means the end of the array wraps around to the beginning. So subarrays may include wrapping elements.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
arr = [8, -8, 9, -9, 10, -11, 12]
```

**Output:**  
```
22
```

**Explanation:**  
Circular subarray `[12, 8, -8, 9, -9, 10]` gives the maximum sum: `22`.

---

### ✅ Example 2:
**Input:**  
```
arr = [10, -3, -4, 7, 6, 5, -4, -1]
```

**Output:**  
```
23
```

**Explanation:**  
Circular subarray `[7, 6, 5, -4, -1, 10]` gives the maximum sum: `23`.

---

### ✅ Example 3:
**Input:**  
```
arr = [-1, 40, -14, 7, 6, 5, -4, -1]
```

**Output:**  
```
52
```

**Explanation:**  
Circular subarray `[7, 6, 5, -4, -1, -1, 40]` gives the maximum sum: `52`.

---

## 🧠 Approach

### 🔄 Kadane's Algorithm (Extended for Circular Array)

There are two cases for the max subarray:

1. **Non-circular (normal)**: Use regular Kadane’s algorithm to get `maxKadane`.
2. **Circular wrap-around**: Total sum of array - minimum subarray sum (obtained using Kadane's on negative values).

Final answer is the **maximum** of:

- `maxKadane`
- `totalSum - minKadane` (only if array has at least one non-negative number)

> Edge Case: If all elements are negative, return `maxKadane` (do not wrap around).

---

## ⏱️ Time & Space Complexity

| Complexity       | Value   | Description                          |
|------------------|---------|--------------------------------------|
| 🕒 Time           | `O(n)`  | Single scan through the array        |
| 📦 Space          | `O(1)`  | Constant space usage                 |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`
- `-10⁴ ≤ arr[i] ≤ 10⁴`

---

## 💻 Code

```java
class Solution {
    public int circularSubarraySum(int arr[]) {
        int max = -10001, min = 10001, maxSum = -10001, minSum = 10001, total = 0;
        boolean allNeg = true;
        for(int i: arr){
            max = Math.max(max + i, i);
            maxSum = Math.max(maxSum, max);
            min = Math.min(min + i, i);
            minSum = Math.min(minSum, min);
            if(i > 0){
                allNeg = false;
            }
            total += i;
        }
        if(allNeg){
            return maxSum;
        }
        return Math.max(maxSum, total - minSum);
    }
}
```

---

> Made with ❤️ by Milan Haria
