<h1 align="center">🧩 Partition Equal Subset Sum 🧩</h1>

---

## 📝 Problem Statement

Given an integer array `arr[]`, determine if it can be partitioned into two subsets such that the **sum of elements in both subsets is equal**.

Every element must be included in **exactly one** of the two subsets.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [1, 5, 11, 5]
```

**Output:**  
```
true
```

**Explanation:**  
- The total sum is 22  
- Target for each subset: 11  
- One possible partition: `[1, 5, 5]` and `[11]`, both sum to 11

---

### ✅ Example 2:

**Input:**  
```
arr = [1, 3, 5]
```

**Output:**  
```
false
```

**Explanation:**  
- Total sum is 9 (odd)  
- Cannot be divided into two equal parts

---

## 🧠 Approach

This is a variation of the **Subset Sum Problem**:

1. First, compute the total sum of the array.  
2. If the sum is **odd**, it’s impossible to divide into two equal subsets. Return `false`.  
3. If the sum is **even**, reduce the problem to checking whether there's a subset with **sum = totalSum / 2**.
4. Use **Dynamic Programming**:
   - Define `dp[i][j]`: true if a subset from the first `i` items has a total of `j`.
   - Base Case: `dp[i][0] = true` (sum of 0 is always possible).
   - Transition:
     - If we exclude current element: `dp[i][j] = dp[i-1][j]`
     - If we include current element: `dp[i][j] = dp[i-1][j-arr[i-1]]` (if `j >= arr[i-1]`)

---

## ⏱️ Time and Space Complexity

| Complexity | Value                     | Description                            |
|------------|---------------------------|----------------------------------------|
| Time       | O(N × Sum)                | DP table of size (n+1) × (sum/2 + 1)   |
| Space      | O(N × Sum)                | DP matrix to store subset possibilities|

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 100`  
- `1 ≤ arr[i] ≤ 200`  

---

## 💻 Code

```java
class Solution {
    static boolean equalPartition(int arr[]) {
        int n = arr.length, sum = 0;
        for(int i: arr){
            sum += i;
        }
        if((sum & 1) == 1){
            return false;
        }
        sum /= 2;
        boolean[][] dp = new boolean[n + 1][sum + 1];
        for(int i = 0; i <= n; i++){
            dp[i][0] = true;
        }
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= sum; j++){
                dp[i][j] = dp[i - 1][j] || (j < arr[i - 1] ? false : dp[i - 1][j - arr[i - 1]]);
            }
        }
        return dp[n][sum];
    }
}
```

---

> Made with ❤️ by Milan Haria
