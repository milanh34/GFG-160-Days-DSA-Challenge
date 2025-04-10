<h1 align="center">🔢 Implement Atoi 🔢</h1>

---

## 🧩 Problem Statement

Given a string `s`, your task is to **convert it into an integer** without using any **built-in conversion methods**.

---

## ✅ Conversion Rules

1. **Skip leading whitespaces.**
2. **Check for optional '+' or '-' sign.** Default is positive.
3. **Convert digits to integer** until a non-digit character or end of string is reached.
4. **Ignore leading zeros.**
5. If no digits are found, return `0`.
6. Clamp the value within the **32-bit signed integer range**:
   - If value > `2³¹ - 1`, return `2147483647`.
   - If value < `-2³¹`, return `-2147483648`.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
s = "-123"
```

**Output:**  
```
-123
```

**Explanation:**  
The string `"-123"` represents the integer `-123`, so the function returns `-123`.

---

### ✅ Example 2:
**Input:**  
```
s = "  -"
```

**Output:**  
```
0
```

**Explanation:**  
After skipping the leading whitespace, the function encounters a `-` but no digits follow. Hence, no valid integer can be formed, and the function returns `0`.

---

### ✅ Example 3:
**Input:**  
```
s = " 1231231231311133"
```

**Output:**  
```
2147483647
```

**Explanation:**  
The number exceeds the 32-bit signed integer limit (`2³¹ - 1`). The function returns `2147483647` because it is the maximum possible value for a 32-bit signed integer.

---

### ✅ Example 4:
**Input:**  
```
s = "-999999999999"
```

**Output:**  
```
-2147483648
```

**Explanation:**  
The value `-999999999999` is smaller than the minimum value for a 32-bit signed integer (`-2³¹`). The function returns `-2147483648` because it is the smallest possible value for a 32-bit signed integer.

---

### ✅ Example 5:
**Input:**  
```
s = "  -0012gfg4"
```

**Output:**  
```
-12
```

**Explanation:**  
After skipping leading whitespaces and processing the `-` sign, the function reads `0012` as the number `12`. The non-digit character `g` is encountered afterward, so the function stops reading further. It returns `-12`.

---

## 🧠 Approach

1. Use a flag `neg` to track negativity.
2. Use a flag `numAppeared` to detect when a number starts.
3. Skip leading whitespaces.
4. On seeing `-` or `+`, set sign.
5. For digits, convert the character by multiplying the previous result by 10 and adding the current digit.
6. Before adding, check if the result exceeds the integer range using a temporary double.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                                |
|------------------|-----------|--------------------------------------------|
| 🕒 Time           | `O(n)`    | One pass through the string                |
| 📦 Space          | `O(1)`    | Constant extra space                       |

---

## 🎯 Constraints

- `1 ≤ |s| ≤ 15`

---

## 💻 Code

```java
class Solution {
    public int myAtoi(String s) {
        boolean neg = false;
        Boolean numAppeared = null;
        int ans = 0, i = 1;
        for(char c: s.toCharArray()){
            if(c == ' '){
                if(numAppeared == null){
                    continue;
                } else if(numAppeared == true){
                    break;
                }
            } else if(c == '-'){
                if(numAppeared == null){
                    neg = true;
                } else if(numAppeared == true){
                    break;
                }
            } else if(c >= '0' && c <= '9'){
                if(numAppeared == null){
                    numAppeared = true;
                }
                double a = (double)ans * 10 + (c - '0');
                if(a > (double)2147483647 + 1 && neg){
                    return -2147483648;
                } else if(a > (double)2147483647 && !neg){
                    return 2147483647;
                }
                ans = (int)a;
            } else{
                break;
            }
        }
        return neg ? -ans : ans;
    }
}
```

---


> Made with ❤️ by Milan Haria
