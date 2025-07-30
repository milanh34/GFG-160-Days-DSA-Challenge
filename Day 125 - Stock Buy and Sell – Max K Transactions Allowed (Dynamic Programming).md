<h1 align="center">💹 Stock Buy and Sell – Max K Transactions Allowed 💹</h1>

---

## 📝 Problem Statement

You are given an array `prices[]` where `prices[i]` represents the stock price on day `i`, and an integer `k` representing the maximum number of allowed transactions.

A **transaction** is defined as a **buy followed by a sell**, and you must complete one transaction before starting the next.

Your task is to calculate the **maximum profit** that can be achieved using at most `k` transactions.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
prices = [10, 22, 5, 80], k = 2
```

**Output:**  
```
87
```

**Explanation:**  
- Buy at 10, sell at 22 → Profit = 12  
- Buy at 5, sell at 80 → Profit = 75  
- Total Profit = 12 + 75 = 87  

---

### ✅ Example 2:

**Input:**  
```
prices = [20, 580, 420, 900], k = 3
```

**Output:**  
```
1040
```

**Explanation:**  
- Buy at 20, sell at 580 → Profit = 560  
- Buy at 420, sell at 900 → Profit = 480  
- Total Profit = 560 + 480 = 1040  

---

### ✅ Example 3:

**Input:**  
```
prices = [100, 90, 80, 50, 25], k = 1
```

**Output:**  
```
0
```

**Explanation:**  
Prices are strictly decreasing, so no profit can be made.

---

## 🧠 Approach

We handle the problem in two cases:

### Case 1: `n <= 2 * k`
If the number of days is less than or equal to twice the transactions allowed, then we can treat it like the **infinite transactions** problem — we can buy and sell whenever there's a profit.

### Case 2: General Case (`n > 2 * k`)
We use **Dynamic Programming**:

- Maintain a 1D array `dp` of size `2 * k + 1`
- `dp[j]` stores the maximum profit up to this point after performing `j` actions (buy/sell)
- We alternate:
  - **Odd indices (`j % 2 == 1`)** represent **buy**
  - **Even indices (`j % 2 == 0`)** represent **sell**
- Initialize `dp[0] = 0` and all others to `-∞`
- For every price:
  - Try each action (buy/sell) and update the profit accordingly
- Finally, return `dp[2 * k]` which gives the result after k complete transactions

---

## ⏱️ Time and Space Complexity

| Complexity | Value      | Description                           |
|------------|------------|---------------------------------------|
| Time       | O(N * K)   | Looping through prices and K actions  |
| Space      | O(K)       | 1D array storing 2K states            |

---

## 🎯 Constraints

- 1 ≤ `prices.length` ≤ 10³  
- 1 ≤ `k` ≤ 200  
- 1 ≤ `prices[i]` ≤ 10³

---

## 💻 Code

```java
class Solution {
    static int maxProfit(int prices[], int k) {
        int n = prices.length;
        if(n <= 2 * k){
            int ans = 0;
            for(int i = 1; i < n; i++){
                ans += Math.max(0, prices[i] - prices[i - 1]);
            }
            return ans;
        } else{
            int[] dp = new int[2 * k + 1];
            Arrays.fill(dp, Integer.MIN_VALUE);
            dp[0] = 0;
            for(int i: prices){
                for(int j = 1; j <= 2 * k; j++){
                    dp[j] = (j & 1) == 1 ? Math.max(dp[j], dp[j - 1] - i) : Math.max(dp[j], dp[j - 1] + i);
                }
            }
            return dp[2 * k];
        }
    }
}
```

---

## 📝 Explanation of Code

- We first check if the number of days is small enough to allow greedy profit-taking.
- In the DP approach:
  - `dp[j]` stores the max profit after performing `j` actions.
  - Buy actions subtract `price`, sell actions add `price`.
  - Only perform an action if the previous state exists (`dp[j - 1]`).
- We update the `dp` array for every price in the list.
- Finally, the result is stored at `dp[2 * k]` — the state after completing all transactions.

---

> Made with ❤️ by Milan Haria
