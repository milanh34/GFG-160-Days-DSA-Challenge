<h1 align="center">🔁 Find Only Repetitive Element from 1 to n-1 🔁</h1>

---

## 📝 Problem Statement

You are given an array **arr[]** of size `n`, containing numbers from `1` to `n-1` in **random order**.  
The array has **exactly one repetitive element**. Your task is to **find that element**.

> It is guaranteed that **one element is repeated**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
arr = [1, 3, 2, 3, 4]
```

**Output:**
```
3
```

**Explanation:**  
The number `3` is repeated.

---

### ✅ Example 2:

**Input:**
```
arr = [1, 5, 1, 2, 3, 4]
```

**Output:**
```
1
```

**Explanation:**  
The number `1` is repeated.

---

### ✅ Example 3:

**Input:**
```
arr = [1, 1]
```

**Output:**
```
1
```

**Explanation:**  
Array size is `2`, both elements are `1`, hence `1` is the repeated element.

---

## 🧠 Approach

### Mathematical Formula Approach

1. Numbers from `1` to `n-1` have a known **sum formula**: `Sum = n * (n - 1) / 2`
2. The given array has one extra duplicate, so its **sum will be larger**.  
3. Subtract expected sum from actual sum → gives the **duplicate element**.

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Description |
|------------|-------|-------------|
| Time       | O(N) | Single loop to calculate sum |
| Space      | O(1) | No extra data structure used |

---

## 🎯 Constraints
- 2 ≤ `arr.length` ≤ 10⁵  
- 1 ≤ `arr[i]` ≤ n-1  

---

## 💻 Code
```java
class Solution {
    public int findDuplicate(int[] arr) {
        int n = arr.length;
        long sum = 0;
        for(int i: arr){
            sum += i;
        }
        return (int)(sum - (((long)n * (n - 1)) / 2));
    }
}
```

---

## 📝 Explanation of Code

1. Compute **actual sum** of all elements.  
2. Compute **expected sum** of numbers `1` to `n-1`.  
3. The **difference = duplicate element**.  

---

> Made with ❤️ by Milan Haria
