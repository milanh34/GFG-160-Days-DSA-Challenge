<h1 align="center">🔠 Maximize Partitions in a String 🔠</h1>

---

## 📝 Problem Statement
Given a string `s` consisting of lowercase English alphabets,  
find the **maximum number of substrings** that can be formed such that **no two substrings share any common character**.  

You can make zero or more partitions in `s`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
s = "acbbcc"  
```

**Output:**  
```
2  
```

**Explanation:**  
- Partition at index 0 → "a" | "cbbcc"  
- No characters are repeated across substrings.  

---

### ✅ Example 2:

**Input:**  
```
s = "ababcbacadefegdehijhklij"  
```

**Output:**  
```
3  
```

**Explanation:**  
- Partition at index 8 → "ababcbaca" | "defegde" | "hijhklij"  
- No substrings share any character.  

---

### ✅ Example 3:

**Input:**  
```
s = "aaa"  
```

**Output:**  
```
1  
```

**Explanation:**  
- All characters are the same, so no valid partition is possible.  

---

## 🧠 Approach
1. **Record Last Occurrence:**  
   For each character, store its last index in the string.  

2. **Greedy Partitioning:**  
   - Traverse the string and track the farthest last occurrence (`last`) for characters seen so far.  
   - When the current index equals `last`, we can partition here because all characters in this substring appear only within it.

3. **Count Partitions:**  
   Increment count whenever a partition point is found.

---

## ⏱️ Time and Space Complexity
| Complexity | Value  | Description |
|------------|--------|-------------|
| Time       | O(N)   | Single pass to record last positions and one pass to partition |
| Space      | O(1)   | Constant extra space for 26 letters |

---

## 🎯 Constraints
- 1 ≤ `s.length` ≤ 10⁵  
- 'a' ≤ `s[i]` ≤ 'z'  

---

## 💻 Code
```java
class Solution {
    public int maxPartitions(String s) {
        int n = s.length(), ans = 0, last = 0;
        int[] end = new int[26];
        for(int i = 0; i < n; i++){
            end[s.charAt(i) - 'a'] = i;
        }
        for(int i = 0; i < n; i++){
            last = Math.max(last, end[s.charAt(i) - 'a']);
            if(last == i){
                ans++;
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **`end[]`** → Stores the last position of each character in `s`.
- **`last`** → Tracks the farthest right index any character in the current substring can go.
- When `i == last`, the current substring is independent, and we can make a partition.

---

> Made with ❤️ by Milan Haria
