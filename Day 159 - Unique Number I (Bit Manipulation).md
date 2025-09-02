<h1 align="center">✨ Unique Number I ✨</h1>

---

## 📝 Problem Statement

You are given an **unsorted array** `arr[]` of positive integers where **every number occurs exactly twice** except for **one unique number** which appears **only once**.  
Your task is to **find the unique number**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
arr = [1, 2, 1, 5, 5]
```
**Output:**
```
2
```
**Explanation:**  
All numbers occur twice except `2`, hence the answer is `2`.

---

### ✅ Example 2:

**Input:**
```
arr = [2, 30, 2, 15, 20, 30, 15]
```
**Output:**
```
20
```
**Explanation:**  
All numbers occur twice except `20`, hence the answer is `20`.

---

## 🧠 Approach

### XOR Trick
- XOR of a number with itself is `0`.  
- XOR of a number with `0` is the number itself.  
- Thus, XORing all numbers will cancel out the duplicates and leave the unique number.

**Steps:**
1. Initialize `ans = 0`.  
2. Iterate through the array and do `ans ^= arr[i]`.  
3. After loop ends, `ans` will be the unique number.

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Description |
|------------|-------|-------------|
| Time       | O(N) | Traverse array once |
| Space      | O(1) | Constant extra space |

---

## 🎯 Constraints

- 1 ≤ `arr.size()` ≤ 10⁶  
- 0 ≤ `arr[i]` ≤ 10⁹  

---

## 💻 Code
```java
class Solution {
    public int findUnique(int[] arr) {
        int ans = 0;
        for(int i: arr){
            ans ^= i;
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. Start with `ans = 0`.  
2. XOR each element of array with `ans`.  
   - If a number appears twice, it cancels out (`x ^ x = 0`).  
   - Only the unique number remains.  
3. Return `ans` as the final answer.  

---

> Made with ❤️ by Milan Haria
