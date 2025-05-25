<h1 align="center">🧱 Container With Most Water 🧱</h1>

---

## 📝 Problem Statement

You are given an array `arr[]` of non-negative integers where each element represents the height of a vertical line on the x-axis. Find the **maximum water** that can be contained between any two lines.

> 📌 **Note:** A single line cannot hold any water — you need two lines to form a container.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [1, 5, 4, 3]
```

**Output:**  
```
6
```

**Explanation:**  
- Choose lines at index 1 (height = 5) and index 3 (height = 3)  
- Width = 3 - 1 = 2  
- Height = min(5, 3) = 3  
- Area = 2 × 3 = 6

---

### ✅ Example 2:

**Input:**  
```
arr = [3, 1, 2, 4, 5]
```

**Output:**  
```
12
```

**Explanation:**  
- Choose lines at index 0 (height = 3) and index 4 (height = 5)  
- Width = 4 - 0 = 4  
- Height = min(3, 5) = 3  
- Area = 4 × 3 = 12

---

### ✅ Example 3:

**Input:**  
```
arr = [2, 1, 8, 6, 4, 6, 5, 5]
```

**Output:**  
```
25
```

**Explanation:**  
- Choose lines at index 2 (height = 8) and index 7 (height = 5)  
- Width = 7 - 2 = 5  
- Height = min(8, 5) = 5  
- Area = 5 × 5 = 25

---

## 🧠 Approach

### Two-Pointer Technique:

- Start with two pointers: one at the beginning (`beg`) and one at the end (`end`) of the array.
- At each step, calculate the area of the container:
  ```
  area = (end - beg) × min(arr[beg], arr[end])
  ```
- Update `ans` if this area is greater than the current maximum.
- Move the pointer pointing to the **shorter line** (since the limiting factor is the smaller height):
  - If `arr[beg] < arr[end]`, move `beg++`
  - Else, move `end--`
- Repeat until both pointers meet.

This greedy strategy works because a taller height on the opposite end might allow a larger area if the width is still good enough.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description              |
|------------|--------|--------------------------|
| Time       | O(N)   | Linear traversal         |
| Space      | O(1)   | Constant space           |

---

## 🎯 Constraints

- 1 ≤ arr.length ≤ 10⁵  
- 1 ≤ arr[i] ≤ 10⁴

---

## 💻 Code

```java
class Solution {
    public int maxWater(int arr[]) {
        int beg = 0, end = arr.length - 1, ans = 0;
        while(beg < end){
            if(arr[beg] < arr[end]){
                ans = Math.max(ans, (end - beg) * arr[beg]);
                beg++;
            } else{
                ans = Math.max(ans, (end - beg) * arr[end]);
                end--;
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- `beg` starts from the left, `end` starts from the right.
- `ans` stores the maximum water seen so far.
- In each iteration:
  - We compute the area formed by the lines at `beg` and `end`.
  - Update `ans` if the computed area is larger.
  - Move the pointer pointing to the shorter line (as it's limiting the container height).
- This ensures all potential max-area combinations are considered efficiently.

---

> Made with ❤️ by Milan Haria
