<h1 align="center">🔗 Longest String Chain 🔗</h1>

---

## 📝 Problem Statement

You are given an array of **words** where each word consists of **lowercase English letters**.

- A word **A** is a **predecessor** of word **B** **if and only if** you can insert **exactly one letter** anywhere in word A *without changing the order of the other characters* to make it equal to word B.
- A **word chain** is a sequence `[word1, word2, ..., wordk]` where `word1` is a predecessor of `word2`, `word2` is a predecessor of `word3` and so on.
- A **single word** is trivially a word chain of length 1.

**Goal:** Return the **length of the longest possible word chain** using the given words.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
words = ["ba", "b", "a", "bca", "bda", "bdca"]
```

**Output:**  
```
4
```

**Explanation:**  
A possible chain is: `["a" -> "ba" -> "bda" -> "bdca"]`

---

### ✅ Example 2

**Input:**  
```
words = ["abc", "a", "ab"]
```

**Output:**  
```
3
```

**Explanation:**  
A chain is: `["a" -> "ab" -> "abc"]`

---

### ✅ Example 3

**Input:**  
```
words = ["abcd", "dbqca"]
```

**Output:**  
```
1
```

**Explanation:**  
Each word alone is a valid chain of length 1.

---

## 🧠 Approach

1. **Sort** the words by length in ascending order.
2. Use **Dynamic Programming (DP)** with a **HashMap** to store the maximum chain length ending at each word.
3. For each word, **try removing each letter** and see if the resulting word exists in the map.
4. If so, it means this word can extend that chain.
5. Update the max chain length accordingly.

---

## ⏱️ Time and Space Complexity

| Complexity | Value      | Description                              |
|------------|------------|------------------------------------------|
| Time       | O(N * L²)  | For each word, try L possible deletions  |
| Space      | O(N)       | For storing the DP map                   |

Where:
- `N` = total number of words
- `L` = maximum word length (≤ 10)

---

## 🎯 Constraints

- `1 ≤ words.length ≤ 10⁴`
- `1 ≤ words[i].length ≤ 10`
- `words[i]` contains only lowercase English letters

---

## 💻 Code

```java
class Solution {
    public int longestStringChain(String words[]) {
        int ans = 1;
        Arrays.sort(words, (a, b) -> a.length() - b.length());
        Map<String, Integer> map = new HashMap<>();
        for(String s: words){
            map.put(s, 1);
            int m = s.length();
            for(int j = 0; j < m; j++){
                String str = s.substring(0, j) + s.substring(j + 1, m);
                if(map.containsKey(str)){
                    map.put(s, Math.max(map.get(str) + 1, map.get(s)));
                }
            }
            ans = Math.max(ans, map.get(s));
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. Sort the words by length (shorter words processed first).
2. For each word:
   - Initialize its chain length to 1.
   - Try removing each letter to form all possible predecessors.
   - If a predecessor exists, update the current word's chain length.
3. Keep track of the longest chain found.
4. Return the maximum chain length.

---

> Made with ❤️ by Milan Haria
