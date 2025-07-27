<h1 align="center">🦘 Minimum Jumps 🦘</h1>

---

## 📝 Problem Statement

You are given an array `arr[]` of non-negative integers.  
Each element `arr[i]` represents the **maximum number of steps you can jump forward** from that index.

Your task is to **determine the minimum number of jumps** required to reach the **last index** starting from the first index.

If it is **not possible** to reach the end, return `-1`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9]
```

**Output:**  
```
3
```

**Explanation:**  
- Jump 1 step to index 1 (value 3)  
- Then jump 3 steps to index 4 (value 9)  
- Then jump 6 steps to the end

---

### ✅ Example 2:

**Input:**  
```
arr = [1, 4, 3, 2, 6, 7]
```

**Output:**  
```
2
```

**Explanation:**  
- Jump to index 1 (value 4)  
- Then directly to the end

---

### ✅ Example 3:

**Input:**  
```
arr = [0, 10, 20]
```

**Output:**  
```
-1
```

**Explanation:**  
You cannot move forward from the first element.

---

## 🧠 Approach

### Bottom-Up Dynamic Programming (Tabulation)

1. Create a `dp` array of size `n`, where `dp[i]` stores the **minimum jumps needed from index `i` to reach the end**.
2. Initialize `dp[n-1] = 0` (0 jumps needed from the end).
3. Traverse from second last index to the first:
   - For each index `i`, try jumping to all indices `j` from `i+1` to `i + arr[i]`.
   - If `dp[j]` is not `Integer.MAX_VALUE`, then `dp[i] = min(dp[i], 1 + dp[j])`.
4. If `dp[0] == Integer.MAX_VALUE`, return `-1` (end is unreachable); otherwise return `dp[0]`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value               | Description                              |
|------------|---------------------|------------------------------------------|
| Time       | O(N²)               | Nested loop for each jump possibility    |
| Space      | O(N)                | For the `dp[]` array                     |

---

## 🎯 Constraints

- `2 ≤ arr.length ≤ 10⁴`  
- `0 ≤ arr[i] ≤ 10⁴`

---

## 💻 Code

```java
class Solution {
    static int minJumps(int[] arr) {
        int n = arr.length;
        int[] dp = new int[n];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[n - 1] = 0;
        for(int i = n - 2; i >= 0; i--){
            for(int j = i + 1; j < n && j <= i + arr[i]; j++){
                if(dp[j] != Integer.MAX_VALUE){
                    dp[i] = Math.min(dp[i], 1 + dp[j]);
                }
            }
        }
        return dp[0] == Integer.MAX_VALUE ? -1 : dp[0];
    }
}
```

---

> Made with ❤️ by Milan Haria
