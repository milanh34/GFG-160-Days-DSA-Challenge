<h1 align="center">🪙 Coin Change (Count Ways) 🪙</h1>

---

## 📝 Problem Statement

Given an integer array `coins[]` representing different denominations of currency and an integer `sum`, find the number of ways to make that `sum` using different combinations from `coins[]`.

> **Note**:  
- You can use **infinite** supply of each coin denomination.
- Answers are guaranteed to fit into a 32-bit integer.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
coins[] = [1, 2, 3], sum = 4
```

**Output:**
```
4
```

**Explanation:**
The 4 ways to make sum = 4 are:
- [1, 1, 1, 1]
- [1, 1, 2]
- [2, 2]
- [1, 3]

---

### ✅ Example 2:

**Input:**
```
coins[] = [2, 5, 3, 6], sum = 10
```

**Output:**
```
5
```

**Explanation:**
The 5 ways to make sum = 10 are:
- [2, 2, 2, 2, 2]
- [2, 2, 3, 3]
- [2, 2, 6]
- [2, 3, 5]
- [5, 5]

---

### ✅ Example 3:

**Input:**
```
coins[] = [5, 10], sum = 3
```

**Output:**
```
0
```

**Explanation:**
No coin combination can make the target sum.

---

## 🧠 Approach

Use **Dynamic Programming** to build a solution bottom-up.

Let `dp[i][j]` represent the number of ways to make sum `j` using the first `i` coins.
- `dp[0][0] = 1` → One way to make sum 0 (use no coins).
- If we don't pick the coin: `dp[i][j] += dp[i-1][j]`
- If we pick the coin: `dp[i][j] += dp[i][j - coin[i-1]]`

---

## ⏱️ Time and Space Complexity

| Complexity | Value          | Description                      |
|------------|----------------|----------------------------------|
| Time       | O(n × sum)    | For each coin and sum combination |
| Space      | O(n × sum)    | 2D DP table                       |

---

## 🎯 Constraints

- `1 ≤ sum ≤ 10³`
- `1 ≤ coins[i] ≤ 10⁴`
- `1 ≤ coins.length ≤ 10³`

---

## 💻 Code

```java
class Solution {
    public int count(int coins[], int sum) {
        int n = coins.length;
        int[][] dp = new int[n + 1][sum + 1];
        dp[0][0] = 1;
        for(int i = 1; i <= n; i++){
            for(int j = 0; j <= sum; j++){
                if(j - coins[i - 1] >= 0){
                    dp[i][j] = dp[i][j - coins[i - 1]] + dp[i - 1][j];
                } else{
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }
        return dp[n][sum];
    }
}
```

---


## 📝 Explanation of Code

- `dp[i][j]` represents the number of ways to make `j` using the first `i` coins.
- For each coin, we compute:
  - Ways by **including** it (`dp[i][j - coins[i-1]]`)
  - Ways by **excluding** it (`dp[i-1][j]`)
- We build the table iteratively and return `dp[n][sum]` as the final result.

---

> Made with ❤️ by Milan Haria
