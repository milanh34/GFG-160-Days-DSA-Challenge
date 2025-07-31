<h1 align="center">📈 Stock Buy and Sell – Max 2 Transactions Allowed 📈</h1>

---

## 📝 Problem Statement

In daily share trading, a trader buys and sells shares. You are allowed to make **at most 2 transactions** in a day.  
Each transaction consists of **one buy and one sell**, and the **second transaction can only start after the first one is complete**.

Given an array `prices[]` representing stock prices throughout the day, find the **maximum profit** a trader could have earned.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
prices = [10, 22, 5, 75, 65, 80]
```

**Output:**
```
87
```

**Explanation:**  
- Buy at 10, sell at 22 → profit = 12  
- Buy at 5, sell at 80 → profit = 75  
- Total profit = 12 + 75 = 87

---

### ✅ Example 2:

**Input:**
```
prices = [2, 30, 15, 10, 8, 25, 80]
```

**Output:**
```
100
```

**Explanation:**  
- Buy at 2, sell at 30 → profit = 28  
- Buy at 8, sell at 80 → profit = 72  
- Total profit = 28 + 72 = 100

---

## 🧠 Approach

We maintain four variables:

- `buy1`: Minimum price to buy for the **first transaction**  
- `sell1`: Maximum profit after the **first sell**  
- `buy2`: Effective cost for the **second buy**, which is current price minus the profit earned in the first sell  
- `sell2`: Maximum profit after the **second sell**

### Algorithm:

1. Iterate through each price in the array:
   - Update `buy1` as the minimum of `buy1` and current price
   - Update `sell1` as the maximum of `sell1` and current price - `buy1`
   - Update `buy2` as the minimum of `buy2` and current price - `sell1` (effectively reinvesting the profit)
   - Update `sell2` as the maximum of `sell2` and current price - `buy2`
2. Return `sell2` as the final answer.

This approach ensures:
- We account for the best profit using 2 transactions
- The second transaction only starts after the first is done

---

## ⏱️ Time and Space Complexity

| Complexity | Value  | Description                                      |
|------------|--------|--------------------------------------------------|
| Time       | O(N)   | Traverse the array once                          |
| Space      | O(1)   | Constant extra space for buy/sell tracking       |

---

## 🎯 Constraints

- `1 ≤ prices.length ≤ 10⁵`  
- `1 ≤ prices[i] ≤ 10⁵`  

---

## 💻 Code

```java
class Solution {
    public static int maxProfit(int[] prices) {
        int buy1 = Integer.MAX_VALUE, buy2 = Integer.MAX_VALUE, sell1 = 0, sell2 = 0;
        for(int i: prices){
            buy1 = Math.min(buy1, i);
            sell1 = Math.max(sell1, i - buy1);
            buy2 = Math.min(buy2, i - sell1);
            sell2 = Math.max(sell2, i - buy2);
        }
        return sell2;
    }
}

```

---

> Made with ❤️ by Milan Haria
