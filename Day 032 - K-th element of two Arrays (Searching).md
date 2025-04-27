<h1 align="center">🔢 K-th Element of Two Sorted Arrays 🔢</h1>

---

## 📝 Problem Statement

Given two **sorted arrays** `a[]` and `b[]` and an integer `k`, find the **k-th element** of the combined sorted array.  
You need to find the element efficiently without actually merging both arrays.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
a = [2, 3, 6, 7, 9]
b = [1, 4, 8, 10]
k = 5
```
**Output:**
```
6
```
**Explanation:**  
Combined sorted array = `[1, 2, 3, 4, 6, 7, 8, 9, 10]`.  
The 5th element is `6`.

---

### ✅ Example 2:
**Input:**
```
a = [100, 112, 256, 349, 770]
b = [72, 86, 113, 119, 265, 445, 892]
k = 7
```
**Output:**
```
256
```
**Explanation:**  
Combined sorted array = `[72, 86, 100, 112, 113, 119, 256, 265, 349, 445, 770, 892]`.  
The 7th element is `256`.

---

## 🧠 Approach

Use a **two-pointer approach**:

- Initialize two pointers at the start of both arrays.
- Move the pointer which has the smaller element, until you reach the `k`-th move.
- Keep track of the current element.
- When `k` elements have been traversed, the current element is the answer.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                          |
|------------------|-----------|--------------------------------------|
| 🕒 Time          | `O(k)`    | We traverse only up to k elements    |
| 📦 Space         | `O(1)`    | Only a few variables are used        |

---

## 🎯 Constraints

- `1 ≤ a.length, b.length ≤ 10⁶`
- `1 ≤ k ≤ a.length + b.length`
- `0 ≤ a[i], b[i] < 10⁸`

---

## 💻 Code

```java
class Solution {
    public int kthElement(int a[], int b[], int k) {
        int n1 = a.length, n2 = b.length, i = 0, j = 0, c = 0, ans = 0;
        while(i < n1 && j < n2 && c < k){
            if(a[i] < b[j]){
                ans = a[i];
                i++;
            } else{
                ans = b[j];
                j++;
            }
            c++;
        }
        while(i < n1 && c < k){
            ans = a[i];
            i++;
            c++;
        }
        while(j < n2 && c < k){
            ans = b[j];
            j++;
            c++;
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- Traverse both arrays until you have moved `k` steps.
- At each step, pick the smaller of the two current elements.
- After `k` steps, the last picked element is the k-th element in the combined sorted array.

---

> Made with ❤️ by Milan Haria
