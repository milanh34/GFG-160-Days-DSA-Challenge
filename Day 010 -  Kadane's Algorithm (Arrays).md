<h1 align="center">⚡ Kadane's Algorithm ⚡</h1>

---

## 🧩 Problem Statement

Given an array of integers `arr[]`, find the **maximum sum** of any **contiguous subarray**.

Your goal is to determine the subarray that yields the **maximum possible sum**.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
arr = [2, 3, -8, 7, -1, 2, 3]
```

**Output:**  
```
11
```

**Explanation:**  
The subarray `[7, -1, 2, 3]` has the highest sum:  
`7 + (-1) + 2 + 3 = 11`

---

### ✅ Example 2:
**Input:**  
```
arr = [-2, -4]
```

**Output:**  
```
-2
```

**Explanation:**  
Since all elements are negative, the subarray with the highest value is `[-2]`.

---

### ✅ Example 3:
**Input:**  
```
arr = [5, 4, 1, 7, 8]
```

**Output:**  
```
25
```

**Explanation:**  
The entire array has a positive sum:  
`5 + 4 + 1 + 7 + 8 = 25`

---

## 🧠 Approach

### 🔍 Kadane's Algorithm

Kadane’s algorithm solves the **Maximum Subarray Sum** problem in linear time `O(n)` using dynamic programming.

### 🚀 Key Idea:
- Maintain a variable `maxEndingHere` to track the **maximum sum ending at current index**.
- Maintain a variable `maxSoFar` to store the **global maximum sum**.

At each step:
- `maxEndingHere = max(current_element, maxEndingHere + current_element)`
- `maxSoFar = max(maxSoFar, maxEndingHere)`

---

## ⏱️ Time & Space Complexity

| Complexity | Value         | Description                          |
|------------|---------------|--------------------------------------|
| 🕒 Time     | `O(n)`        | We traverse the array once to compute the max subarray sum. |
| 📦 Space    | `O(1)`        | Only a few variables (max, ans) are used—no extra space. |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`
- `-10⁹ ≤ arr[i] ≤ 10⁴`

---

## 💻 Code

```java
class Solution {
    int maxSubarraySum(int[] arr) {
        int max = 0, ans = Integer.MIN_VALUE;
        for(int i: arr){
            max = Math.max(max + i, i);
            ans = Math.max(ans, max);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
