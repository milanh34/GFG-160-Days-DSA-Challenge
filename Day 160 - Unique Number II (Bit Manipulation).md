<h1 align="center">🔢 Unique Number II 🔢</h1>

---

## 📝 Problem Statement  

You are given an array `arr[]` of size **2*n + 2**, containing positive integers. 

- Out of these numbers, **2*n numbers exist in pairs** (each appears exactly twice).  
- Only **two numbers occur exactly once** and they are **distinct**.  

Your task is to **find those two unique numbers** and return them in **increasing order**.

---

## ✅ Examples  

### ✅ Example 1:

**Input:**  
```
arr = [1, 2, 3, 2, 1, 4]
```
**Output:**  
```
[3, 4]
```
**Explanation:**  
- Numbers `1` and `2` appear twice.  
- Numbers `3` and `4` appear only once.  

---

### ✅ Example 2:

**Input:**  
```
arr = [2, 1, 3, 2]
```
**Output:**  
```
[1, 3]
```
**Explanation:**  
- Numbers `2` appear twice.  
- Numbers `1` and `3` appear only once.  

---

### ✅ Example 3:

**Input:**  
```
arr = [2, 1, 3, 3]
```
**Output:**  
```
[1, 2]
```
**Explanation:**  
- Numbers `3` appear twice.  
- Numbers `1` and `2` appear only once.  

---

## 🧠 Approach  

We use the **XOR Bit Manipulation Trick**:

1. XOR all numbers in the array → `xor = a ^ b` (where `a` and `b` are the two unique numbers).  
2. Find the **rightmost set bit** in `xor`. This bit must be set in one of the unique numbers and unset in the other.  
3. Partition numbers into **two groups** based on this bit:  
   - Group 1: Numbers with this bit = 0.  
   - Group 2: Numbers with this bit = 1.  
4. XOR numbers inside each group → gives the two unique numbers.  
5. Sort them and return as answer.  

---

## ⏱️ Time & Space Complexity  

| Complexity | Value | Description |
|------------|-------|-------------|
| Time       | O(N)  | Single pass for XOR + partition |
| Space      | O(1)  | Only two variables and constants used |

---

## 🎯 Constraints

- 2 ≤ `arr.size()` ≤ 10⁶  
- 1 ≤ `arr[i]` ≤ 5 × 10⁶  
- `arr.size()` is **even**  

---

## 💻 Code  
```java
class Solution {
    public int[] singleNum(int[] arr) {
        int xor = 0;
        int[] ans = new int[2];
        for(int i: arr){
            xor ^= i;
        }
        xor &= -xor;
        for(int i: arr){
            if((i & xor) == 0){
                ans[0] ^= i;
            } else{
                ans[1] ^= i;
            }
        }
        Arrays.sort(ans);
        return ans;
    }
}
```

---

## 📝 Explanation of Code  

1. Compute `xor` of all elements → duplicates cancel out, leaving `xor = a ^ b`.  
2. Find the **rightmost set bit** in `xor` → used to differentiate `a` and `b`.  
3. Partition numbers into two sets and XOR within each → isolates `a` and `b`.  
4. Return `[min(a, b), max(a, b)]`.  

---

> Made with ❤️ by Milan Haria  
