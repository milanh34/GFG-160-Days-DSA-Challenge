<h1 align="center">🤝 Pair With Given Sum In A Sorted Array 🤝</h1>

---

## 📝 Problem Statement

You are given a **sorted array** `arr[]` and an integer `target`.  
Find the **number of pairs** `(i, j)` such that:

```
arr[i] + arr[j] == target, and i ≠ j
```

Multiple identical elements are allowed, and **distinct indices** must be used.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [-1, 1, 5, 5, 7], target = 6
```
**Output:**
```
3
```
**Explanation:**
Valid pairs: (1, 5), (1, 5), (-1, 7)

---

### ✅ Example 2:
**Input:**
```
arr = [1, 1, 1, 1], target = 2
```
**Output:**
```
6
```
**Explanation:**
All possible pairs of 1s add up to 2 → C(4, 2) = 6 pairs.

---

### ✅ Example 3:
**Input:**
```
arr = [-1, 10, 10, 12, 15], target = 125
```
**Output:**
```
0
```
**Explanation:**
No pair has sum = 125.

---

## 🧠 Approach

- Use the **two-pointer technique** since the array is sorted.
- Move two pointers from both ends:
  - If the sum is less than target, move `beg` forward.
  - If the sum is more, move `end` backward.
  - If the sum matches:
    - Count duplicates on both ends.
    - If elements are different, add `countLeft * countRight`.
    - If both sides are the same element, use combination formula: `nC2 = n*(n-1)/2`.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                   |
|------------------|-----------|-------------------------------|
| 🕒 Time          | O(N)      | Linear scan with two pointers |
| 📦 Space         | O(1)      | No extra space used           |

---

## 🎯 Constraints

- -10⁵ ≤ target ≤ 10⁵  
- 2 ≤ arr.length ≤ 10⁵  
- -10⁵ ≤ arr[i] ≤ 10⁵  

---

## 💻 Code

```java
class Solution {
    int countPairs(int arr[], int target) {
        int n = arr.length, ans = 0;
        int beg = 0, end = n - 1;
        while(beg < end){
            int sum = arr[beg] + arr[end];
            if(sum == target){
                int i = 0, j = 0, l = arr[beg], r = arr[end];
                while(beg <= end && arr[beg] == l){
                    i++;
                    beg++;
                }
                while(beg <= end && arr[end] == r){
                    j++;
                    end--;
                }
                if(l != r){
                    ans += i * j;
                } else{
                    ans += ((i - 1) * i) / 2;
                }
            } else if(sum < target){
                beg++;
            } else{
                end--;
            }
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
