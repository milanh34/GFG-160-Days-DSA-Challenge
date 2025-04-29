<h1 align="center">🐄 Aggressive Cows 🐄</h1>

---

## 📝 Problem Statement

You are given an array `stalls[]` where each element represents the position of a stall.  
Also given is an integer `k` representing the number of **aggressive cows**.  
You must place the cows in the stalls such that the **minimum distance** between any two cows is **as large as possible**.

Return the **largest minimum distance** possible.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
stalls = [1, 2, 4, 8, 9], k = 3
```
**Output:**
```
3
```
**Explanation:**  
Place cows at positions `1`, `4`, and `8`.  
Minimum distance between any two cows = `3`.

---

### ✅ Example 2:
**Input:**
```
stalls = [10, 1, 2, 7, 5], k = 3
```
**Output:**
```
4
```
**Explanation:**  
Sorted stalls: `[1, 2, 5, 7, 10]`  
Place cows at `1`, `5`, and `10`. Minimum distance = `4`.

---

### ✅ Example 3:
**Input:**
```
stalls = [2, 12, 11, 3, 26, 7], k = 5
```
**Output:**
```
1
```
**Explanation:**  
Sorted stalls: `[2, 3, 7, 11, 12, 26]`  
There are exactly 6 stalls and we want to place 5 cows. The best minimum distance possible is 1.

---

## 🧠 Approach

1. **Sort the stalls**.
2. Use **Binary Search** on the answer (minimum possible distance between cows).
3. For a middle distance value `mid`, try to place all `k` cows:
   - If possible, try to maximize distance by moving right.
   - Otherwise, move left to reduce distance.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                          |
|------------------|-----------|--------------------------------------|
| 🕒 Time          | `O(N log(max - min))` | Sorting + Binary Search + Check Loop  |
| 📦 Space         | `O(1)`    | No extra space used                  |

---

## 🔒 Constraints

- `2 ≤ stalls.length ≤ 10⁶`
- `0 ≤ stalls[i] ≤ 10⁸`
- `2 ≤ k ≤ stalls.length`

---

## 💻 Code

```java
class Solution {
    public static int aggressiveCows(int[] stalls, int k) {
        Arrays.sort(stalls);
        int n = stalls.length;
        int beg = 1, end = stalls[n - 1] - stalls[0], ans = 0;
        while(beg <= end){
            int mid = beg + (end - beg) / 2, prev = stalls[0], count = 1;
            for(int i = 1; i < n; i++){
                if(stalls[i] - mid >= prev){
                    count++;
                    prev = stalls[i];
                }
            }
            if(count >= k){
                beg = mid + 1;
                ans = mid;
            } else{
                end = mid - 1;
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **`Arrays.sort(stalls);`**  
  Sorts the stall positions to simplify distance calculations.

- **Binary Search Range:**
  - `beg = 1`: Smallest possible distance.
  - `end = stalls[n-1] - stalls[0]`: Largest possible distance.

- **Loop: `while (beg <= end)`**
  - **`mid`** is the candidate minimum distance between any two cows.
  - Start placing cows from the first stall and count how many cows can be placed such that each next cow is at least `mid` distance apart.
  - If `count >= k`, it's a valid configuration; update answer and try for a larger distance.
  - Else, try for a smaller distance.

- **`return ans;`**  
  This holds the largest minimum distance at which all cows can be placed.

---

> Made with ❤️ by Milan Haria
