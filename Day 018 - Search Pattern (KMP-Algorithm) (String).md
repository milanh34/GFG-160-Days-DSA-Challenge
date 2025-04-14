<h1 align="center">🔍 Search Pattern (KMP Algorithm) 🔍</h1>

---

## 🧩 Problem Statement

Given two strings:
- `txt`: The text string.
- `pat`: The pattern string.

The task is to print the indexes of all occurrences of the pattern string in the text string using **0-based indexing**.

If the pattern does not appear in the text, return an empty list.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
txt = "abcab", pat = "ab"
```

**Output:**  
```
[0, 3]
```

**Explanation:**  
The pattern `"ab"` occurs twice in the text `"abcab"`, once starting at index `0` and again starting at index `3`.

---

### ✅ Example 2:
**Input:**  
```
txt = "abesdu", pat = "edu"
```

**Output:**  
```
[]
```

**Explanation:**  
The pattern `"edu"` is not present in the string `"abesdu"`, so the result is an empty list.

---

### ✅ Example 3:
**Input:**  
```
txt = "aabaacaadaabaaba", pat = "aaba"
```

**Output:**  
```
[0, 9, 12]
```

**Explanation:**  
The pattern `"aaba"` occurs three times in the text `"aabaacaadaabaaba"`, at indices `0`, `9`, and `12`.

---

## 🧠 Approach

### KMP Algorithm:

The **Knuth-Morris-Pratt (KMP)** algorithm is a string matching algorithm that improves the efficiency of searching by avoiding unnecessary comparisons.

- **Preprocessing Step**: Create a "partial match" table (also known as the **prefix table** or **LPS (Longest Prefix Suffix)** array) to store the lengths of the longest prefix which is also a suffix for each substring.
- **Matching Step**: Use the LPS array to skip over unnecessary comparisons when a mismatch happens.

However, in this solution, we use a simpler approach to demonstrate string matching:

1. **Find all occurrences of the pattern**:
   - Use `indexOf()` to find the first occurrence of the pattern in the text.
   - Keep searching for the pattern starting from the next character after the last found occurrence until no more matches are found.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                               |
|------------------|-----------|-------------------------------------------|
| 🕒 Time           | `O(n + m)` | For each match, we search from the current index onwards. In the worst case, this is a linear search for each occurrence. |
| 📦 Space          | `O(1)` | We are only storing the result indices. |

---

## 🎯 Constraints

- `1 ≤ txt.size() ≤ 10⁶`
- `1 ≤ pat.size() < txt.size()`
- Both strings consist of lowercase English alphabets.

---

## 💻 Code

```java
class Solution {
    ArrayList<Integer> search(String pat, String txt) {
        ArrayList<Integer> ans = new ArrayList<>();
        int idx = txt.indexOf(pat);
        if(idx != -1){
            while(idx != -1){
                ans.add(idx);
                idx = txt.indexOf(pat, idx + 1);
            }
        }
        return ans;
    }
}
```

---

## 📝 Notes

- **Index Search**: The solution uses the `indexOf()` function to find the occurrences of the pattern. This function efficiently finds the first occurrence and can be used repeatedly with an offset to find subsequent matches.
- **KMP Complexity**: While this approach does not implement the full KMP algorithm, it is simple and works well for the problem constraints. For larger datasets, implementing the KMP algorithm would reduce time complexity to `O(n + m)`.

---

> Made with ❤️ by Milan Haria
