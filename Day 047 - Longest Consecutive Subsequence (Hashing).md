<h1 align="center">🔥 Longest Consecutive Subsequence 🔥</h1>

---

## 📝 Problem Statement

Given an array `arr[]` of non-negative integers. Find the length of the **longest subsequence** such that the elements are **consecutive integers**.  
Note that the consecutive numbers can be in any order within the array.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [2, 6, 1, 9, 4, 5, 3]
```
**Output:**
```
6
```
**Explanation:**  
Longest consecutive sequence is `1, 2, 3, 4, 5, 6`.

---

### ✅ Example 2:
**Input:**
```
arr = [1, 9, 3, 10, 4, 20, 2]
```
**Output:**
```
4
```
**Explanation:**  
Longest consecutive sequence is `1, 2, 3, 4`.

---

### ✅ Example 3:
**Input:**
```
arr = [15, 13, 12, 14, 11, 10, 9]
```
**Output:**
```
7
```
**Explanation:**  
Longest consecutive sequence is `9, 10, 11, 12, 13, 14, 15`.

---

## 🧠 Approach

- Use a **boolean array** to mark the presence of numbers.
- Iterate from `0` to `100000` and **count consecutive `true` values**.
- Keep updating the **maximum consecutive count** encountered.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value        | Description                           |
|------------------|--------------|---------------------------------------|
| 🕒 Time          | `O(n + max_element)` | Insert in boolean array and iterate full range |
| 📦 Space         | `O(max_element)`  | Boolean array of size `100001` |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`
- `0 ≤ arr[i] ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public int longestConsecutive(int[] arr) {
        boolean[] nums = new boolean[100001];
        for(int i: arr){
            nums[i] = true;
        }
        int count = 0, max = 0;
        for(boolean i: nums){
            if(i){
                count++;
                max = Math.max(max, count);
            } else{
                count = 0;
            }
        }
        return max;
    }
}
```

---

## 📝 Explanation of Code

- Mark each number's presence using a `boolean` array.
- Traverse the array from start to end and count continuous `true` entries.
- This ensures linear time complexity, making it efficient for large arrays.

---

> Made with ❤️ by Milan Haria
