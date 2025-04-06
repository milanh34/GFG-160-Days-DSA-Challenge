<h1 align="center">💡 Kadane's Algorithm 💡</h1>

---

## 🧩 Problem Statement

Given an integer array `arr[]`, find the **maximum sum of a subarray** in the given array. A subarray is a contiguous part of an array.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
arr[] = [2, 3, -8, 7, -1, 2, 3]
```

**Output:**  
```
11
```

**Explanation:**  
The subarray `{7, -1, 2, 3}` has the largest sum `11`.

---

### ✅ Example 2:
**Input:**  
```
arr[] = [-2, -4]
```

**Output:**  
```
-2
```

**Explanation:**  
The subarray `{-2}` has the largest sum `-2`.

---

### ✅ Example 3:
**Input:**  
```
arr[] = [5, 4, 1, 7, 8]
```

**Output:**  
```
25
```

**Explanation:**  
The subarray `{5, 4, 1, 7, 8}` has the largest sum `25`.

---

## 🧠 Approach

Kadane's Algorithm is a famous technique to solve the "maximum sum subarray" problem efficiently in **O(n)** time. Here's how it works:

1. **Initialization**: Initialize two variables:
   - `max`: Keeps track of the current maximum sum that ends at the current element.
   - `ans`: Keeps track of the overall maximum sum found so far.

2. **Iterate through the array**: For each element:
   - Update `max` to be the maximum of the current element or the sum of the current element and `max`. This is done to decide whether to extend the current subarray or start a new subarray at the current element.
   - Update `ans` to be the maximum of `ans` and `max`.

3. **Result**: Once the iteration is complete, `ans` contains the maximum sum of the subarray.

---

### 💡 Algorithm

1. **Initialize**: Start with `max = 0` and `ans = Integer.MIN_VALUE`.
2. **Loop** through the array:
   - Update `max = Math.max(max + i, i)`, where `i` is the current element.
   - Update `ans = Math.max(ans, max)`.
3. **Return** `ans` which holds the maximum sum.

---

## ⏱️ Time & Space Complexity

| Complexity | Value             | Reason                         |
|------------|-------------------|--------------------------------|
| 🕒 Time     | `O(n)`             | We only loop through the array once. |
| 📦 Space    | `O(1)`             | We are using a constant amount of space. |

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10^5`
- `-10^9 ≤ arr[i] ≤ 10^4`

---

## 💻 Code

```java
class Solution {
    int maxSubarraySum(int[] arr) {
        int max = 0, ans = Integer.MIN_VALUE;
        for(int i: arr) {
            max = Math.max(max + i, i);
            ans = Math.max(ans, max);
        }
        return ans;
    }
}
```


---

> Made with ❤️ by Milan Haria
