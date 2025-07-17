<h1 align="center">🔗 Longest Common Subsequence 🔗</h1>

---

## 📝 Problem Statement

Given **two strings** `s1` and `s2`, return the **length** of their **Longest Common Subsequence (LCS)**.

A **subsequence** is a sequence derived from the string by deleting **some or no elements** *without changing the order* of the remaining elements.  
For example, `"ABE"` is a subsequence of `"ABCDE"`.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
s1 = "ABCDGH"
s2 = "AEDFHR"
```

**Output:**  
```
3
```

**Explanation:**  
The longest common subsequence is `"ADH"`.

---

### ✅ Example 2

**Input:**  
```
s1 = "ABC"
s2 = "AC"
```

**Output:**  
```
2
```

**Explanation:**  
The LCS is `"AC"`.

---

### ✅ Example 3

**Input:**  
```
s1 = "XYZW"
s2 = "XYWZ"
```

**Output:**  
```
3
```

**Explanation:**  
Possible LCS are `"XYW"` or `"XYZ"`.

---

## 🧠 Approach

**Dynamic Programming (DP)** is used to solve this classic problem efficiently.

#### How it works:
- Create a DP table `dp` of size `(n1+1) x (n2+1)`.
- `dp[i][j]` represents the length of the LCS of the first `i` characters of `s1` and first `j` characters of `s2`.
- If characters `s1[i-1]` and `s2[j-1]` match:
  - Extend the LCS by 1: `dp[i][j] = dp[i-1][j-1] + 1`
- Else:
  - Take the max between skipping a character from either `s1` or `s2`:
    - `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`
- The answer is `dp[n1][n2]`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value            | Description                |
|------------|------------------|----------------------------|
| Time       | O(N * M)         | N = length of s1, M = length of s2 |
| Space      | O(N * M)         | For storing the DP table   |

---

## 🎯 Constraints

- `1 ≤ s1.length(), s2.length() ≤ 10³`
- `s1` and `s2` contain only **uppercase English letters**

---

## 💻 Code

```java
class Solution {
    static int lcs(String s1, String s2) {
        int n1 = s1.length(), n2 = s2.length();
        int[][] lcs = new int[n1 + 1][n2 + 1];
        for(int i = 1; i <= n1; i++){
            for(int j = 1; j <= n2; j++){
                if(s1.charAt(i - 1) == s2.charAt(j - 1)){
                    lcs[i][j] = lcs[i - 1][j - 1] + 1;
                } else{
                    lcs[i][j] = Math.max(lcs[i - 1][j], lcs[i][j - 1]);
                }
            }
        }
        return lcs[n1][n2];
    }
}
```

---

> Made with ❤️ by Milan Haria
