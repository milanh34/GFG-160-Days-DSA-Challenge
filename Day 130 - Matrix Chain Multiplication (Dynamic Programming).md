<h1 align="center">🔗 Matrix Chain Multiplication 🔗</h1>

---

## 📝 Problem Statement

You're given an array `arr[]` of size `n`, representing the dimensions of matrices such that:
- Matrix `M1` is of dimension `(arr[0] x arr[1])`
- Matrix `M2` is of dimension `(arr[1] x arr[2])`
- ... and so on, until
- Matrix `Mn-1` is of dimension `(arr[n-2] x arr[n-1])`

You need to find the **minimum number of scalar multiplications** needed to multiply the sequence of matrices optimally.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [2, 1, 3, 4]
```

**Output:**  
```
20
```

**Explanation:**
- M1 = (2x1), M2 = (1x3), M3 = (3x4)
- Two ways to parenthesize:
  - ((M1×M2)×M3): (2×1×3) + (2×3×4) = 6 + 24 = 30
  - (M1×(M2×M3)): (1×3×4) + (2×1×4) = 12 + 8 = 20 ✅ Minimum

---

### ✅ Example 2:

**Input:**  
```
arr = [1, 2, 3, 4, 3]
```

**Output:**  
```
30
```

**Explanation:**
- M1 = (1x2), M2 = (2x3), M3 = (3x4), M4 = (4x3)
- Optimal parenthesization leads to 30 scalar multiplications.

---

### ✅ Example 3:

**Input:**  
```
arr = [3, 4]
```

**Output:**  
```
0
```

**Explanation:**
- Only one matrix → no multiplication needed.

---

## 🧠 Approach

We use **Dynamic Programming** to solve this using the **Matrix Chain Multiplication** technique.

- Define `dp[i][j]` as the minimum number of scalar multiplications needed to multiply matrices from `i` to `j`.
- Base case: No multiplication needed for one matrix.
- For each possible chain length from 2 to n:
  - Try placing parenthesis at every valid position between `i` and `j`
  - Cost = cost of multiplying left sub-chain + cost of multiplying right sub-chain + cost of multiplying the result
  - Track the **minimum** across all such possible splits

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                                |
|------------|-------|--------------------------------------------|
| Time       | O(N³) | 3 nested loops (length, start, partition)  |
| Space      | O(N²) | 2D DP array to store subproblem solutions  |

---

## 🎯 Constraints

- 2 ≤ `arr.length` ≤ 100  
- 1 ≤ `arr[i]` ≤ 200

---

## 💻 Code

```java
class Solution {
    static int matrixMultiplication(int arr[]) {
        int n = arr.length;
        int[][] dp = new int[n][n];
        for(int i = 2; i < n; i++){
            for(int j = 0; j < n - i; j++){
                int k = i + j;
                dp[j][k] = Integer.MAX_VALUE;
                for(int l = j + 1; l < k; l++){
                    int cost = dp[j][l] + dp[l][k] + arr[j] * arr[l] * arr[k];
                    if(cost < dp[j][k]){
                        dp[j][k] = cost;
                    }
                }
            }
        }
        return dp[0][n - 1];
    }
}
```

---

## 📝 Explanation of Code

- `dp[i][j]` represents the **minimum cost** of multiplying matrices from `i` to `j`.
- We fill the table diagonally starting from chains of length 2 to n.
- For each sub-chain, we try every possible position `k` to split:
  - Left side: `dp[i][k]`
  - Right side: `dp[k][j]`
  - Multiplying two result matrices: `arr[i] * arr[k] * arr[j]`
- Store and update the minimum cost in `dp[i][j]`
- Finally, `dp[0][n-1]` contains the minimum cost to multiply the full matrix chain.

---

> Made with ❤️ by Milan Haria
