<h1 align="center">💹 Stock Buy and Sell – Multiple Transaction Allowed 💹</h1>

---

## 🧩 Problem Statement

You are given an array `prices[]` where the `i-th` element represents the cost of stock on the `i-th` day. You may decide to either buy or sell the stock on any given day. Your task is to find the maximum profit that you can get by making multiple transactions. 

> **Note:** A stock can only be sold if it has been bought previously, and multiple stocks cannot be held on any given day.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
prices = [100, 180, 260, 310, 40, 535, 695]
```

**Output:**  
```
865
```

**Explanation:**  
- Buy the stock on day 0 at price `100` and sell it on day 3 at price `310`. Profit = `310 - 100 = 210`.
- Buy the stock on day 4 at price `40` and sell it on day 6 at price `695`. Profit = `695 - 40 = 655`.
- Total Maximum Profit = `210 + 655 = 865`.

---

### ✅ Example 2:
**Input:**  
```
prices = [4, 2, 2, 2, 4]
```

**Output:**  
```
2
```

**Explanation:**  
- Buy the stock on day 3 at price `2` and sell it on day 4 at price `4`. Profit = `4 - 2 = 2`.
- Maximum Profit = `2`.

---

## 🧠 Approach

### 🧮 Key Idea:

In this problem, we aim to maximize profit by buying and selling stocks on different days. The trick is to accumulate profit whenever there is an increase in stock price from one day to the next.

- **Step 1**: Loop through the array of prices.
- **Step 2**: Whenever the price on the next day is greater than the price on the current day, accumulate the profit (difference between the two).
- **Step 3**: Return the total accumulated profit at the end.

> 📝 **Note**: We can perform multiple transactions as long as there is an increase in price. Thus, we capture all positive price differences.

---

### 🧑‍💻 Detailed Steps:

1. **Iterate through the array**:  
   Loop through the prices array from the second day onwards (index 1) to check if there is an increase in price from the previous day.

2. **Accumulate the profit**:  
   Every time the price increases, calculate the difference (profit) and add it to the total profit.

3. **Return the total profit**:  
   The total profit is the sum of all the differences where prices have increased.

---

## ⏱️ Time & Space Complexity

| Complexity | Value             | Reason                         |
|------------|-------------------|--------------------------------|
| 🕒 Time     | `O(n)`             | We are iterating through the `prices` array once. |
| 📦 Space    | `O(1)`             | We only need a few variables to track the total profit. |

---

## 🎯 Constraints

- `1 ≤ prices.size() ≤ 10⁵`
- `0 ≤ prices[i] ≤ 10⁴`

---

## 💻 Code

```java
class Solution {
    public int maximumProfit(int prices[]) {
        int n = prices.length, ans = 0;
        for(int i = 1; i < n; i++){
            int diff = prices[i] - prices[i - 1];
            if(diff > 0){
                ans += diff;
            }
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
