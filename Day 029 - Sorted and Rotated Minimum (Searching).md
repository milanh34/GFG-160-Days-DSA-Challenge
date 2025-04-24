<h1 align="center">🔍 Sorted and Rotated Minimum 🔍</h1>

---

## 📝 Problem Statement

A sorted array `arr[]` is rotated at an unknown index. Your task is to find the **minimum element** in the array.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr[] = [5, 6, 1, 2, 3, 4]
```
**Output:**
```
1
```
**Explanation:**  
The original sorted array `[1, 2, 3, 4, 5, 6]` was rotated, and `1` is now at index 2.  
So, `1` is the minimum element.

---

### ✅ Example 2:
**Input:**
```
arr[] = [3, 1, 2]
```
**Output:**
```
1
```
**Explanation:**  
The original sorted array `[1, 2, 3]` was rotated twice, and `1` is at index 1.  
Hence, the minimum element is `1`.

---

### ✅ Example 3:
**Input:**
```
arr[] = [4, 2, 3]
```
**Output:**
```
2
```
**Explanation:**  
The original sorted array `[2, 3, 4]` was rotated once.  
`2` is now at index 1 and is the smallest element in the array.

---

## 🧠 Approach

We use a **modified binary search** to find the smallest element in the rotated array.

### 🔹 Case 1: Already Sorted
If the first element is smaller than the last element, then the array is not rotated.  
Return `arr[0]`.

### 🔹 Case 2: Rotated Array
We perform binary search:
- If `arr[mid] < arr[0]`, the minimum lies on the **left half**, so move `end = mid`.
- Otherwise, the minimum lies on the **right half**, so move `beg = mid + 1`.

The loop ends when `beg == end`, which points to the smallest element.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                    |
|------------------|-----------|--------------------------------|
| 🕒 Time          | `O(log n)`| Binary search is used         |
| 📦 Space         | `O(1)`    | No extra space is used        |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁶`
- `1 ≤ arr[i] ≤ 10⁹`
- All elements are **distinct**

---

## 💻 Code

```java
class Solution {
    public int findMin(int[] arr) {
        int n = arr.length;
        if(arr[0] < arr[n - 1]){
            return arr[0];
        }
        int beg = 0, end = n - 1;
        while(beg < end){
            int mid = beg + (end - beg) / 2;
            if(arr[mid] < arr[0]){
                end = mid;
            } else{
                beg = mid + 1;
            }
        }
        return arr[end];
    }
}
```

---

## 📝 Explanation of Code

- **Initial Check**:  
  If the array is already sorted (`arr[0] < arr[n-1]`), return `arr[0]`.

- **Binary Search Loop**:  
  Find the rotation point where the value drops — that is the minimum element.

- **Final Result**:  
  The index `beg` (or `end`) after the loop ends is the index of the smallest element.

---

> Made with ❤️ by Milan Haria
