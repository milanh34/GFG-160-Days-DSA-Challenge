<h1 align="center">✏️ Edit Distance ✏️</h1>

---

## 📝 Problem Statement

Given two strings `s1` and `s2`, return the **minimum number of operations** required to convert `s1` to `s2`.

Allowed operations are:
- **Insert** a character at any position of the string.
- **Remove** any character from the string.
- **Replace**  any character from the string with any other character.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s1 = "geek"
s2 = "gesek"
```

**Output:**  
```
1
```

**Explanation:**  
Insert `'s'` between the two `'e'`s → `"geek"` → `"gesek"`.

---

### ✅ Example 2:
**Input:**  
```
s1 = "gfg"
s2 = "gfg"
```

**Output:**  
```
0
```

**Explanation:**  
Both strings are already equal → No operation needed.

---

### ✅ Example 3:
**Input:**  
```
s1 = "abcd"
s2 = "bcfe"
```

**Output:**  
```
3
```

**Explanation:**  
- Remove `'a'` → `"bcd"`
- Replace `'d'` with `'f'` → `"bcf"`
- Insert `'e'` → `"bcfe"`

---

## 🧠 Approach

### Dynamic Programming:
- Use a `dp` table where `dp[i][j]` = minimum operations to convert `s1[0..i-1]` to `s2[0..j-1]`.
- If characters match → no extra operation.
- Else → choose minimum among:
  - Replace: `dp[i-1][j-1] + 1`
  - Insert: `dp[i][j-1] + 1`
  - Remove: `dp[i-1][j] + 1`

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                    |
|------------|-------|--------------------------------|
| Time       | O(n × m) | `n` = length of `s1`, `m` = length of `s2` |
| Space      | O(n × m) | DP table                      |

---

## 🎯 Constraints

- `1 ≤ s1.length(), s2.length() ≤ 10³`
- `s1` and `s2` are lowercase.

---

## 💻 Code

```java
class Solution {
    public int editDistance(String s1, String s2) {
        int n = s1.length(), m = s2.length();
        int[][] dp = new int[n + 1][m + 1];
        for(int i = 0; i <= n; i++){
            dp[i][0] = i;
        }
        for(int i = 0; i <= m; i++){
            dp[0][i] = i;
        }
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(s1.charAt(i - 1) == s2.charAt(j - 1)){
                    dp[i][j] = dp[i - 1][j - 1];
                } else{
                    dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1])) + 1;
                }
            }
        }
        return dp[n][m];
    }
}
```

---

> Made with ❤️ by Milan Haria
