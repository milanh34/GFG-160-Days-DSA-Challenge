<h1 align="center">🪙 Coin Change (Minimum Coins) 🪙</h1>

---

## 📝 Problem Statement

You are given an array `coins[]`, where each element represents a coin of a different denomination, and a target value `sum`. You have an **unlimited supply** of each coin type.

Your task is to determine the **minimum number of coins** needed to obtain the target sum. If it is not possible to form the sum using the given coins, return `-1`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
coins[] = [25, 10, 5], sum = 30
```

**Output:**
```
2
```

**Explanation:**
Use coins [25, 5]

---

### ✅ Example 2:

**Input:**
```
coins[] = [9, 6, 5, 1], sum = 19
```

**Output:**
```
53
```

**Explanation:**
Use coins [9, 9, 1]

---

### ✅ Example 3:

**Input:**
```
coins[] = [5, 1], sum = 0
```

**Output:**
```
0
```

**Explanation:**
No coins needed for sum = 0

---

### ✅ Example 4:

**Input:**
```
coins[] = [4, 6, 2], sum = 5
```

**Output:**
```
-1
```

**Explanation:**
No combination forms sum = 5

---

## 🧠 Approach

We use **Dynamic Programming (Bottom-Up Tabulation)**:

Let `dp[i][j]` be the minimum number of coins required to make sum `j` using coins from index `i` to `n - 1`.

For each coin, we can either:
- **Take it** (if `j - coins[i] >= 0`): `dp[i][j] = 1 + dp[i][j - coins[i]]`
- **Not take it**: `dp[i][j] = dp[i + 1][j]`

We initialize all `dp[i][j]` with `Integer.MAX_VALUE` to represent "not possible". Base case is handled implicitly by the bottom-up traversal.

Finally, `dp[0][sum]` will contain the minimum coins required. If it's still `Integer.MAX_VALUE`, return `-1`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value            | Description                                       |
|------------|------------------|---------------------------------------------------|
| Time       | O(n × sum)       | For each coin and sum combination                |
| Space      | O(n × sum)       | 2D DP table to store subproblem results          |

---

## 🎯 Constraints

- `0 ≤ sum ≤ 10⁴`
- `1 ≤ coins[i] ≤ 10⁴`
- `1 ≤ coins.length ≤ 10³`
- `1 ≤ sum * coins.length ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    public int minCoins(int coins[], int sum) {
        int n = coins.length;
        int[][] dp = new int[n][sum + 1];
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 1; j <= sum; j++) {
                dp[i][j] = Integer.MAX_VALUE;
                int take = Integer.MAX_VALUE, dontTake = Integer.MAX_VALUE;
                if (j - coins[i] >= 0) {
                    take = dp[i][j - coins[i]];
                    if (take != Integer.MAX_VALUE) {
                        take++;
                    }
                }
                if (n > i + 1) {
                    dontTake = dp[i + 1][j];
                }
                dp[i][j] = Math.min(take, dontTake);
            }
        }
        return dp[0][sum] == Integer.MAX_VALUE ? -1 : dp[0][sum];
    }
}
```

---


## 📝 Explanation of Code

- We use a 2D DP table, where `dp[i][j]` represents the minimum number of coins to make sum `j` using coins from index `i` onward.
- For each cell:
    - We try taking the coin (`j - coins[i]`) and add 1 to the result.
    - We also try not taking the coin and move to the next index (`i + 1`).
    - We take the minimum of both choices.
- If at the end, `dp[0][sum]` is still `Integer.MAX_VALUE`, it means there's no way to reach that sum.

---

> Made with ❤️ by Milan Haria
