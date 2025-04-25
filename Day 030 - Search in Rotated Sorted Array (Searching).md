<h1 align="center">🔍 Search in Rotated Sorted Array 🔍</h1>

---

## 📝 Problem Statement

Given a **sorted and rotated array** `arr[]` of distinct elements, and a `key`, find the **index** of the key in the array.  
If the key is **not present**, return `-1`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr[] = [5, 6, 7, 8, 9, 10, 1, 2, 3], key = 3
```
**Output:**
```
8
```
**Explanation:**  
The original sorted array was `[1, 2, 3, 5, 6, 7, 8, 9, 10]`, rotated at index 5.  
The element `3` is present at index `8`.

---

### ✅ Example 2:
**Input:**
```
arr[] = [3, 5, 1, 2], key = 6
```
**Output:**
```
-1
```
**Explanation:**  
Element `6` is not present in the array, so the output is `-1`.

---

### ✅ Example 3:
**Input:**
```
arr[] = [33, 42, 72, 99], key = 42
```
**Output:**
```
1
```
**Explanation:**  
The array is already sorted, no rotation. Element `42` is found at index `1`.

---

## 🧠 Approach

This problem is solved using **modified binary search** by considering the rotation:

- At each step, check if `arr[mid] == key`.
- If not, check **which side** of the array is sorted:
  - If **left half** is sorted:
    - Check if key lies in this half.
  - If **right half** is sorted:
    - Check if key lies in this half.
- Move your binary search window accordingly.

This logic works because **one side of the array will always be sorted**, even if the entire array is rotated.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                      |
|------------------|-----------|----------------------------------|
| 🕒 Time          | `O(log n)`| Efficient binary search approach |
| 📦 Space         | `O(1)`    | No extra space is required       |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁶`
- `0 ≤ arr[i] ≤ 10⁶`
- `1 ≤ key ≤ 10⁶`
- All elements in the array are **distinct**

---

## 💻 Code

```java
class Solution {
    int search(int[] arr, int key) {
        int beg = 0, end = arr.length - 1;
        while(beg < end){
            int mid = beg + (end - beg) / 2;
            if(arr[mid] == key){
                return mid;
            } else if(arr[mid] < key){
                if(arr[mid] >= arr[0] || key < arr[0]){
                    beg = mid + 1;
                } else{
                    end = mid - 1;
                }
            } else{
                if(key >= arr[0] || arr[mid] < arr[0]){
                    end = mid - 1;
                } else{
                    beg = mid + 1;
                }
            }
        }
        if(arr[beg] == key){
            return beg;
        } else{
            return -1;
        }
    }
}
```

---

## 📝 Explanation of Code

- **Binary Search** is applied while checking which part of the array (left or right) is sorted.
- Adjust the search window (`beg`, `end`) depending on where the key can possibly lie.
- After the loop ends, we do a final comparison for `arr[beg]`.

---

> Made with ❤️ by Milan Haria
