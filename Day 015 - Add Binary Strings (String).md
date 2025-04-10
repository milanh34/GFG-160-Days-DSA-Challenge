<h1 align="center">💻 Add Binary Strings 💻</h1>

---

## 🧩 Problem Statement

Given two binary strings `s1` and `s2` consisting of only `0`s and `1`s, **find the resultant binary string** after adding the two binary strings.

### Key Points:

1. The input strings may contain **leading zeros**.
2. The output string **should not** have any leading zeros.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s1 = "1101", s2 = "111"
```

**Output:**  
```
10100
```

**Explanation:**  
```
  1101
+  111
-------
  10100
```
The sum of the binary strings `1101` (13 in decimal) and `111` (7 in decimal) results in `10100` (20 in decimal).

---

### ✅ Example 2:
**Input:**  
```
s1 = "00100", s2 = "010"
```

**Output:**  
```
110
```

**Explanation:**  
```
   100
+   10
------
   110
```
The sum of `00100` (4 in decimal) and `010` (2 in decimal) results in `110` (6 in decimal).

---

## 🧠 Approach

To solve the problem:

1. **Strip Leading Zeros**: We first strip the leading zeros from both binary strings.
2. **Addition with Carry**: We then perform the binary addition from right to left, similar to how manual binary addition works:
   - Compare corresponding bits from `s1` and `s2`.
   - Add the bits along with any carry.
   - If the sum is `0`, append `0` to the result; if the sum is `1`, append `1`; and if the sum is `2` or `3`, handle the carry and append accordingly.
3. **Handle Remaining Bits**: If one string is longer, continue the addition with the remaining bits from the longer string.
4. **Final Carry**: If there is any carry left after the main addition, append it to the result.

Finally, return the resulting string after removing any leading zeros.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                                |
|------------------|-----------|--------------------------------------------|
| 🕒 Time           | `O(max(n1, n2))` | We traverse both strings once, where `n1` and `n2` are the lengths of `s1` and `s2`. |
| 📦 Space          | `O(max(n1, n2))` | The space required to store the result string. |

---

## 🎯 Constraints

- `1 ≤ s1.size(), s2.size() ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    public String addBinary(String s1, String s2) {
        StringBuilder sb = new StringBuilder();
        int i = 0;
        for(char c: s1.toCharArray()){
            if(c != '1'){
                i++;
            } else{
                break;
            }
        }
        s1 = s1.substring(i, s1.length());
        i = 0;
        for(char c: s2.toCharArray()){
            if(c != '1'){
                i++;
            } else{
                break;
            }
        }
        s2 = s2.substring(i, s2.length());
        i = 0;
        int n1 = s1.length() - 1, n2 = s2.length() - 1;
        boolean carry = false;
        while(n1 >= 0 && n2 >= 0){
            char a = s1.charAt(n1), b = s2.charAt(n2);
            if(a == '0' && b == '0'){
                if(carry){
                    sb.insert(0, 1);
                    carry = false;
                    i = 0;
                } else{
                    sb.insert(0, 0);
                    i++;
                }
            } else if((a == '0' && b == '1') || (a == '1' && b == '0')){
                if(carry){
                    sb.insert(0, 0);
                    i++;
                } else{
                    sb.insert(0, 1);
                    i = 0;
                }
            } else{
                if(carry){
                    sb.insert(0, 1);
                    i = 0;
                } else{
                    sb.insert(0, 0);
                    carry = true;
                    i++;
                }
            }
            n1--;
            n2--;
        }
        while(n1 >= 0){
            if(carry){
                if(s1.charAt(n1) == '0'){
                    sb.insert(0, 1);
                    carry = false;
                    i = 0;
                } else{
                    sb.insert(0, 0);
                    i++;
                }
            } else{
                if(s1.charAt(n1) == '0'){
                    sb.insert(0, 0);
                    i++;
                } else{
                    sb.insert(0, 1);
                    i = 0;
                }
            }
            n1--;
        }
        while(n2 >= 0){
            if(carry){
                if(s2.charAt(n2) == '0'){
                    sb.insert(0, 1);
                    carry = false;
                    i = 0;
                } else{
                    sb.insert(0, 0);
                    i++;
                }
            } else{
                if(s2.charAt(n2) == '0'){
                    sb.insert(0, 0);
                    i++;
                } else{
                    sb.insert(0, 1);
                    i = 0;
                }
            }
            n2--;
        }
        if(carry){
            sb.insert(0, 1);
            i = 0;
        }
        return sb.substring(i, sb.length()).toString();
    }
}
```

---


> Made with ❤️ by Milan Haria
