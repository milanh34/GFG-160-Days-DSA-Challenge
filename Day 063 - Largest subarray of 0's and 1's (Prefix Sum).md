<h1 align="center">🟰 Largest Subarray of 0's and 1's 🟰</h1>

---

## 📝 Problem Statement

Given a binary array `arr[]` consisting of only `0`s and `1`s, find the **length of the longest subarray** that contains an **equal number of 0s and 1s**.  
If no such subarray exists, return `0`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [1, 0, 1, 1, 1, 0, 0]
```

**Output:**  
```
6
```

**Explanation:**  
- The subarray `[0, 1, 1, 1, 0, 0]` has 3 zeros and 3 ones.

---

### ✅ Example 2:

**Input:**  
```
arr = [0, 0, 1, 1, 0]
```

**Output:**  
```
4
```

**Explanation:**  
- The subarrays `[0, 0, 1, 1]` and `[0, 1, 1, 0]` both have 2 zeros and 2 ones.

---

### ✅ Example 3:

**Input:**  
```
arr = [0]
```

**Output:**  
```
0
```

**Explanation:**  
- There is no subarray with equal number of 0s and 1s.

---

## 🧠 Approach

### Transform + Prefix Sum Method:

1. **Convert 0s to -1s:**  
   This way, the problem reduces to finding the longest subarray with **sum = 0**.
2. Initialize a `prefix` variable to store running sum.
3. Use a `HashMap` to store the **first occurrence** of each prefix sum.
4. If at any index the prefix sum is 0, the subarray from `0` to `i` is balanced.
5. If a prefix is repeated, it means the subarray between those two indices has sum 0 → update maximum length.
6. Return the length of the longest such subarray.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                  |
|------------|--------|------------------------------|
| Time       | O(N)   | Single pass through the array |
| Space      | O(N)   | Storing prefix sums in map    |

---

## 🎯 Constraints

- 1 ≤ arr.length ≤ 10⁵  
- 0 ≤ arr[i] ≤ 1

---

## 💻 Code

```java
class Solution {
    public int maxLen(int[] arr) {
        Map<Integer, Integer> map = new HashMap<>();
        int n = arr.length, prefix = 0, ans = 0;
        for(int i = 0; i < n; i++){
            prefix += (arr[i] == 1) ? 1 : -1;
            if(prefix == 0){
                ans = i + 1;
            } else if(map.containsKey(prefix)){
                ans = Math.max(ans, i - map.get(prefix));
            } else{
                map.put(prefix, i);
            }
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
