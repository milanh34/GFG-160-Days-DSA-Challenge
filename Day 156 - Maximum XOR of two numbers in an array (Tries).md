<h1 align="center">⚡ Maximum XOR of Two Numbers in an Array ⚡</h1>

---

## 📝 Problem Statement

You are given an array **arr[]** of non-negative integers of size `n`.  
Your task is to find the **maximum XOR value** obtainable between any two numbers present in the array.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
arr = [25, 10, 2, 8, 5, 3]
```

**Output:**
```
28
```

**Explanation:**
- The maximum XOR is `25 ^ 5 = 28`.

---

### ✅ Example 2:

**Input:**
```
arr = [1, 2, 3, 4, 5, 6, 7]
```

**Output:**
```
7
```

**Explanation:**
- The maximum XOR is `1 ^ 6 = 7`.

---

## 🧠 Approach

We can solve this problem in **two ways**:

### 1. Brute Force (O(N²)) ✅
- Compare every pair `(i, j)` with `i < j`.
- Compute `arr[i] ^ arr[j]`.
- Keep track of the maximum result.

This works for small constraints, but is inefficient for large arrays.

### 2. Optimized Approach using Trie (O(N * log M)) 🚀
- Build a **bitwise Trie** for all numbers (since XOR is bitwise).  
- Traverse each number and try to maximize XOR by choosing opposite bits from the Trie.  
- This reduces complexity significantly.

---

## ⏱️ Time & Space Complexity

| Approach   | Time Complexity | Space Complexity | Descripttion |
|------------|----------------|------------------|-------------|
| Brute Force | O(N²) | O(1) | Compare all pairs |
| Trie-based  | O(N · log M) | O(N · log M) | Insert numbers into bitwise trie, check max XOR |

Here `M` = maximum number in the array.

---

## 🎯 Constraints
- 2 ≤ `arr.length` ≤ 5 × 10⁴  
- 1 ≤ `arr[i]` ≤ 10⁶  

---

## 💻 Code (Brute Force)
```java
class Solution {
    public int maxXor(int[] arr) {
        int n = arr.length, ans = 0;
        for(int i = 0; i < n; i++){
            for(int j = i + 1; j < n; j++){
                ans = Math.max(ans, arr[i] ^ arr[j]);
            }
        }
        return ans;
    }
}
```

---

## 💻 Code (Optimized using Trie)
```java
class Solution {
    class TrieNode {
        TrieNode[] child = new TrieNode[2];
    }

    private void insert(TrieNode root, int num) {
        TrieNode node = root;
        for(int i = 31; i >= 0; i--){
            int bit = (num >> i) & 1;
            if(node.child[bit] == null){
                node.child[bit] = new TrieNode();
            }
            node = node.child[bit];
        }
    }

    private int getMaxXor(TrieNode root, int num) {
        TrieNode node = root;
        int max = 0;
        for(int i = 31; i >= 0; i--){
            int bit = (num >> i) & 1;
            if(node.child[1 - bit] != null){
                max |= (1 << i);
                node = node.child[1 - bit];
            } else{
                node = node.child[bit];
            }
        }
        return max;
    }

    public int maxXor(int[] arr) {
        TrieNode root = new TrieNode();
        for(int num: arr){
            insert(root, num);
        }
        int ans = 0;
        for(int num: arr){
            ans = Math.max(ans, getMaxXor(root, num));
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code
1. **Brute Force:** Compare every pair with XOR, track maximum.  
2. **Trie-based:**  
   - Insert numbers in bitwise form into Trie.  
   - For each number, traverse Trie preferring the opposite bit at each step to maximize XOR.  
   - Return the highest XOR found.  

The **Trie-based approach** is far more efficient for large inputs.

---

> Made with ❤️ by Milan Haria
