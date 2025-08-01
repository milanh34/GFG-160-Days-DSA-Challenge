<h1 align="center">🦹‍♂️ Stickler Thief 🦹‍♂️</h1>

---

## 📝 Problem Statement

Stickler the thief wants to **loot houses arranged in a straight line**, but he **cannot loot two consecutive houses**.  
Given an integer array `arr[]` where `arr[i]` represents the money in the i-th house, return the **maximum amount of money** he can loot without looting two adjacent houses.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [6, 5, 5, 7, 4]
```

**Output:**  
```
15
```

**Explanation:**  
Looting house 1 (6), house 3 (5), and house 5 (4) gives the total: 6 + 5 + 4 = **15**

---

### ✅ Example 2:

**Input:**  
```
arr = [1, 5, 3]
```

**Output:**  
```
5
```

**Explanation:**  
Best choice is to loot only house 2 (5).

---

### ✅ Example 3:

**Input:**  
```
arr = [4, 4, 4, 4]
```

**Output:**  
```
8
```

**Explanation:**  
Looting alternate houses — either (1 and 3) or (2 and 4) — gives: 4 + 4 = **8**

---

## 🧠 Approach

### Dynamic Programming (Bottom-Up)

1. Let `dp[i]` represent the **maximum loot** from the first `i` houses.
2. Base cases:
   - `dp[0] = 0` → no houses, no loot.
   - `dp[1] = arr[0]` → only first house to loot.
3. For each house `i` from 2 to n:
   - Either **loot the i-th house** and add `dp[i-2]`, or
   - **Skip** it and take `dp[i-1]`
   - `dp[i] = max(arr[i-1] + dp[i-2], dp[i-1])`
4. Return `dp[n]` as the result.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                        |
|------------|-------|------------------------------------|
| Time       | O(N)  | Traverse all houses once           |
| Space      | O(N)  | For storing dp[0…n]                |

---

## 🎯 Constraints

- 1 ≤ `arr.length` ≤ 10⁵  
- 1 ≤ `arr[i]` ≤ 10⁴

---

## 💻 Code

```java
class Solution {
    public int findMaxSum(int arr[]) {
        int n = arr.length;
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = arr[0];
        for(int i = 2; i <= n; i++){
            dp[i] = Math.max(arr[i - 1] + dp[i - 2], dp[i - 1]);
        }
        return dp[n];
    }
}
```

---

## 📝 Explanation of Code

- `dp[i]` stores the **maximum money** that can be looted from the first `i` houses.
- At each step, we check:
  - If we **loot the current house**, we must skip the previous one, so add `arr[i-1] + dp[i-2]`.
  - If we **don’t loot** it, just carry over the previous max i.e., `dp[i-1]`.
- We take the **maximum of both options**.
- Finally, return `dp[n]`, which contains the answer for all houses.

---

> Made with ❤️ by Milan Haria
