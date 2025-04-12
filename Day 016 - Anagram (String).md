<h1 align="center">🔄 Anagram Check 🔄</h1>

---

## 🧩 Problem Statement

Given two strings `s1` and `s2` consisting of lowercase characters, your task is to check whether the two given strings are **anagrams** of each other or not.

### Definition:
An **anagram** of a string is another string that contains the same characters, but the order of the characters can be different. For example:
- `"act"` and `"tac"` are anagrams of each other.

### Note:
- Strings `s1` and `s2` can only contain lowercase alphabets.
- Both strings `s1` and `s2` are **non-empty**.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s1 = "geeks", s2 = "kseeg"
```

**Output:**  
```
true
```

**Explanation:**  
Both strings have the same characters with the same frequency, so they are anagrams of each other.

---

### ✅ Example 2:
**Input:**  
```
s1 = "allergy", s2 = "allergic"
```

**Output:**  
```
false
```

**Explanation:**  
The characters in both strings are not the same, so they are not anagrams.

---

### ✅ Example 3:
**Input:**  
```
s1 = "g", s2 = "g"
```

**Output:**  
```
true
```

**Explanation:**  
Both strings contain the same character, so they are anagrams of each other.

---

## 🧠 Approach

To check if two strings are anagrams:

1. **Length Check**: If the strings `s1` and `s2` have different lengths, they cannot be anagrams. Return `false`.
2. **Frequency Counting**: 
   - Create a frequency array of size 26 (since there are 26 lowercase alphabets).
   - Iterate over the characters in `s1` and update the frequency array.
   - Iterate over the characters in `s2` and decrement the frequency of each character in the array.
3. **Final Check**: After updating the frequency array, if all values are zero, then the strings are anagrams. Otherwise, they are not.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                               |
|------------------|-----------|-------------------------------------------|
| 🕒 Time           | `O(n)` | We traverse each string once where `n` is the length of the strings. |
| 📦 Space          | `O(1)` | We use a constant size array (of size 26) for character frequency. |

---

## 🎯 Constraints

- `1 ≤ s1.size(), s2.size() ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public static boolean areAnagrams(String s1, String s2) {
        if(s1.length() != s2.length()){
            return false;
        }
        int[] freq = new int[26];
        for(char c: s1.toCharArray()){
            freq[c - 'a']++;
        }
        for(char c: s2.toCharArray()){
            freq[c - 'a']--;
        }
        for(int i: freq){
            if(i != 0){
                return false;
            }
        }
        return true;
    }
}
```

---

> Made with ❤️ by Milan Haria
