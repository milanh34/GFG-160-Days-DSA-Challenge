<h1 align="center">🚫 Non-overlapping Intervals 🚫</h1>

---

## 📝 Problem Statement

Given a 2D array `intervals[][]` where each `intervals[i] = [starti, endi]` represents a time interval, return the **minimum number of intervals** you need to **remove** to make the rest of the intervals **non-overlapping**.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
intervals = [[1, 2], [2, 3], [3, 4], [1, 3]]
```

**Output:**  
```
1
```

**Explanation:**  
Interval `[1, 3]` overlaps with `[1, 2]` and `[2, 3]`, so we can remove it.

---

### ✅ Example 2:
**Input:**  
```
intervals = [[1, 3], [1, 3], [1, 3]]
```

**Output:**  
```
2
```

**Explanation:**  
All intervals are identical and hence overlapping. We can keep only one and remove the other two.

---

### ✅ Example 3:
**Input:**  
```
intervals = [[1, 2], [5, 10], [18, 35], [40, 45]]
```

**Output:**  
```
0
```

**Explanation:**  
All intervals are non-overlapping. No need to remove any.

---

## 🧠 Approach

1. **Sort the intervals** based on their **start time**.
2. Initialize:
   - `ans = 0` to count the number of intervals to remove.
   - `prev = intervals[0][1]` to keep track of the **end** of the last added interval.
3. Traverse the sorted intervals:
   - If `current.start >= prev`, no overlap — update `prev = current.end`.
   - Else, we have an overlap — increment `ans`, and update `prev` to the **minimum of previous and current end** to retain the interval that ends earlier (greedy).

---

## ⏱️ Time & Space Complexity

| Complexity       | Value         | Description                                 |
|------------------|---------------|---------------------------------------------|
| 🕒 Time          | `O(n log n)`  | Due to sorting of intervals                 |
| 📦 Space         | `O(1)`        | Only a few variables used                   |

---

## 🎯 Constraints

- `1 ≤ intervals.length ≤ 10⁵`
- Each interval has two values: `starti`, `endi`
- `0 ≤ starti < endi ≤ 5 × 10⁴`

---

## 💻 Code

```java
class Solution {
    static int minRemoval(int intervals[][]) {
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        int n = intervals.length, ans = 0, prev = intervals[0][1];
        for(int i = 1; i < n; i++){
            if(prev <= intervals[i][0]){
                prev = intervals[i][1];
            } else{
                ans++;
                prev = Math.min(prev, intervals[i][1]);
            }
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
