<h1 align="center">📈 Longest Increasing Subsequence 📈</h1>

---

## 📝 Problem Statement

Given an array `arr[]` of **non-negative integers**, find the **length of the Longest Strictly Increasing Subsequence (LIS)**.

A subsequence is *strictly increasing* if each element is **less than** the next element in the subsequence.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
arr = [5, 8, 3, 7, 9, 1]
```

**Output:**  
```
3
```

**Explanation:**  
One of the LIS: `[5, 7, 9]` → length = 3

---

### ✅ Example 2

**Input:**  
```
arr = [0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 13, 3, 11, 7, 15]
```

**Output:**  
```
6
```

**Explanation:**  
One possible LIS: `[0, 2, 6, 9, 13, 15]` → length = 6

---

### ✅ Example 3

**Input:**  
```
arr = [3, 10, 2, 1, 20]
```

**Output:**  
```
3
```

**Explanation:**  
LIS: `[3, 10, 20]` → length = 3

---

## 🧠 Approach

### Key Idea:
- Use **Dynamic Programming (DP)**.
- Maintain a `dp[]` array where `dp[i]` represents the **length of the LIS ending at index i**.
- For each `i`, look back at `j < i`. If `arr[i] > arr[j]`, `dp[i]` can be `dp[j] + 1`.

### Steps:
1. Initialize `dp[]` with 1 (minimum LIS length for each element).
2. For each `i`:
   - For each `j` before `i`:
     - If `arr[i] > arr[j]`, update `dp[i] = max(dp[i], dp[j] + 1)`.
3. Return the **maximum** value in `dp[]`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                 |
|------------|-------|-----------------------------|
| Time       | O(n²) | Nested loops for DP         |
| Space      | O(n)  | For storing `dp[]`          |

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10³`
- `0 ≤ arr[i] ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    static int lis(int arr[]) {
        int n = arr.length, ans = 1;
        int[] dp = new int[n];
        Arrays.fill(dp, 1);
        for(int i = 1; i < n; i++){
            for(int j = 0; j < i; j++){
                if(arr[i] > arr[j] && dp[i] < dp[j] + 1){
                    dp[i] = dp[j] + 1;
                }
            }
        }
        for(int i: dp){
            ans = Math.max(ans, i);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
