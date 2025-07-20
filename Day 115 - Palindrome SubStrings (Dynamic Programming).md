<h1 align="center">✨ Palindrome SubStrings ✨</h1>

---

## 📝 Problem Statement

Given a string `s`, count **all palindromic substrings** of length **≥ 2**.

- A **substring** is contiguous characters.
- A **palindrome** reads the same forwards and backwards.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s = "abaab"
```

**Output:**  
```
3
```

**Explanation:**  
Palindromic substrings: `"aba"`, `"aa"`, `"baab"`.

---

### ✅ Example 2:
**Input:**  
```
s = "aaa"
```

**Output:**  
```
3
```

**Explanation:**  
Palindromic substrings: `"aa"`, `"aa"`, `"aaa"`.

---

### ✅ Example 3:
**Input:**  
```
s = "abbaeae"
```

**Output:**  
```
4
```

**Explanation:**  
Palindromic substrings: `"bb"`, `"abba"`, `"aea"`, `"eae"`.

---

## 🧠 Approach

### Dynamic Programming:
- Use a `dp` table → `dp[i][j] = true` if `s[i..j]` is a palindrome.
- All single characters are palindromes (but ignored here).
- For length `2` substrings: mark if both chars are same.
- For longer: expand if outer chars match and inner is palindrome.
- Count only substrings where length ≥ 2.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                |
|------------|-------|----------------------------|
| Time       | O(n²) | Check all substring pairs  |
| Space      | O(n²) | DP table                   |

---

## 🎯 Constraints

- `2 ≤ s.size() ≤ 10³`
- `s` contains only lowercase English letters.

---

## 💻 Code

```java
class Solution {
    public int countPS(String s) {
        int n = s.length(), ans = 0;
        boolean[][] dp = new boolean[n][n];
        for(int i = 0; i < n; i++){
            dp[i][i] = true;
        }
        for(int i = 0; i < n - 1; i++){
            if(s.charAt(i) == s.charAt(i + 1)){
                dp[i][i + 1] = true;
            }
        }
        for(int l = 3; l <= n; l++){
            for(int i = 0; i < n - l + 1; i++){
                if(dp[i + 1][i + l - 2] && s.charAt(i) == s.charAt(i + l - 1)){
                    dp[i][i + l - 1] = true;
                }
            }
        }
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                if(i != j && dp[i][j]){
                    ans++;
                }
            }
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
