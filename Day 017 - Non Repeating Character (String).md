<h1 align="center">🔍 Non Repeating Character 🔍</h1>

---

## 🧩 Problem Statement

Given a string `s` consisting of lowercase English letters, the task is to return the **first non-repeating character** in the string. If there is no non-repeating character, return `$`. When `$` is returned, the driver code will output `-1`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s = "geeksforgeeks"
```

**Output:**  
```
'f'
```

**Explanation:**  
In the given string, the first character that does not repeat is `'f'`.

---

### ✅ Example 2:
**Input:**  
```
s = "racecar"
```

**Output:**  
```
'e'
```

**Explanation:**  
In the given string, the character `'e'` is the only character that does not repeat.

---

### ✅ Example 3:
**Input:**  
```
s = "aabbccc"
```

**Output:**  
```
-1
```

**Explanation:**  
All the characters in the given string are repeating, so there is no non-repeating character.

---

## 🧠 Approach

To solve the problem, we can take the following approach:

1. **Iterate through the string**:
   - Maintain a boolean array `visited` to keep track of the characters we’ve already checked.
2. **Check for Non-Repeating Character**:
   - For each character in the string, check if it is repeating. This can be done by searching for the next occurrence of the character using `indexOf()`.
   - If a character is found to be non-repeating, return it immediately.
3. **Return Default Character**:
   - If no non-repeating character is found after checking the entire string, return `$`.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                               |
|------------------|-----------|-------------------------------------------|
| 🕒 Time           | `O(n²)` | For each character, `indexOf()` is called, which is `O(n)` for each character. Hence, overall time complexity is `O(n²)`. |
| 📦 Space          | `O(1)` | We are using a fixed size array of size 26 for lowercase English letters. |

---

## 🎯 Constraints

- `1 ≤ s.size() ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    static char nonRepeatingChar(String s) {
        int n = s.length();
        boolean[] visited = new boolean[26];
        for(int i = 0; i < n; i++){
            if(!visited[s.charAt(i) - 'a']){
                char c = s.charAt(i);
                visited[c - 'a'] = true;
                if(s.indexOf(c, i + 1) == -1){
                    return c;
                }
            }
        }
        return '$';
    }
}
```

---


> Made with ❤️ by Milan Haria
