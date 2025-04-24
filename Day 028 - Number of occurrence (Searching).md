<h1 align="center">🔢 Number of Occurrence 🔢</h1>

---

## 📝 Problem Statement

Given a **sorted array** `arr[]` and an integer `target`, return the **number of times** `target` appears in the array.

---

## ✅ Examples

### Example 1
**Input:**  
```
arr = [1, 1, 2, 2, 2, 2, 3]
target = 2
```
**Output:**  
```
4
```
**Explanation:**  
The number `2` appears 4 times.

---

### Example 2
**Input:**  
```
arr = [1, 1, 2, 2, 2, 2, 3]
target = 4
```
**Output:**  
```
0
```
**Explanation:**  
The number `4` does not appear in the array.

---

### Example 3
**Input:**  
```
arr = [8, 9, 10, 12, 12, 12]
target = 12
```
**Output:**  
```
3
```
**Explanation:**  
The number `12` appears 3 times.

---

## 🧠 Approach

To count the number of times `target` appears in a **sorted array**, we use **binary search** to find:

1. **First Occurrence of `target`**
- We look for the **leftmost index** where the value is equal to `target`.
- If `arr[mid] >= target`, the possible first occurrence is on the **left side**, so we move `end = mid`.
- Else, move to the **right side** with `beg = mid + 1`.
2. **Last Occurrence of `target`**
- We look for the **rightmost index** where the value is equal to `target`.
- If `arr[mid] <= target`, the possible last occurrence is on the **right side**, so we move `beg = mid`.
- Else, move to the **left side** with `end = mid - 1`.
3. Final Step
- Once both **first** and **last** positions are found, the total count is: ```count = last - first + 1;```
---

## ⏱️ Time & Space Complexity

| Type       | Complexity | Explanation                           |
|------------|------------|---------------------------------------|
| 🕒 Time     | O(log n)   | Due to two binary search passes       |
| 📦 Space    | O(1)       | No extra space used                   |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁶`
- `1 ≤ arr[i] ≤ 10⁶`
- `1 ≤ target ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    int countFreq(int[] arr, int target) {
        int n = arr.length;
        if(target < arr[0] || target > arr[n - 1]){
            return 0;
        }
        int lower = 0, upper = n - 1;
        if(arr[0] == target){
            lower = 0;
        } else{
            int beg = 0, end = n - 1;
            while(beg < end){
                int mid = beg + (end - beg) / 2;
                if(arr[mid] >= target){
                    end = mid;
                } else{
                    beg = mid + 1;
                }
            }
            if(arr[beg] != target){
                return 0;
            }
            lower = beg;
        }
        if(arr[n - 1] == target){
            upper = n - 1;
        } else{
            int beg = lower, end = n - 1;
            while(beg < end){
                int mid = beg + (end - beg + 1) / 2;
                if(arr[mid] <= target){
                    beg = mid;
                } else{
                    end = mid - 1;
                }
            }
            upper = end;
        }
        return upper - lower + 1;
    }
}
```

---

## 🧩 Edge Cases

- `target` not present → return `0`
- All elements are `target` → return full length
- Only one element equals `target` → return `1`

---

> Made with ❤️ by Milan Haria
