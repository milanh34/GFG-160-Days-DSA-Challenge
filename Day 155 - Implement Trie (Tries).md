<h1 align="center">📖 Implement Trie 📖</h1>

---

## 📝 Problem Statement

You need to implement a **Trie (Prefix Tree)** data structure that supports the following operations:

1. **Insert a word** into the Trie.  
2. **Search for a word** in the Trie.  
3. **Check if a word is a prefix** of any word in the Trie.

---

## ✅ Examples

### ✅ Example 1

**Input:**
```
query = [[1, "abcd"], [1, "abc"], [1, "bcd"], [2, "bc"], [3, "bc"], [2, "abc"]]
```

**Output:**
```
[false, true, true]
```

**Explanation:**
- `"bc"` does **not** exist as a complete word → `false`
- `"bc"` is a prefix of `"bcd"` → `true`
- `"abc"` exists as a complete word → `true`

---

### ✅ Example 2

**Input:**
```
query = [[1, "gfg"], [1, "geeks"], [3, "fg"], [3, "geek"], [2, "for"]]
```

**Output:**
```
[false, true, false]
```

**Explanation:**
- `"for"` does **not** exist in the Trie → `false`
- `"fg"` is not a valid prefix → `false`
- `"geek"` is a prefix of `"geeks"` → `true`

---

## 🧠 Approach

We use a **TrieNode structure** with:  
- An array `child[26]` to store links for each character.  
- A boolean `isEnd` to mark the **end of a word**.  

### Operations:
1. **Insert(word):**
   - Traverse character by character, creating new nodes if needed.  
   - Mark last node’s `isEnd = true`.  

2. **Search(word):**
   - Traverse character by character.  
   - If any node is missing → return `false`.  
   - Return `true` only if `isEnd = true`.  

3. **isPrefix(word):**
   - Similar traversal as search.  
   - If traversal succeeds, return `true` (even if `isEnd = false`).  

---

## ⏱️ Time & Space Complexity

| Operation | Time Complexity | Space Complexity | Description |
|-----------|-----------------|------------------|-------------|
| Insert    | O(L) | O(26 × L) | Each character is processed once, new nodes created only when needed |
| Search    | O(L) | O(1) | Each character is checked once, no extra space used |
| isPrefix  | O(L) | O(1) | Each character is checked once, stops at mismatch |

---

## 🎯 Constraints
- 1 ≤ `query.size` ≤ 10⁴  
- 1 ≤ `word.length` ≤ 10³  

---

## 💻 Code
```java
class Trie {
    
    public TrieNode root;

    public class TrieNode{
        TrieNode[] child;
        boolean isEnd;
        TrieNode(){
            child = new TrieNode[26];
            isEnd = false;
        }
    }

    public Trie() {
        root = new TrieNode();
    }

    public void insert(String word) {
        TrieNode node = root;
        for(char c: word.toCharArray()){
            if(node.child[c - 'a'] == null){
                node.child[c - 'a'] = new TrieNode();
            }
            node = node.child[c - 'a'];
        }
        node.isEnd = true;
    }

    public boolean search(String word) {
        TrieNode node = root;
        for(char c: word.toCharArray()){
            if(node.child[c - 'a'] == null){
                return false;
            }
            node = node.child[c - 'a'];
        }
        return node.isEnd;
    }

    public boolean isPrefix(String word) {
        TrieNode node = root;
        for(char c: word.toCharArray()){
            if(node.child[c - 'a'] == null){
                return false;
            }
            node = node.child[c - 'a'];
        }
        return true;
    }
}
```

---

## 📝 Explanation of Code
1. **TrieNode class** stores children (26 possible chars) and `isEnd`.  
2. **Insert(word):** Iteratively adds each character, ensuring path exists.  
3. **Search(word):** Traverses path; only returns true if last node marks end of word.  
4. **isPrefix(word):** Traverses path; returns true if path exists, regardless of end.  

---

> Made with ❤️ by Milan Haria
