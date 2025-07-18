<h1 align="center">🔁 Longest Palindromic Subsequence 🔁</h1>

---

## 📝 Problem Statement

Given a string `s`, return the **length of the longest palindromic subsequence**.

- A **subsequence** is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.
- A **palindromic subsequence** reads the same forward and backward.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
s = "bbabcbcab"
```

**Output:**  
```
7
```

**Explanation:**  
The longest palindromic subsequence is `"babcbab"`.

---

### ✅ Example 2

**Input:**  
```
s = "abcd"
```

**Output:**  
```
1
```

**Explanation:**  
Any single character is a palindromic subsequence.

---

### ✅ Example 3

**Input:**  
```
s = "agbdba"
```

**Output:**  
```
5
```

**Explanation:**  
The longest palindromic subsequence is `"abdba"`.

---

## 🧠 Approach

### Key Idea:
- The **longest palindromic subsequence** problem is equivalent to finding the **Longest Common Subsequence (LCS)** of the string and its reverse.

### Steps:
1. Reverse the string `s` to get `r`.
2. Use **Dynamic Programming (DP)** to find the **LCS** of `s` and `r`.
3. The value of the LCS gives the length of the longest palindromic subsequence.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                  |
|------------|-------|------------------------------|
| Time       | O(n²) | DP table of size n x n       |
| Space      | O(n²) | For storing DP values        |

---

## 🎯 Constraints

- `1 ≤ s.size() ≤ 1000`
- The string contains only lowercase letters.

---

## 💻 Code

```java
class Solution {
    public int longestPalinSubseq(String s) {
        String r = new StringBuilder(s).reverse().toString();
        int n = s.length();
        int[][] lcs = new int[n + 1][n + 1];
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= n; j++){
                if(s.charAt(i - 1) == r.charAt(j - 1)){
                    lcs[i][j] = lcs[i - 1][j - 1] + 1;
                } else{
                    lcs[i][j] = Math.max(lcs[i][j - 1], lcs[i - 1][j]);
                }
            }
        }
        return lcs[n][n];
    }
}
```

---

## 📝 Explanation of Code

- Reverse the input string.
- Initialize a DP table lcs[n+1][n+1].
- lcs[i][j] stores the length of the LCS of the first i chars of s and first j chars of r.
- If chars match: lcs[i][j] = lcs[i-1][j-1] + 1.
- If not: take max(lcs[i-1][j], lcs[i][j-1]).
- The last cell of the table (lcs[n][n]) contains the length of the longest palindromic subsequence.
---

> Made with ❤️ by Milan Haria
