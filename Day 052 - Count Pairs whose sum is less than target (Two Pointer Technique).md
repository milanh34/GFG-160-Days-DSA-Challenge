<h1 align="center">🧮 Count Pairs Whose Sum Is Less Than Target 🧮</h1>

---

## 📝 Problem Statement

Given an array `arr[]` and an integer `target`, find the **number of pairs** in the array such that:

```
arr[i] + arr[j] < target, where i < j
```

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [7, 2, 5, 3], target = 8
```
**Output:**
```
2
```
**Explanation:**
Valid pairs: (2, 5), (2, 3)

---

### ✅ Example 2:
**Input:**
```
arr = [5, 2, 3, 2, 4, 1], target = 5
```
**Output:**
```
4
```
**Explanation:**
Valid pairs: (2, 2), (2, 1), (3, 1), (2, 1)

---

### ✅ Example 3:
**Input:**
```
arr = [2, 1, 8, 3, 4, 7, 6, 5], target = 7
```
**Output:**
```
6
```
**Explanation:**
Valid pairs: (2, 1), (2, 3), (2, 4), (1, 3), (1, 4), (1, 5)

---

## 🧠 Approach

- Sort the array.
- Use two pointers: one from the beginning (`beg`) and one from the end (`end`).
- If `arr[beg] + arr[end] >= target`, move `end` left.
- If it's less, count all pairs between `beg` and `end` (`end - beg`) and move `beg` right.
- Continue until `beg < end`.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                     |
|------------------|-----------|---------------------------------|
| 🕒 Time          | O(N log N) | Sorting + two pointer pass     |
| 📦 Space         | O(1)      | Constant extra space            |

---

## 🎯 Constraints

- 1 ≤ arr.length ≤ 10⁵  
- 0 ≤ arr[i] ≤ 10⁴  
- 1 ≤ target ≤ 10⁴  

---

## 💻 Code

```java
class Solution {
    int countPairs(int arr[], int target) {
        Arrays.sort(arr);
        int beg = 0, end = arr.length - 1, ans = 0;
        while(beg < end){
            if(arr[beg] + arr[end] >= target){
                end--;
            } else{
                ans += (end - beg);
                beg++;
            }
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
