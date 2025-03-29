<h1 align="center">💨 Move All Zeroes to End 💨</h1>

---

## 🧩 Problem Statement

You are given an array `arr[]` of **non-negative integers**.  
Your task is to **move all the zeros** in the array to the **right end**, while maintaining the **relative order** of the non-zero elements.

🎯 The operation must be **performed in place**, meaning **no extra space** should be used.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```java
arr[] = [1, 2, 0, 4, 3, 0, 5, 0]
```

**Output:**  
```
[1, 2, 4, 3, 5, 0, 0, 0]
```

**Explanation:**  
Three zeroes are shifted to the end while preserving the order of the other numbers.

---

### ✅ Example 2:
**Input:**  
```java
arr[] = [10, 20, 30]
```

**Output:**  
```
[10, 20, 30]
```

**Explanation:**  
No zeroes to move, so the array stays the same.

---

### ✅ Example 3:
**Input:**  
```java
arr[] = [0, 0]
```

**Output:**  
```
[0, 0]
```

**Explanation:**  
All elements are zero — nothing changes.

---

## 🧠 Approach

> 💡 **Idea:**  
We'll keep a pointer `j` to track the position where the next non-zero element should go.

> ⚙️ **Steps:**
1. Traverse the array from left to right.
2. If the current element is non-zero, place it at index `j` and increment `j`.
3. Once all non-zero elements are repositioned, fill the remaining part of the array from index `j` to `n-1` with `0`s.

This approach ensures:
- Non-zero elements maintain their original order ✅
- Zeroes are moved to the end ✅
- All done in-place without extra space ✅

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Reason |
|------------|-------|--------|
| 🕒 Time     | `O(n)` | Single pass to move elements, and another to fill 0s |
| 📦 Space    | `O(1)` | In-place, no extra storage used |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`  
- `0 ≤ arr[i] ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    void pushZerosToEnd(int[] arr) {
       int n = arr.length, j = 0;
       for(int i = 0; i < n; i++){
           if(arr[i] != 0){
               arr[j++] = arr[i];
           }
       }
       for(int i = j; i < n; i++){
           arr[i] = 0;
       }
    }
}
```

---

> Made with 🧡 by Milan Haria
