<h1 align="center">🎯 Subset Sum Problem 🎯</h1>

---

## 📝 Problem Statement

Given an array of positive integers `arr[]` and a value `sum`, determine whether there exists a **subset** of the array whose elements **add up to the given sum**.

Return `true` if such a subset exists, otherwise return `false`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [3, 34, 4, 12, 5, 2], sum = 9
```

**Output:**  
```
true
```

**Explanation:**  
Subset `[3, 4, 2]` has a sum of 9.

---

### ✅ Example 2:

**Input:**  
```
arr = [3, 34, 4, 12, 5, 2], sum = 30
```

**Output:**  
```
false
```

**Explanation:**  
There is no subset whose sum is 30.

---

### ✅ Example 3:

**Input:**  
```
arr = [1, 2, 3], sum = 6
```

**Output:**  
```
true
```

**Explanation:**  
The entire array `[1, 2, 3]` forms the subset with sum 6.

---

## 🧠 Approach

We use **Dynamic Programming** (DP) to solve this problem.

Let `dp[i][j]` represent whether a subset of the first `i` elements of the array can sum to `j`.

### Transition:

- If we **don't include** `arr[i-1]`, then `dp[i][j] = dp[i-1][j]`
- If we **include** `arr[i-1]`, then `dp[i][j] = dp[i-1][j - arr[i-1]]` (only if `j >= arr[i-1]`)
- So, `dp[i][j] = dp[i-1][j] || dp[i-1][j - arr[i-1]]`

### Base Case:

- `dp[0][0] = true` — empty subset sums to 0.
- `dp[i][0] = true` for all `i` — any number of elements can sum to 0 using the empty subset.
- `dp[0][j] = false` for all `j > 0` — no subset of 0 elements can sum to j.

---

## ⏱️ Time and Space Complexity

| Complexity | Value                 | Description                            |
|------------|-----------------------|----------------------------------------|
| Time       | O(n × sum)            | DP table of size `n x sum`             |
| Space      | O(n × sum)            | 2D boolean table used for computation  |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 200`  
- `1 ≤ arr[i] ≤ 200`
- `1 ≤ sum ≤ 10⁴`

---

## 💻 Code

```java
class Solution {
    static Boolean isSubsetSum(int arr[], int sum) {
        int n = arr.length;
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

## 📝 Explanation of Code

- We initialize a 2D DP table `dp[n+1][sum+1]`, where `dp[i][j]` means "is it possible to form sum `j` using the first `i` elements".
- We initialize all `dp[i][0] = true` since zero sum is possible with the empty subset.
- For each element, we either include it or skip it to build the subset.
- In the end, `dp[n][sum]` tells us whether it's possible to form `sum` using all `n` elements.

---

> Made with ❤️ by Milan Haria
