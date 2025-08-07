<h1 align="center">🚉 Minimum Platforms 🚉</h1>

---

## 📝 Problem Statement

You are given two arrays:  
- `arr[]` → **arrival times** of trains  
- `dep[]` → **departure times** of trains  

Your task is to find the **minimum number of platforms** required so that no train waits for a platform.

> **Note:**  
> - Times are given in 24-hour format (`HHMM`).  
> - If a train arrives before another departs, both need separate platforms.
> - At any given time, the same platform cannot be used for both the arrival of one train and the departure of another

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
arr = [900, 940, 950, 1100, 1500, 1800]
dep = [910, 1200, 1120, 1130, 1900, 2000]
```

**Output:**
```
3
```

**Explanation:**  
From **9:40 to 12:00**, 3 trains are present at the station at the same time. Hence, at least **3 platforms** are required.

---

### ✅ Example 2:

**Input:**
```
arr = [900, 1235, 1100]
dep = [1000, 1240, 1200]
```

**Output:**
```
1
```

**Explanation:**  
All train timings are mutually exclusive, so only **1 platform** is needed.

---

### ✅ Example 3:

**Input:**
```
arr = [1000, 935, 1100]
dep = [1200, 1240, 1130]
```

**Output:**
```
3
```

**Explanation:**  
From **11:00 to 11:30**, all **3 trains** are at the station, so **3 platforms** are required.

---

## 🧠 Approach

We can solve this efficiently using a **difference array** technique:

1. Create an array `time[]` representing each possible minute of the day (0 to 2399).
2. For each arrival time `arr[i]`, increment `time[arr[i]]` by 1 (train arrives).
3. For each departure time `dep[i]`, decrement `time[dep[i] + 1]` (train leaves after its departure time).
4. Calculate the **prefix sum** of `time[]` to get the number of trains present at each minute.
5. The **maximum value** during this process is the minimum number of platforms required.

---

## ⏱️ Time and Space Complexity

| Complexity | Value        | Description                           |
|------------|-------------|---------------------------------------|
| Time       | O(N + T)    | N = number of trains, T = 2400 minutes |
| Space      | O(T)        | Array of size 2400 for time tracking   |

---

## 🎯 Constraints

- 1 ≤ number of trains ≤ 50,000  
- 0000 ≤ `arr[i]` ≤ `dep[i]` ≤ 2359  

---

## 💻 Code

```java
class Solution {
    static int findPlatform(int arr[], int dep[]) {
        int n = arr.length, ans = 0, count = 0;
        int[] time = new int[2400];
        for(int i = 0; i < n; i++){
            time[arr[i]]++;
            if(dep[i] + 1 < 2400){
                time[dep[i] + 1]--;
            }
        }
        for(int i: time){
            count += i;
            ans = Math.max(ans, count);
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- Marking arrivals → For each train's arrival time `arr[i]`, increment `time[arr[i]]` to indicate a train arrives at that minute.
- Marking departures → For each train's departure time `dep[i]`, decrement `time[dep[i] + 1]` to show the train leaves immediately after its departure time.
- Prefix sum calculation → We iterate through `time[]`, accumulating the number of trains present at each minute `(count)`.
- Tracking maximum platforms → At every minute, update `ans` with the maximum count value found so far, which represents the highest number of platforms needed at once.

---

> Made with ❤️ by Milan Haria
