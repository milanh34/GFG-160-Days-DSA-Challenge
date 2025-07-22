<h1 align="center">🪜 Ways to Reach the nᵗʰ Stair 🪜</h1>

---

## 📝 Problem Statement

There are `n` stairs. A person at the bottom wants to reach the top.  
They can climb either **1 stair** or **2 stairs** at a time.  
Count the total **number of distinct ways** to reach the top.  
*(Order matters: e.g. {1,2} and {2,1} are different)*

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
n = 1
```

**Output:**  
```
1
```

**Explanation:**  
Only 1 way → `{1}`.

---

### ✅ Example 2:
**Input:**  
```
n = 2
```

**Output:**  
```
2
```

**Explanation:**  
Two ways → `{1,1}`, `{2}`.

---

### ✅ Example 3:
**Input:**  
```
n = 4
```

**Output:**  
```
5
```

**Explanation:**  
Possible ways: `{1,1,1,1}`, `{1,1,2}`, `{1,2,1}`, `{2,1,1}`, `{2,2}`.

---

## 🧠 Approach

This is a classic **Fibonacci DP**:
- `ways(n) = ways(n-1) + ways(n-2)`
  - `ways(n-1)` → climb 1 step from `(n-1)`th stair.
  - `ways(n-2)` → climb 2 steps from `(n-2)`th stair.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description |
|------------|-------|--------------|
| Time       | O(n)  | Linear DP    |
| Space      | O(n)  | DP table     |

---

## 🎯 Constraints

- `1 ≤ n ≤ 44`

---

## 💻 Code

```java
class Solution {
    int countWays(int n) {
        if(n == 1){
            return 1;
        }
        if(n == 2){
            return 2;
        }
        int[][] dp = new int[n + 1][2];
        dp[1][0] = 1;
        dp[1][1] = 0;
        dp[2][0] = 1;
        dp[2][1] = 1;
        for(int i = 3; i <= n; i++){
            dp[i][0] = dp[i - 1][0] + dp[i - 1][1];
            dp[i][1] = dp[i - 2][0] + dp[i - 2][1];
        }
        return dp[n][0] + dp[n][1];
    }
}

```

---

## 📝 Explanation of Code

1. **Base cases**:
    - `dp[1][0]` = 1 (one way to reach 1 using step 1)
    - `dp[1][1]` = 0 (can't use step 2 for stair 1)
    - `dp[2][0]` = 1 (two 1-steps)
    - `dp[2][1]` = 1 (one 2-step)

2. **For each stair `i`**:
    - `dp[i][0]`: ways ending with a 1-step.
    - `dp[i][1]`: ways ending with a 2-step.

3. **Result**:
    - sum of both ways for stair `n`.
    
---

> Made with ❤️ by Milan Haria
