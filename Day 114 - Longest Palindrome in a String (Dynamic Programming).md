<h1 align="center">🔍 Longest Palindromic Substring 🔍</h1>

---

## 📝 Problem Statement

Given a string `s`, find the **longest palindromic substring** within `s`.

- A **substring** is a contiguous sequence of characters within a string, defined as `s[i...j]` where `0 ≤ i ≤ j < len(s)`.
- A **palindrome** reads the same forward and backward. More formally, `s` is a palindrome if `reverse(s)` == `s`.
- If multiple longest palindromic substrings exist, return the **first one** from left to right.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s = "forgeeksskeegfor"
```

**Output:**  
```
"geeksskeeg"
```

**Explanation:**  
Possible palindromic substrings: `"kssk"`, `"ss"`, `"eeksskee"`, `"geeksskeeg"` → The longest is `"geeksskeeg"`.

---

### ✅ Example 2:
**Input:**  
```
s = "Geeks"
```

**Output:**  
```
"ee"
```

**Explanation:**  
The longest palindromic substring is `"ee"`.

---

### ✅ Example 3:
**Input:**  
```
s = "abc"
```

**Output:**  
```
"a"
```

**Explanation:**  
Single letters `"a"`, `"b"`, and `"c"` are palindromic substrings. First is `"a"`.

---

## 🧠 Approach

### Dynamic Programming:
- Use a 2D DP table `dp[i][j]` → `true` if `s[i..j]` is a palindrome.
- All substrings of length `1` are palindromes.
- Substrings of length `2` are palindromes if both chars match.
- For length `≥ 3`: `s[i] == s[j]` **and** `dp[i+1][j-1] == true`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                      |
|------------|-------|----------------------------------|
| Time       | O(n²) | Check all substring pairs        |
| Space      | O(n²) | DP table for substrings          |

---

## 🎯 Constraints

- `1 ≤ s.length ≤ 10³`
- `s` consists of only lowercase English letters.

---

## 💻 Code

```java

class Solution {
    static String longestPalindrome(String s) {
        int n = s.length();
        boolean[][] dp = new boolean[n][n];
        int beg = 0, max = 1;
        for(int i = 0; i < n; i++){
            dp[i][i] = true;
        }
        for(int i = 0; i < n - 1; i++){
            if(s.charAt(i) == s.charAt(i + 1)){
                dp[i][i + 1] = true;
                if(max < 2){
                    beg = i;
                    max = 2;
                }
            }
        }
        for(int l = 3; l <= n; l++){
            for(int i = 0; i < n - l + 1; i++){
                if(s.charAt(i) == s.charAt(i + l - 1) && dp[i + 1][i + l - 2]){
                    dp[i][i + l - 1] = true;
                    if(max < l){
                        max = l;
                        beg = i;
                    }
                }
            }
        }
        return s.substring(beg, beg + max);
    }
}
```

---

## 📝 Explanation of Code

1. Initialize `dp[i][i]` to `true` → single chars are palindromes.
2. For substrings of length 2, mark `dp[i][i+1] = true` if both chars match.
3. For longer substrings, check:
   - `s[i] == s[j]` and `dp[i+1][j-1]` must be true.
   - If true, update starting index and length.
4. Return substring from `beg` with length `max`.

---

> Made with ❤️ by Milan Haria
