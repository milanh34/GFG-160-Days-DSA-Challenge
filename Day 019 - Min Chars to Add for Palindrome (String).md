<h1 align="center">🧩 Min Chars to Add for Palindrome 🧩</h1>

---

## 📝 Problem Statement

Given a string `s`, the task is to find the minimum number of characters that need to be added at the front of the string to make it a palindrome.

A **palindrome** is a string that reads the same forward and backward.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s = "abc"
```

**Output:**  
```
2
```

**Explanation:**  
To make the string `"abc"` a palindrome, we can add `'b'` and `'c'` at the front to get `"cbabc"`, which is a palindrome.

---

### ✅ Example 2:
**Input:**  
```
s = "aacecaaaa"
```

**Output:**  
```
2
```

**Explanation:**  
To make the string `"aacecaaaa"` a palindrome, we can add two `'a'`s at the front to get `"aaaacecaaaa"`, which is a palindrome.

---

## 🧠 Approach

We can approach this problem using the concept of **longest prefix which is a palindrome**:

1. **Matching Prefix and Suffix**: 
   We need to identify the longest prefix of the string `s` that matches a suffix. If a part of the string is already a palindrome, we don't need to add characters to it. The remaining characters of the string will need to be added in reverse order at the front to complete the palindrome.

2. **Algorithm**:
   - Iterate through the string starting from the end and find the longest substring from the start that matches a suffix.
   - The characters after this matching part must be added at the front in reverse order to make the string a palindrome.

3. **Steps**:
   - Find the first position `i` from the end of the string where the substring `s[0..i]` matches a suffix of `s`.
   - The characters from `s[i+1..n-1]` will need to be added in reverse at the front of the string.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                               |
|------------------|-----------|-------------------------------------------|
| 🕒 Time          | `O(n)`    | We are only iterating over the string once to find the matching prefix and suffix. |
| 📦 Space         | `O(n)`    | We are using additional space for the substring and string manipulation. |

---

## 🎯 Constraints

- `1 ≤ s.size() ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    public static String getPalindrome(String s){
        int n = s.length(), left = 0;
        for(int i = n - 1; i >= 0; i--){
            if(s.charAt(i) == s.charAt(left)){
                left++;
            }
        }
        if(left == n){
            return s;
        }
        String a = s.substring(left, n);
        StringBuilder sb = new StringBuilder(a).reverse();
        return sb.append(getPalindrome(s.substring(0, left))).append(a).toString();
    }
    public static int minChar(String s) {
        String str = getPalindrome(s);
        return str.length() - s.length();
    }
}
```

---

## 📝 Explanation of Code

- **`getPalindrome` Function**:  
  This function recursively finds the longest palindromic prefix and suffix, then constructs the palindrome by adding the reversed substring at the front.

- **`minChar` Function**:  
  This function calculates how many characters need to be added by comparing the length of the palindrome created by `getPalindrome` with the original string length.

---

## 🧩 Edge Cases

- **Already Palindrome**:  
  If the string is already a palindrome, the result will be `0` as no characters need to be added.
  
- **String with No Palindromic Prefix**:  
  In the worst case, all characters except the first one will need to be added at the front.

---

> Made with ❤️ by Milan Haria
