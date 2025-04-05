<h1 align="center">🏰 Minimize the Heights II 🏰</h1>

---

## 🧩 Problem Statement

You are given an array `arr[]` of size `n` representing the heights of `n` towers. You are also given a positive integer `k`. Your task is to **modify each tower exactly once** by either:
- Increasing the height by `k`, or
- Decreasing the height by `k`.

Then, determine the **minimum possible difference** between the height of the tallest and the shortest tower **after** these modifications.

> ⚠️ Note: No height should become negative after the modification.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
k = 2  
arr = [1, 5, 8, 10]
```

**Output:**  
```
5
```

**Explanation:**  
After modifying:  
`{1+k, 5-k, 8-k, 10-k} = {3, 3, 6, 8}`  
Max height = 8, Min height = 3  
Difference = 8 - 3 = **5**

---

### ✅ Example 2:
**Input:**  
```
k = 3  
arr = [3, 9, 12, 16, 20]
```

**Output:**  
```
11
```

**Explanation:**  
After modifying:  
`{3+k, 9+k, 12-k, 16-k, 20-k} = {6, 12, 9, 13, 17}`  
Max height = 17, Min height = 6  
Difference = 17 - 6 = **11**

---

## 🧠 Approach

### 🔍 Key Insight:

To minimize the difference between the tallest and shortest towers, the idea is to:
1. **Sort the array**.
2. **Modify the smallest elements by increasing them**, and
3. **Modify the largest elements by decreasing them**.

We explore every partition of the sorted array and find the optimal point where the left part is increased and the right part is decreased. This strategy ensures that we're balancing heights effectively.

---

## 🧑‍💻 Detailed Steps:

1. **Sort** the array in non-decreasing order.
2. Initialize:
   - `initialDiff = arr[n-1] - arr[0]` — this is the difference before any operations.
   - `small = arr[0] + k`, `big = arr[n-1] - k` — assumed min and max after modification.
3. For each index `i` from `1` to `n-1`:
   - If `arr[i] - k < 0`, continue (skip to avoid negative heights).
   - Update `minHeight = min(small, arr[i] - k)`
   - Update `maxHeight = max(big, arr[i - 1] + k)`
   - Update `diff = min(diff, maxHeight - minHeight)`
4. Return the minimum difference obtained.

---

## ⏱️ Time & Space Complexity

| Complexity | Value           | Description                          |
|------------|------------------|--------------------------------------|
| 🕒 Time     | `O(n log n)`      | For sorting the array                |
| 📦 Space    | `O(1)`            | Constant extra space used            |

---

## 🎯 Constraints

- `1 ≤ k ≤ 10⁷`
- `1 ≤ n ≤ 10⁵`
- `1 ≤ arr[i] ≤ 10⁷`

---

## 💻 Code

```java
class Solution {
    int getMinDiff(int[] arr, int k) {
        Arrays.sort(arr);
        int n = arr.length;
        int max = arr[n- 1], min = arr[0];
        int diff = max - min;
        max -= k;
        min += k;
        for(int i = 1; i < n; i++){
            if(arr[i] - k >= 0){
                diff = Math.min(diff, Math.max(max, arr[i - 1] + k) - Math.min(min, arr[i] - k));
            }
        }
        return diff;
    }
}
```

---

> Made with ❤️ by Milan Haria
