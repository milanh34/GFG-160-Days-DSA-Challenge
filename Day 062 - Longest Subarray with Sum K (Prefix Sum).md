<h1 align="center">📏 Longest Subarray with Sum K 📏</h1>

---

## 📝 Problem Statement

Given an array `arr[]` containing integers and an integer `k`, your task is to find the **length of the longest subarray** where the **sum of its elements is equal to `k`**.  
If no such subarray exists, return `0`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [10, 5, 2, 7, 1, -10], k = 15
```

**Output:**  
```
6
```

**Explanation:**  
The subarray `[10, 5, 2, 7, 1, -10]` has a sum of 15. Its length is 6, which is the longest.

---

### ✅ Example 2:

**Input:**  
```
arr = [-5, 8, -14, 2, 4, 12], k = -5
```

**Output:**  
```
5
```

**Explanation:**  
The subarray `[-5, 8, -14, 2, 4]` has a sum of -5 and is the longest such subarray.

---

### ✅ Example 3:

**Input:**  
```
arr = [10, -10, 20, 30], k = 5
```

**Output:**  
```
0
```

**Explanation:**  
There is no subarray with a sum of 5.

---

## 🧠 Approach

### Prefix Sum + HashMap Method:

1. Initialize a `prefix` sum variable as 0.
2. Use a `HashMap` to store the **first occurrence** of each prefix sum.
3. Traverse the array:
   - Add the current element to `prefix`.
   - If `prefix == k`, update the answer to `i + 1`.
   - If `prefix - k` is found in the map, a subarray with sum `k` exists — update max length.
   - Use `putIfAbsent()` to ensure we store the **earliest index** for each prefix sum.
4. Return the maximum length found.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                     |
|------------|-------|---------------------------------|
| Time       | O(N)  | Single pass through the array   |
| Space      | O(N)  | Storing prefix sums in a map    |

---

## 🎯 Constraints

- 1 ≤ arr.length ≤ 10⁵  
- -10⁴ ≤ arr[i] ≤ 10⁴  
- -10⁹ ≤ k ≤ 10⁹

---

## 💻 Code

```java
class Solution {
    public int longestSubarray(int[] arr, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        int n = arr.length, prefix = 0, ans = 0;
        for(int i = 0; i < n; i++){
            if((prefix += arr[i]) == k){
                ans = i + 1;
            }
            if(map.containsKey(prefix - k)){
                ans = Math.max(ans, i - map.get(prefix - k));
            }
            map.putIfAbsent(prefix, i);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
