<h1 align="center">🔢 Sort 0s, 1s, and 2s 🔢</h1>

---

## 📝 Problem Statement

Given an array `arr[]` containing only the elements 0s, 1s, and 2s, the task is to sort the array in ascending order without utilizing any built-in sort function.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr[] = [0, 1, 2, 0, 1, 2]
```

**Output:**  
```
[0, 0, 1, 1, 2, 2]
```

**Explanation:**  
The 0s, 1s, and 2s are segregated into ascending order.

---

### ✅ Example 2:
**Input:**  
```
arr[] = [0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1]
```

**Output:**  
```
[0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2]
```

**Explanation:**  
The 0s, 1s, and 2s are segregated into ascending order.

---

## 🧠 Approach

The problem is solved using a **three-pass approach** to segregate 0s, 1s, and 2s.

### Steps:
1. **First Pass**: 
   - We traverse the array to segregate 0s and 2s.
   - As we encounter 0, we place it at the `zero` pointer and increment the `zero` pointer as well.
   - As we encounter 2, we decrease the `two` pointer.
   
2. **Second Pass**: 
   - After the first pass, we place all 2s at the end of the array.

3. **Third Pass**: 
   - Place all 1s in the middle section between 0s and 2s.

This approach runs in linear time and makes sure the array is sorted without any extra space.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                               |
|------------------|-----------|-------------------------------------------|
| 🕒 Time          | `O(n)`    | We traverse the array a few times.       |
| 📦 Space         | `O(1)`    | Only constant extra space is used.       |

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10⁶`
- `0 ≤ arr[i] ≤ 2`

---

## 💻 Code

```java
class Solution {
    public void sort012(int[] arr) {
        int n = arr.length;
        int zero = 0, two = n - 1;
        for(int i: arr){
            if(i == 0){
                arr[zero] = 0;
                zero++;
            } else if(i == 2){
                two--;
            }
        }
        for(int i = n - 1; i > two; i--){
            arr[i] = 2;
        }
        for(int i = zero; i <= two; i++){
            arr[i] = 1;
        }
    }
}
```

---

## 📝 Explanation of Code

- **Pointers Initialization**:  
  The `zero` pointer starts from the beginning of the array, and `two` starts from the end of the array.

- **First Pass**:  
  We iterate through the array to count the 0s and 2s. When a 0 is encountered, it's placed at the `zero` pointer, and the pointer is incremented. When a 2 is encountered, we decrease the `two` pointer.

- **Second Pass**:  
  Once the positions for 0s and 2s are determined, we place all 2s at the end of the array.

- **Third Pass**:  
  After placing 0s and 2s, we assign 1s to the remaining positions.

---


> Made with ❤️ by Milan Haria
