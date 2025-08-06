<h1 align="center">🧩 Word Break 🧩</h1>

---

## 📝 Problem Statement

You are given a string `s` and a list `dictionary[]` of words.  
Your task is to determine whether `s` can be **formed by concatenating one or more words** from `dictionary[]`.

> Words from the dictionary can be used **any number of times** and in **any order**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
s = "ilike"
dictionary = ["i", "like", "gfg"]
```

**Output:**
```
true
```

**Explanation:**  
We can split the string as `"i like"` which are both present in the dictionary.

---

### ✅ Example 2:

**Input:**
```
s = "ilikegfg"
dictionary = ["i", "like", "man", "india", "gfg"]
```

**Output:**
```
true
```

**Explanation:**  
Valid segmentation: `"i like gfg"`

---

### ✅ Example 3:

**Input:**
```
s = "ilikemangoes"
dictionary = ["i", "like", "man", "india", "gfg"]
```

**Output:**
```
false
```

**Explanation:**  
No valid segmentation using only dictionary words.

---

## 🧠 Approach

We use **Dynamic Programming** to check if `s` can be segmented:

### Steps:
1. Convert `dictionary[]` to a `HashSet` for O(1) lookup.
2. Track the maximum length of any word in the dictionary to reduce unnecessary checks.
3. Use a `dp[]` array where:
   - `dp[i] = true` means substring `s[0...i-1]` can be segmented.
4. For each index `i` in `s`:
   - If `dp[i] == false`, skip
   - Try all substrings of length ≤ `maxWordLen` from `i` onward
   - If substring is in dictionary, set `dp[i + j] = true`

---

## ⏱️ Time and Space Complexity

| Complexity | Value            | Description                                |
|------------|------------------|--------------------------------------------|
| Time       | O(N × L)         | N = length of string, L = max word length  |
| Space      | O(N + D)         | N = DP array, D = dictionary HashSet       |

---

## 🎯 Constraints

- 1 ≤ `s.length()` ≤ 3000  
- 1 ≤ `dictionary.length` ≤ 1000  
- 1 ≤ `dictionary[i].length()` ≤ 100  

---

## 💻 Code

```java
class Solution {
    public boolean wordBreak(String s, String[] dictionary) {
        int n = s.length(), max = 0;
        boolean[] dp = new boolean[n + 1];
        Set<String> set = new HashSet<>();
        for(String str: dictionary){
            set.add(str);
            max = Math.max(max, str.length());
        }
        dp[0] = true;
        for(int i = 0; i < n; i++){
            if(!dp[i]){
                continue;
            }
            for(int j = 1; j <= max && i + j <= n; j++){
                if(set.contains(s.substring(i, i + j))){
                    dp[i + j] = true;
                }
            }
        }
        return dp[n];
    }
}
```

---

## 📝 Explanation of Code

- We use a `boolean dp[]` to represent whether `s[0...i-1]` can be formed.
- Start from index 0, and for every reachable index `i`, try adding dictionary words.
- If `s.substring(i, i + j)` is in the dictionary, mark `dp[i + j]` as `true`.
- Finally, if `dp[n] == true`, it means the full string can be formed.

---

> Made with ❤️ by Milan Haria
