<h1 align="center">➕ Insert Interval ➕</h1>

---

## 📝 Problem Statement

You are given a list of **non-overlapping intervals**, where each interval is represented as a pair `[start, end]`. These intervals are already **sorted in ascending order** by their start values.

You are also given a **new interval** `[newStart, newEnd]` which you need to insert into the existing list such that:

- The result list remains sorted.
- All overlapping intervals are merged into a single interval.
- The final list still contains only **non-overlapping intervals**.

Your task is to return the updated list of intervals after inserting and merging.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
intervals = [[1,3], [4,5], [6,7], [8,10]]
newInterval = [5,6]
```

**Output:**  
```
[[1,3], [4,7], [8,10]]
```

**Explanation:**  
The new interval [5,6] overlaps with [4,5] and [6,7]. After merging, we get [4,7].

---

### ✅ Example 2:
**Input:**  
```
intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]]
newInterval = [4,9]
```

**Output:**  
```
[[1,2], [3,10], [12,16]]
```

**Explanation:**  
The new interval [4,9] overlaps with [3,5], [6,7], and [8,10]. After merging, we get [3,10].

---

## 🧠 Approach

1. **Check Boundary Cases**:
   - If `newInterval` lies **before** all intervals → Insert at the beginning.
   - If it lies **after** all intervals → Insert at the end.

2. **Merge Intervals**:
   - Loop through each interval and:
     - If overlapping, merge them.
     - If not, add them to the result.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value       | Description                              |
|------------------|-------------|------------------------------------------|
| 🕒 Time          | `O(n)`      | We visit each interval once              |
| 📦 Space         | `O(n)`      | Output list to store merged intervals    |

---

## 🎯 Constraints

- `1 ≤ intervals.length ≤ 10⁵`
- `0 ≤ start[i], end[i] ≤ 10⁹`

---

## 💻 Code

```java
class Solution {
    static ArrayList<int[]> insertInterval(int[][] intervals, int[] newInterval) {
        int n = intervals.length, a = newInterval[0], b = newInterval[1];
        ArrayList<int[]> ans = new ArrayList<>();
        if(b < intervals[0][0]){
            ans.add(newInterval);
            for(int[] i: intervals){
                ans.add(i);
            }
        } else if(a > intervals[n - 1][1]){
            for(int[] i: intervals){
                ans.add(i);
            }
            ans.add(newInterval);
        } else{
            int i = 0;
            while(i < n){
                int beg = intervals[i][0], end = intervals[i][1];
                if(a >= beg && a <= end){
                    beg = Math.min(beg, a);
                    end = Math.max(end, b);
                    i++;
                    while(i < n && end >= intervals[i][0]){
                        end = Math.max(end, intervals[i][1]);
                        i++;
                    }
                    ans.add(new int[]{ beg, end });
                    break;
                } else if(a < beg){
                    if(b < beg){
                        ans.add(newInterval);
                        break;
                    } else{
                        i++;
                        end = Math.max(end, b);
                        while(i < n && end >= intervals[i][0]){
                            end = Math.max(end, intervals[i][1]);
                            i++;
                        }
                        ans.add(new int[]{ a, end });
                        break;
                    }
                }
                ans.add(intervals[i]);
                i++;
            }
            while(i < n){
                ans.add(intervals[i]);
                i++;
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- First, we initialize variables for the new interval's start and end, as well as the result list to store the final merged intervals.
- If the new interval comes **before all existing intervals** (i.e., its end is less than the start of the first interval), we simply insert it at the beginning and append all original intervals afterward.
- If the new interval comes **after all existing intervals** (i.e., its start is greater than the end of the last interval), we add all existing intervals first, then append the new interval at the end.
- For all other cases (where overlaps may occur), we traverse the intervals:
  - If the new interval **overlaps** with the current interval, we find the **merged interval** by updating the start to the minimum and the end to the maximum of the overlapping range.
  - We continue merging as long as overlaps exist with the new interval.
  - Once merging is done, we add the merged interval to the result.
- Any intervals that **do not overlap** with the new interval are directly added to the result list.
- Finally, we ensure all **remaining intervals** are appended after the merged portion.

---

> Made with ❤️ by Milan Haria
