<h1 align="center">🔄 Strings Rotations of Each Other 🔄</h1>

---

## 📝 Problem Statement

Given two strings `s1` and `s2` of equal length, the task is to check if `s2` is a rotated version of `s1`.

A string `s2` is considered a rotated version of `s1` if it can be obtained by rotating `s1` any number of times (either left or right).

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s1 = "abcd"
s2 = "cdab"
```

**Output:**  
```
true
```

**Explanation:**  
After 2 right rotations, `"abcd"` becomes `"cdab"`. Therefore, `s2` is a rotated version of `s1`.

---

### ✅ Example 2:
**Input:**  
```
s1 = "aab"
s2 = "aba"
```

**Output:**  
```
true
```

**Explanation:**  
After 1 left rotation, `"aab"` becomes `"aba"`. Therefore, `s2` is a rotated version of `s1`.

---

### ✅ Example 3:
**Input:**  
```
s1 = "abcd"
s2 = "acbd"
```

**Output:**  
```
false
```

**Explanation:**  
The strings `"abcd"` and `"acbd"` are not rotations of each other, so the result is `false`.

---

## 🧠 Approach

To check if one string is a rotated version of the other, we can use the following efficient approach:

1. **Concatenate `s1` with itself**:  
   By concatenating `s1` with itself (i.e., `s1 + s1`), we form a new string that contains all possible rotations of `s1` as its substrings. For example, for `s1 = "abcd"`, `s1 + s1 = "abcdabcd"`, which includes `"abcd"`, `"bcda"`, `"cdab"`, and `"dabc"`.

2. **Check if `s2` is a substring of `s1 + s1`**:  
   If `s2` is a rotated version of `s1`, it must appear as a substring of `s1 + s1`.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                               |
|------------------|-----------|-------------------------------------------|
| 🕒 Time          | `O(n)`    | We check if `s2` is a substring of `s1 + s1`, where `n` is the length of the strings. |
| 📦 Space         | `O(n)`    | We create a new string `s1 + s1` for substring search. |

---

## 🎯 Constraints

- `1 ≤ s1.size(), s2.size() ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public static boolean kmp(String t, String p){
        int n = t.length(), m = p.length(), i = 1, len = 0;
        int[] lps = new int[m];
        while(i < m){
            if(p.charAt(i) == p.charAt(len)){
                len++;
                lps[i] = len;
                i++;
            } else{
                if(len != 0){
                    len = lps[len - 1];
                } else{
                    lps[i] = 0;
                    i++;
                }
            }
        }
        i = 0;
        len = 0;
        while(i < n){
            if(t.charAt(i) == p.charAt(len)){
                i++;
                len++;
            }
            if(len == m){
                return true;
            } else if(i < n && p.charAt(len) != t.charAt(i)){
                if(len != 0){
                    len = lps[len - 1];
                } else{
                    i++;
                }
            }
        }
        return false;
    }
    public static boolean areRotations(String s1, String s2) {
        if(s1.length() != s2.length()){
            return false;
        }
        return kmp(s1 + s1, s2);
    }
}
```

---

## 📝 Explanation of Code

- **`kmp` Function**:  
  This is the **Knuth-Morris-Pratt (KMP)** algorithm for substring search. It is used here to check if `s2` is a substring of `s1 + s1`.

- **`areRotations` Function**:  
  This function checks if `s2` is a rotation of `s1` by concatenating `s1` with itself and using the `kmp` function to check if `s2` exists as a substring of `s1 + s1`.

---

## 🧩 Edge Cases

- **Strings of Different Lengths**:  
  If `s1` and `s2` have different lengths, they cannot be rotations of each other. The function returns `false` immediately in this case.

- **Identical Strings**:  
  If `s1` and `s2` are identical, they are trivially rotations of each other, and the function returns `true`.

---

> Made with ❤️ by Milan Haria
