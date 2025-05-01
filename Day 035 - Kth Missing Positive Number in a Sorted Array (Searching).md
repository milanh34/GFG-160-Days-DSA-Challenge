<h1 align="center">🔍 Kth Missing Positive Number in a Sorted Array 🔍</h1>

---

## 📝 Problem Statement

Given a **sorted array** of **distinct positive integers** `arr[]`, and an integer `k`,  
your task is to **find the k-th positive integer** that is **missing** from the array.

A positive number `x` is said to be **missing** if it does not appear in the array `arr[]`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr = [2, 3, 4, 7, 11], k = 5
```
**Output:**  
```
9
```
**Explanation:**  
Missing numbers = `1, 5, 6, 8, 9, 10, ...`  
The **5th missing** number is `9`.

---

### ✅ Example 2:
**Input:**  
```
arr = [1, 2, 3], k = 2
```
**Output:**  
```
5
```
**Explanation:**  
Missing numbers = `4, 5, 6, ...`  
The 2nd missing number is `5`.

---

### ✅ Example 3:
**Input:**  
```
arr = [3, 5, 9, 10, 11, 12], k = 2
```
**Output:**  
```
2
```
**Explanation:**  
Missing numbers = `1, 2, 4, 6, 7, 8...`  
The 2nd missing number is `2`.

---

## 🧠 Approach

### Intuition:
If the array had no missing numbers, `arr[i]` would be equal to `i + 1`.  
The actual number of missing numbers before `arr[i]` is:  
```
missing = arr[i] - (i + 1)
```

### Steps:

1. **Edge Case 1**:  
   If the first element `arr[0]` is greater than or equal to `k`,  
   then the `k`-th missing number is just `k`.

2. **Edge Case 2**:  
   If the total number of missing numbers before the last element is less than `k`,  
   then the answer lies after the last element.  
   So return: `arr.length + k`

3. **Binary Search**:
   - Initialize `beg = 0`, `end = arr.length`.
   - While `beg < end`, find `mid = (beg + end) / 2`.
   - If `arr[mid] - (mid + 1) < k`, move to the right (`beg = mid + 1`).
   - Else, move to the left (`end = mid`).

4. After the loop, the result is: `beg + k`.

---

## ⏱️ Time & Space Complexity

| Complexity | Value     | Explanation                            |
|------------|-----------|----------------------------------------|
| Time       | O(log N)  | Binary search over the array indices   |
| Space      | O(1)      | Only constant extra space is used      |

---

## 🔒 Constraints

- `1 <= arr.length <= 10⁵`
- `1 <= k <= 10⁵`
- `1 <= arr[i] <= 10⁶`
- `arr[]` is **strictly increasing**

---

## 💻 Code

```java
class Solution {
    public int kthMissing(int[] arr, int k) {
        int n = arr.length;
        if(arr[0]  - 1 >= k){
            return k;
        }
        if(arr[n - 1] - n < k){
            return n + k;
        }
        int beg = 0, end = n;
        while(beg < end){
            int mid = beg + (end - beg) / 2;
            if(arr[mid] - mid - 1 < k){
                beg = mid + 1;
            } else{
                end = mid;
            }
        }
        return beg + k;
    }
}
```

---

> Made with ❤️ by Milan Haria
