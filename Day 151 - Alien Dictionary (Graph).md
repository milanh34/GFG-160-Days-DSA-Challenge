<h1 align="center">👽 Alien Dictionary 👽</h1>

---

## 📝 Problem Statement
You are given an array of strings `words[]` from an **alien dictionary** where the words are sorted lexicographically according to the rules of the alien language.  
Your task is to determine the **order of characters** in this alien language.

- If multiple valid orders exist, return any one of them.  
- If the order is invalid or contradictory, return an empty string `""`.

A string `a` is lexicographically smaller than a string `b` if:  
- At the first differing position, the character in `a` appears earlier in the alien dictionary order than the corresponding character in `b`.  
- If all characters of the shorter word match the beginning of the longer word, the shorter word is considered smaller.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
words = ["baa", "abcd", "abca", "cab", "cad"]
```

**Output:**
```
"bdac"
```

**Explanation:**
- "baa" vs "abcd" → `b` before `a`
- "abcd" vs "abca" → `d` before `a`
- "abca" vs "cab" → `a` before `c`
- "cab" vs "cad" → `b` before `d`  
Valid ordering: **"bdac"**

---

### ✅ Example 2:

**Input:**
```
words = ["caa", "aaa", "aab"]
```

**Output:**
```
"cab"
```

**Explanation:**
- "caa" vs "aaa" → `c` before `a`
- "aaa" vs "aab" → `a` before `b`  
Valid ordering: **"cab"**

---

### ✅ Example 3:
**Input:**
```
words = ["ab", "cd", "ef", "ad"]
```
**Output:**
```
""
```
**Explanation:**  
Contradiction arises:  
- "ab" vs "ef" → `a` before `e`  
- "ef" vs "ad" → `e` before `a`  
Forms a cycle, so **no valid order exists**.

---

## 🧠 Approach

### Topological Sort (Kahn's Algorithm)

1. **Build Graph**  
   - Compare each consecutive pair of words.  
   - Find first differing character → create edge (u → v).  
   - If word A is prefix of word B but longer, return `""`.

2. **In-degree Array**  
   - Track number of incoming edges for each character.

3. **Topological Sort**  
   - Start with characters having `inDegree = 0`.  
   - Use a queue to process characters.  
   - Decrease neighbors’ `inDegree`.  
   - Append processed characters to result.

4. **Cycle Check**  
   - If some nodes remain unprocessed (`inDegree > 0`), return `""`.

---

## ⏱️ Time & Space Complexity
| Complexity | Value | Description |
|------------|-------|-------------|
| Time       | O(N * L + 26 + E) | N = words, L = avg word length, E = edges |
| Space      | O(26 + E) | Adjacency list, in-degree array, visited set |

---

## 🎯 Constraints
- 1 ≤ `words.length` ≤ 500  
- 1 ≤ `words[i].length` ≤ 100  
- `words[i]` consists only of lowercase English letters  

---

## 💻 Code
```java
class Solution {
    public String findOrder(String[] words) {
        int n = words.length;
        List<List<Integer>> adj = new ArrayList<>();
        int[] inDegree = new int[26];
        boolean[] visited = new boolean[26];
        for(int i = 0; i < 26; i++){
            adj.add(new ArrayList<>());
        }
        for(String s: words){
            for(char c: s.toCharArray()){
                visited[c - 'a'] = true;
            }
        }
        for(int i = 0; i < n - 1; i++){
            String a = words[i], b = words[i + 1];
            int j = 0, m = Math.min(a.length(), b.length());
            while(j < m && a.charAt(j) == b.charAt(j)){
                j++;
            }
            if(j == m && a.length() > b.length()){
                return "";
            }
            if(j < m){
                adj.get(a.charAt(j) - 'a').add(b.charAt(j) - 'a');
                inDegree[b.charAt(j) - 'a']++;
            }
        }
        Queue<Integer> queue = new LinkedList<>();
        for(int i = 0; i < 26; i++){
            if(visited[i] && inDegree[i] == 0){
                queue.offer(i);
            }
        }
        StringBuilder ans = new StringBuilder();
        while(!queue.isEmpty()){
            int a = queue.poll();
            ans.append((char)(a + 'a'));
            for(int i: adj.get(a)){
                inDegree[i]--;
                if(inDegree[i] == 0){
                    queue.offer(i);
                }
            }
        }
        for(int i = 0; i < 26; i++){
            if(visited[i] && inDegree[i] > 0){
                return "";
            }
        }
        return ans.toString();
    }
}
```

---

## 📝 Explanation of Code

1. **Graph Construction**: Compare adjacent words to build precedence edges.  
2. **Prefix Handling**: Detect invalid ordering if a longer word comes before its prefix.  
3. **Topological Sort**: Use BFS (Kahn’s algorithm) with in-degree to build order.  
4. **Cycle Detection**: If some nodes remain unprocessed, return `""`.  
5. **Return Result**: String representing valid alien dictionary order.

---

> Made with ❤️ by Milan Haria
