<h1 align="center">🏔️ Minimize the Heights II 🏔️</h1>

---

## 🧩 Problem Statement

Given an array `arr[]` denoting the heights of `N` towers and a positive integer `K`, you need to perform one of the following operations on each tower:

1. Increase the height of the tower by `K`
2. Decrease the height of the tower by `K`

Your task is to find the minimum possible difference between the height of the shortest and tallest towers after performing the operations.

> **Note:** The resultant heights of all towers must not be negative integers. It is compulsory to increase or decrease the height by `K` for each tower.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
k = 2, arr[] = {1, 5, 8, 10}
```

**Output:**  
```
5
```

**Explanation:**  
- After modifying the array: `{1 + 2, 5 - 2, 8 - 2, 10 - 2}` = `{3, 3, 6, 8}`.
- The difference between the largest and smallest is `8 - 3 = 5`.

---

### ✅ Example 2:
**Input:**  
```
k = 3, arr[] = {3, 9, 12, 16, 20}
```

**Output:**  
```
11
```

**Explanation:**  
- After modifying the array: `{3 + 3, 9 + 3, 12 - 3, 16 - 3, 20 - 3}` = `{6, 12, 9, 13, 17}`.
- The difference between the largest and smallest is `17 - 6 = 11`.

---

## 🧠 Approach

The goal is to minimize the difference between the tallest and shortest towers after applying the operations. Here's the approach:

### Step 1: Sort the Array
- First, sort the array to make sure that you can easily access the smallest and largest towers.

### Step 2: Modify Heights
- For each tower, you can either increase or decrease its height by `K`. The aim is to minimize the height difference after the operation.

### Step 3: Check Possible Differences
- After modifying the heights, compute the difference between the tallest and shortest tower for each possible configuration and return the minimum difference.

### Step 4: Ensure Valid Heights
- Ensure that no tower has a height less than 0 after the operation.

---

### 💡 Algorithm

1. **Sort the Array**: Start by sorting the `arr[]` to easily find the smallest and largest values.
2. **Adjust Heights**: For each tower, calculate the possible new heights by either increasing or decreasing the height by `K`.
3. **Calculate the Difference**: For each configuration, calculate the difference between the tallest and shortest towers.
4. **Return the Minimum Difference**: Find the configuration with the smallest height difference and return it.

---

## ⏱️ Time & Space Complexity

| Complexity | Value             | Reason                         |
|------------|-------------------|--------------------------------|
| 🕒 Time     | `O(n log n)`       | Sorting the array takes `O(n log n)`. |
| 📦 Space    | `O(1)`             | We are using a constant amount of space. |

---

## 🎯 Constraints

- `1 ≤ k ≤ 10^7`
- `1 ≤ n ≤ 10^5`
- `1 ≤ arr[i] ≤ 10^7`

---

## 💻 Code

```java
class Solution {
    int getMinDiff(int[] arr, int k) {
        Arrays.sort(arr);
        int n = arr.length;
        int max = arr[n - 1], min = arr[0];
        int diff = max - min;
        max -= k;
        min += k;
        for(int i = 1; i < n; i++) {
            if(arr[i] - k >= 0) {
                diff = Math.min(diff, Math.max(max, arr[i - 1] + k) - Math.min(min, arr[i] - k));
            }
        }
        return diff;
    }
}
```


---

> Made with ❤️ by Milan Haria
