<h1 align="center">⛰️ Peak Element ⛰️</h1>

---

## 📝 Problem Statement

Given an array `arr[]` where **no two adjacent elements are same**, find the **index** of a **peak element**.  
An element is considered a peak if it is **greater** than its adjacent elements (if they exist).  
If multiple peaks exist, return the index of **any one** of them.  

> **Note:**  
> - Consider the element before the first and after the last as **negative infinity**.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [1, 2, 4, 5, 7, 8, 3]
```
**Output:**
```
true
```
**Explanation:**  
`arr[5] = 8` is a peak because `arr[4] < arr[5] > arr[6]`.

---

### ✅ Example 2:
**Input:**
```
arr = [10, 20, 15, 2, 23, 90, 80]
```
**Output:**
```
true
```
**Explanation:**  
Both `arr[1] = 20` and `arr[5] = 90` are peaks.  
`arr[1]` satisfies `arr[0] < arr[1] > arr[2]`, and  
`arr[5]` satisfies `arr[4] < arr[5] > arr[6]`.

---

### ✅ Example 3:
**Input:**
```
arr = [1, 2, 3]
```
**Output:**
```
true
```
**Explanation:**  
`arr[2] = 3` is a peak because `arr[1] < arr[2]`, and beyond it is negative infinity.

---

## 🧠 Approach

We check:
- If the first or last element is a peak (because the virtual neighbor is `-∞`).
- Otherwise, loop through the array and check for any element that is greater than both its neighbors.

Since the array has no two adjacent elements equal, it's guaranteed that at least one peak will exist.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                            |
|------------------|-----------|----------------------------------------|
| 🕒 Time          | `O(n)`    | Linear scan of the array               |
| 📦 Space         | `O(1)`    | No extra space used                    |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁶`
- `-2³¹ ≤ arr[i] ≤ 2³¹ - 1`
- No two adjacent elements are the same

---

## 💻 Code

```java
class Solution {
    public int peakElement(int[] arr) {
        int n = arr.length;
        if(n == 1 || arr[0] > arr[1]){
            return 0;
        }
        if(arr[n - 1] > arr[n - 2]){
            return n - 1;
        }
        for(int i = 1; i < n - 1; i++){
            if(arr[i] > arr[i -1] && arr[i] > arr[i + 1]){
                return i;
            }
        }
        return -1;
    }
}
```

---

## 📝 Explanation of Code

- If the first element is greater than the second, it is a peak.
- If the last element is greater than the second-last, it is a peak.
- Otherwise, traverse from index `1` to `n-2` and find any element that is greater than both its neighbors.
- Return its index.

---

> Made with ❤️ by Milan Haria
