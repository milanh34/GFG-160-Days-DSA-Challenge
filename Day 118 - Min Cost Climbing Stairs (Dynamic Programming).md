<h1 align="center">🪜 Min Cost Climbing Stairs 🪜</h1>

---

## 📝 Problem Statement

Given an array `cost[]` where `cost[i]` is the cost of stepping on the `i`-th stair, find the **minimum cost** to reach the top of the floor.

- You can climb **one or two steps** after paying the cost.
- You can **start** at index `0` or `1`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
cost = [10, 15, 20]
```

**Output:**  
```
15
```

**Explanation:**  
- Cheapest way: Start at index `1` → pay `15` → reach the top.

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/708151/Web/Other/blobid1_1741612335.png"> </img>

---

### ✅ Example 2:

**Input:**  
```
cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
```

**Output:**  
```
6
```

**Explanation:**  
- Cheapest way: `1 → 1 → 1 → 1 → 1 → 1` = `6`.  
- Skip expensive steps at `1` and `5`.

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/708151/Web/Other/blobid0_1741612208.png"> </img>

---

## 🧠 Approach

### Idea:
Use **Dynamic Programming** to keep track of the minimum cost to reach each step.

### Steps:
1. Let `dp[i]` be the minimum cost to reach step `i`.
2. Base cases:
   - `dp[0] = cost[0]`
   - `dp[1] = cost[1]`
3. For each step `i ≥ 2`:
   - `dp[i] = cost[i] + min(dp[i-1], dp[i-2])`
4. Minimum cost to reach the top is `min(dp[n-1], dp[n-2])`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value   | Description               |
|------------|---------|---------------------------|
| Time       | O(n)    | Single pass through array |
| Space      | O(n)    | DP array to store states  |

---

## 🎯 Constraints

- `2 ≤ cost.length ≤ 10⁵`
- `0 ≤ cost[i] ≤ 999`

---

## 💻 Code

```java
class Solution {
    static int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        if(n == 2){
            return Math.min(cost[0], cost[1]);
        }
        int[] dp = new int[n];
        dp[0] = cost[0];
        dp[1] = cost[1];
        for(int i = 2; i < n; i++){
            dp[i] = Math.min(dp[i - 1], dp[i - 2]) + cost[i];
        }
        return Math.min(dp[n - 1], dp[n - 2]);
    }
}
```

---

> Made with ❤️ by Milan Haria
