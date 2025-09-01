<h1 align="center">🔍 Missing in Array 🔍</h1>

---

## 📝 Problem Statement

You are given an array **arr[]** of size `n-1` that contains **distinct integers** in the range from `1` to `n` (inclusive).  
This array represents a **permutation of integers from 1 to n with one element missing**.  
Your task is to **find and return the missing element**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
arr = [1, 2, 3, 5]
```
**Output:**
```
4
```
**Explanation:**  
All numbers from 1 to 5 should be present, but `4` is missing.

---

### ✅ Example 2:

**Input:**
```
arr = [8, 2, 4, 5, 3, 7, 1]
```
**Output:**
```
6
```
**Explanation:**  
All numbers from 1 to 8 should be present, but `6` is missing.

---

### ✅ Example 3:

**Input:**
```
arr = [1]
```
**Output:**
```
2
```
**Explanation:**  
Numbers should be from 1 to 2, but `2` is missing.

---

## 🧠 Approach

### Mathematical Formula Method

1. Sum of numbers from `1` to `n` is: `Sum = n * (n + 1) / 2
2. Compute the **sum of given array**.  
3. Subtract array sum from expected sum → gives the **missing element**.

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Description |
|------------|-------|-------------|
| Time       | O(N) | Loop through array once |
| Space      | O(1) | No extra space used |

---

## 🎯 Constraints
- 1 ≤ `arr.length` ≤ 10⁶  
- 1 ≤ `arr[i]` ≤ arr.length + 1  

---

## 💻 Code
```java
class Solution {
    int missingNum(int arr[]) {
        int n = arr.length + 1;
        long sum = 0;
        for(int i: arr){
            sum += i;
        }
        return (int)(((long)n * (n + 1)) / 2 - sum);
    }
}
```

---

## 📝 Explanation of Code

1. Compute **n = arr.length + 1**, because one number is missing.  
2. Calculate **expected sum** using formula.  
3. Subtract **actual sum** of array → result is the missing number.  

---

> Made with ❤️ by Milan Haria
