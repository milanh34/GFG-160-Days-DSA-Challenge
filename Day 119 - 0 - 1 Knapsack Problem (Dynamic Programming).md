<h1 align="center">🎒 0 - 1 Knapsack Problem 🎒</h1>

---

## 📝 Problem Statement

Given **n items**, each with a **value** and **weight**, and a knapsack with capacity **W**, find the **maximum total value** that can be accommodated **without exceeding W**.

- You can **either include an item or exclude it** (cannot break an item).
- Each item is available **only once**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
W = 4  
val = [1, 2, 3]  
wt = [4, 5, 1]
```

**Output:**  
```
3
```

**Explanation:**  
- Only the last item can be picked (weight = 1, value = 3).

---

### ✅ Example 2:

**Input:**  
```
W = 3  
val = [1, 2, 3]  
wt = [4, 5, 6]
```

**Output:**  
```
0
```

**Explanation:**  
- No item fits in the knapsack.

---

### ✅ Example 3:

**Input:**  
```
W = 5  
val = [10, 40, 30, 50]  
wt = [5, 4, 2, 3]
```

**Output:**  
```
80
```

**Explanation:**  
- Pick the 3rd (value 30, weight 2) and 4th (value 50, weight 3) items.

---

## 🧠 Approach

Use **Dynamic Programming (DP)** to build solutions to subproblems:
- `dp[i][j]` = Maximum value for the first `i` items with knapsack capacity `j`.

### Steps:
1. Initialize `dp[0][*]` and `dp[*][0]` to 0.
2. For each item `i` and capacity `j`:
    - If weight `wt[i-1]` <= `j`:  
        - Include it: `val[i-1] + dp[i-1][j - wt[i-1]]`  
        - Or exclude it: `dp[i-1][j]`
    - Take the maximum.
3. Final answer is `dp[n][W]`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value   | Description                   |
|------------|---------|-------------------------------|
| Time       | O(n*W)  | Fill n * W DP states          |
| Space      | O(n*W)  | DP table for memoization      |

---

## 🎯 Constraints

- `2 ≤ n ≤ 10³`
- `1 ≤ W, val[i], wt[i] ≤ 10³`

---

## 💻 Code

```java
class Solution {
    static int knapsack(int W, int val[], int wt[]) {
        int n = val.length;
        int[][] dp = new int[n + 1][W + 1];
        for(int i = 0; i <= n; i++){
            for(int j = 0; j <= W; j++){
                if(i == 0 || j == 0){
                    dp[i][j] = 0;
                } else{
                    dp[i][j] = Math.max(
                        wt[i - 1] <= j ? 
                            val[i - 1] + dp[i - 1][j - wt[i - 1]] : 0, 
                        dp[i - 1][j]
                    );
                }
            }
        }
        return dp[n][W];
    }
}

```

---

## 📝 Explanation of Code

- Loop through all items (i) and capacities (j).
- If the item fits, choose max of:
    - including it (value + remaining capacity)
    - or skipping it.
- Use 2D DP to build up solution.
- Return dp[n][W] for max value.

---

> Made with ❤️ by Milan Haria
