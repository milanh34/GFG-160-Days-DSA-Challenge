<h1 align="center">📅 Activity Selection 📅</h1>

---

## 📝 Problem Statement

You are given two arrays:  
- `start[]` → **start times** of activities  
- `finish[]` → **finish times** of activities  

A person can perform only **one activity at a time** (no overlapping).  
Your task is to determine the **maximum number of activities** that can be completed in a single day.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
start = [1, 3, 0, 5, 8, 5]
finish = [2, 4, 6, 7, 9, 9]
```

**Output:**
```
4
```

**Explanation:**  
The person can perform activities {0, 1, 3, 4} for a total of 4 activities.

---

### ✅ Example 2:

**Input:**
```
start = [10, 12, 20]
finish = [20, 25, 30]
```

**Output:**
```
1
```

**Explanation:**  
Only one activity can be selected since all activities overlap.

---

### ✅ Example 3:

**Input:**
```
start = [1, 3, 2, 5]
finish = [2, 4, 3, 6]
```

**Output:**
```
3
```

**Explanation:**  
The person can perform activities {0, 1, 3}.

---

## 🧠 Approach

We can solve this problem using the **Greedy Algorithm**:

1. Store activities as pairs of `(start, finish)` times.
2. Sort the activities by **finish time** (earliest first).  
   - If two activities finish at the same time, sort by start time.
3. Always select the first activity.
4. For each next activity:
   - If its **start time** is greater than the **finish time** of the last selected activity, select it.
5. Count the number of selected activities.

---

## ⏱️ Time and Space Complexity

| Complexity | Value         | Description                               |
|------------|--------------|-------------------------------------------|
| Time       | O(N log N)   | Sorting activities based on finish time    |
| Space      | O(N)         | Storing activity pairs for sorting         |

---

## 🎯 Constraints

- 1 ≤ `start.length` = `finish.length` ≤ 2 × 10⁵  
- 0 ≤ `start[i]` ≤ `finish[i]` ≤ 10⁹  

---

## 💻 Code

```java
class Solution {
    public int activitySelection(int[] start, int[] finish) {
        int n = start.length, ans = 1, j = 0;
        int[][] time = new int[n][2];
        for(int i = 0; i < n; i++){
            time[i][0] = start[i];
            time[i][1] = finish[i];
        }
        Arrays.sort(time, (a, b) -> {
            if(a[1] == b[1]){
                return a[0] - b[0];
            }
            return a[1] - b[1];
        });
        for(int i = 1; i < n; i++){
            if(time[i][0] > time[j][1]){
                ans++;
                j = i;
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **Activity storage**:
The start and finish times are stored together in a 2D array time[][] for easier sorting.
- **Sorting**:
Activities are sorted based on finish time (and start time in case of a tie) to ensure we always pick the earliest finishing activity.
- **Selection loop**:
We iterate through activities and select one if it starts after the last selected activity finishes.
- **Result**:
The count ans represents the maximum number of non-overlapping activities.

---

> Made with ❤️ by Milan Haria
