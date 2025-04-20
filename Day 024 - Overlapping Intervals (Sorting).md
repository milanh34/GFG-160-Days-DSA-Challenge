<h1 align="center">📅 Overlapping Intervals 📅</h1>

---

## 📝 Problem Statement

Given an array of intervals `arr[][]`, where `arr[i] = [starti, endi]`, the task is to **merge all the overlapping intervals**.

### Objective:
- Merge intervals where they overlap and return the merged intervals.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr[][] = [[1,3],[2,4],[6,8],[9,10]]
```

**Output:**  
```
[[1,4], [6,8], [9,10]]
```

**Explanation:**  
- The intervals [1,3] and [2,4] overlap, so they are merged into [1,4].
- The remaining intervals [6,8] and [9,10] do not overlap and are returned as-is.

---

### ✅ Example 2:
**Input:**  
```
arr[][] = [[6,8],[1,9],[2,4],[4,7]]
```

**Output:**  
```
[[1,9]]
```

**Explanation:**  
- All the intervals overlap with the interval [1,9], so they are all merged into [1,9].

---

## 🧠 Approach

The problem can be efficiently solved using the **greedy approach**:
1. **Sort the intervals** by the starting time of each interval.
2. Iterate through the intervals, and for each interval:
   - If it overlaps with the previous interval (i.e., the start time of the current interval is less than or equal to the end time of the previous interval), merge them.
   - Otherwise, add the current interval to the result list as it doesn't overlap with the previous one.

### Steps:
1. **Sort** the intervals based on their starting time.
2. Initialize the first interval as the current range.
3. Iterate through the intervals:
   - If the current interval overlaps with the previous one, merge them by updating the end of the current range.
   - Otherwise, add the current range to the result and update the current range to the new interval.
4. Return the result list containing merged intervals.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                               |
|------------------|-----------|-------------------------------------------|
| 🕒 Time          | `O(n log n)` | Sorting takes `O(n log n)` time.         |
| 📦 Space         | `O(n)`    | Space used for storing the result list.   |

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10⁵`
- `0 ≤ starti ≤ endi ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public List<int[]> mergeOverlap(int[][] arr) {
        Arrays.sort(arr, (a, b) -> a[0] - b[0]);
        List<int[]> ans = new ArrayList<>();
        int n = arr.length;
        int beg = arr[0][0], end = arr[0][1];
        for(int i = 1; i < n; i++){
            if(arr[i][0] <= end){
                end = Math.max(end, arr[i][1]);
            } else{
                ans.add(new int[]{ beg, end });
                beg = arr[i][0];
                end = arr[i][1];
            }
        }
        ans.add(new int[]{ beg, end });
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **mergeOverlap()**:
  - **Sorting**: The intervals are sorted based on the start time to make sure we process them in order.
  - **Merging Logic**:
    - If the current interval overlaps with the previous one (i.e., its start time is less than or equal to the end time of the last merged interval), we merge the two intervals by updating the end time.
    - Otherwise, we add the current interval as a separate interval to the result list.
  - Finally, we add the last merged interval to the result.

---

> Made with ❤️ by Milan Haria
