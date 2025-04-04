<h1 align="center">📈 Stock Buy and Sell – Max One Transaction Allowed 📉</h1>

---

## 🧩 Problem Statement

You are given an array `prices[]` where each element represents the price of a stock on a particular day. You need to determine the maximum profit that can be made by performing at most one transaction, where a transaction consists of buying on one day and selling on a later day.

> **Note:** You must buy the stock before selling it. If it is not possible to make a profit, return `0`.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
prices = [7, 10, 1, 3, 6, 9, 2]
```

**Output:**  
```
8
```

**Explanation:**  
- Buy the stock on day 2 at price `1` and sell it on day 5 at price `9`. Profit = `9 - 1 = 8`.

---

### ✅ Example 2:
**Input:**  
```
prices = [7, 6, 4, 3, 1]
```

**Output:**  
```
0
```

**Explanation:**  
- The prices are in decreasing order, so no matter when you buy, you won't be able to sell it at a higher price. Hence, the maximum profit is `0`.

---

### ✅ Example 3:
**Input:**  
```
prices = [1, 3, 6, 9, 11]
```

**Output:**  
```
10
```

**Explanation:**  
- Buy the stock on day 0 at price `1` and sell it on day 4 at price `11`. Profit = `11 - 1 = 10`.

---

## 🧠 Approach

### 🧮 Key Idea:

To maximize profit with at most one transaction, the strategy is simple:
1. **Track the minimum price** seen so far as you iterate through the list.
2. For each price, calculate the potential profit if the stock were bought at the minimum price and sold at the current price.
3. Keep track of the maximum profit encountered during this iteration.

This solution only needs one pass through the array, making it efficient.

---

### 🧑‍💻 Detailed Steps:

1. **Initialize Variables**:
   - `ans`: To store the maximum profit, initially set to `0`.
   - `min`: To track the minimum stock price encountered so far, initialized to `Integer.MAX_VALUE`.

2. **Iterate Through Prices**:
   - For each price, update the `min` value if a lower price is encountered.
   - Calculate the potential profit by subtracting the `min` from the current price.
   - Update `ans` if this profit is greater than the current maximum profit.

3. **Return the Maximum Profit**:
   - After completing the loop, return the value of `ans` as the result.

---

## ⏱️ Time & Space Complexity

| Complexity | Value             | Reason                         |
|------------|-------------------|--------------------------------|
| 🕒 Time     | `O(n)`             | We are iterating through the `prices` array once. |
| 📦 Space    | `O(1)`             | We are using only a few variables to track the minimum price and the maximum profit. |

---

## 🎯 Constraints

- `1 ≤ prices.size() ≤ 10⁵`
- `0 ≤ prices[i] ≤ 10⁴`

---

## 💻 Code

```java
class Solution {
    public int maximumProfit(int prices[]) {
        int ans = 0, min = Integer.MAX_VALUE;
        for(int i: prices){
            if(min > i){
                min = i;
            } else {
                ans = Math.max(ans, i - min); 
            }
        }
        return ans;
    }
}
```


---

> Made with ❤️ by Milan Haria
