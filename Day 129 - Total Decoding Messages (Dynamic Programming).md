<h1 align="center">🔐 Total Decoding Messages 🔐</h1>

---

## 📝 Problem Statement

Given a string `digits` containing only digit characters (`'0'` to `'9'`), determine the **total number of ways** it can be decoded into alphabets using the following mapping:

```
'A' -> 1, 'B' -> 2, ..., 'Z' -> 26
```

> Leading zeros and invalid numbers like "06" are not valid encodings.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
digits = "123"
```

**Output:**  
```
3
```

**Explanation:**  
There are three valid ways to decode:
- "1 2 3" → "A B C"
- "12 3" → "L C"
- "1 23" → "A W"

---

### ✅ Example 2:

**Input:**  
```
digits = "90"
```

**Output:**  
```
0
```

**Explanation:**  
- No valid decoding exists.
- '90' is not a valid code (no letter maps to '90').

---

### ✅ Example 3:

**Input:**  
```
digits = "05"
```

**Output:**  
```
0
```

**Explanation:**  
- Starts with '0', which cannot be decoded.
- "05" is invalid, as '0' cannot be mapped and leading zeros are disallowed.

---

## 🧠 Approach

We use a dynamic programming approach with two variables to keep track of the decoding ways:

1. **Base Cases:**
   - If the first character is '0', return 0.
   - Set `prev1 = 1` and `prev2 = 1` for DP initialization.

2. **Transition:**
   - For each index `i` from 1 to n-1:
     - If `digits[i]` is not '0', then current ways = `prev1`.
     - If the two-digit number from `digits[i-1]` to `digits[i]` is valid (<=26), add `prev2` to current ways.

3. **Return:** Final value of `prev1`, which stores the total number of decodings.

---

## ⏱️ Time and Space Complexity

| Complexity | Value     | Description                           |
|------------|-----------|---------------------------------------|
| Time       | O(N)      | Traverse the string once              |
| Space      | O(1)      | Only constant extra variables used    |

---

## 🎯 Constraints

- 1 ≤ `digits.length` ≤ 10³  
- `digits` consists only of digits `'0'` to `'9'`

---

## 💻 Code

```java
class Solution {
    public int countWays(String digits) {
        if(digits.charAt(0) == '0'){
            return 0;
        }
        int n = digits.length(), prev1 = 1, prev2 = 1;
        for(int i = 1; i < n; i++){
            int curr = digits.charAt(i) == '0' ? 0 : prev1;
            if(digits.charAt(i - 1) != '0' && Integer.parseInt(digits.substring(i - 1, i + 1)) < 27){
                curr += prev2;
            }
            prev2 = prev1;
            prev1 = curr;
        }
        return prev1;
    }
}
```

---

## 📝 Explanation of Code

1. **Check Invalid Start:**  
   - If the string starts with `'0'`, it's invalid. Return `0`.

2. **Initialize Two Variables:**  
   - `prev1` and `prev2` hold the number of ways to decode up to the current and previous characters.

3. **Loop Through the String:**  
   - If the current character is not `'0'`, it contributes to the decoding → take `prev1`.
   - If the two-digit number is between 10 and 26 (inclusive), add `prev2` to ways.

4. **Update DP Variables:**  
   - Shift `prev1` and `prev2` forward for the next character.

---

> Made with ❤️ by Milan Haria
