<h1 align="center">🔠 Longest Substring with Distinct Characters 🔠</h1>

---

## 📝 Problem Statement

Given a string `s`, find the length of the **longest substring** that contains **all distinct characters**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
s = "geeksforgeeks"
```

**Output:**  
```
7
```

**Explanation:**  
The longest substring with all distinct characters is `"eksforg"`, which has 7 characters.

---

### ✅ Example 2:

**Input:**  
```
s = "aaa"
```

**Output:**  
```
1
```

**Explanation:**  
All characters are same, so the longest distinct character substring is `"a"` with length 1.

---

### ✅ Example 3:

**Input:**  
```
s = "abcdefabcbb"
```

**Output:**  
```
6
```

**Explanation:**  
The substring `"abcdef"` is the longest one with all distinct characters.

---

## 🧠 Approach

- Use the **sliding window** technique with two pointers (`beg`, `end`) and a frequency array.
- Expand the window to include new unique characters.
- If a repeating character is found, shrink the window from the left until the duplicate is removed.
- Update the answer after each expansion.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                                          |
|------------------|-----------|------------------------------------------------------|
| 🕒 Time          | O(N)      | Traverse each character once                         |
| 📦 Space         | O(1)      | Frequency array of 26 lowercase letters              |

---

## 🎯 Constraints

- 1 ≤ s.length() ≤ 30,000  
- All characters are lowercase English letters.

---

## 💻 Code

```java
class Solution {
    public int longestUniqueSubstr(String s) {
        int n = s.length(), beg = 0, end = 0, ans = 0, unique = 0;
        int[] freq = new int[26];
        while(end < n){
            int j = s.charAt(end) - 'a';
            freq[j]++;
            if(freq[j] == 1){
                unique++;
                end++;
            } else{
                int i = s.charAt(beg) - 'a';
                while(i != j){
                    freq[i]--;
                    unique--;
                    beg++;
                    i = s.charAt(beg) - 'a';
                }
                freq[i]--;
                beg++;
                end++;
            }
            ans = Math.max(ans, unique);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
