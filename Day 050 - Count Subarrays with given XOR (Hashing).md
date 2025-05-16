<h1 align="center">❌ Count Subarrays with Given XOR ❌</h1>

---

## 📝 Problem Statement

Given an array of integers `arr[]` and an integer `k`, count the number of subarrays whose XOR of elements is exactly equal to `k`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [4, 2, 2, 6, 4], k = 6
```
**Output:**
```
4
```
**Explanation:**
- Subarrays with XOR `6` are:
  - `[4, 2]` → 4 ^ 2 = 6.
  - `[4, 2, 2, 6, 4]` → 4 ^ 2 ^ 2 ^ 6 ^ 4 = 6.
  - `[2, 2, 6]` → 2 ^ 2 ^ 6 = 6.
  - `[6]` → 6.

---

### ✅ Example 2:
**Input:**
```
arr = [5, 6, 7, 8, 9], k = 5
```
**Output:**
```
2
```
**Explanation:**
- Subarrays with XOR `5` are:
  - `[5]`.
  - `[5, 6, 7, 8, 9]` → 5 ^ 6 ^ 7 ^ 8 ^ 9 = 5.

---

### ✅ Example 3:
**Input:**
```
arr = [1, 1, 1, 1], k = 0
```
**Output:**
```
4
```
**Explanation:**
- Subarrays with XOR `0` are:
  - `[1, 1]` (from index 0 to 1).
  - `[1, 1]` (from index 1 to 2).
  - `[1, 1]` (from index 2 to 3).
  - `[1, 1, 1, 1]` (whole array).

---

## 🧠 Approach

- Use **prefix XOR with hashmap** approach.
- Maintain the **prefix XOR up to current element**.
- If `(prefix XOR ^ k)` exists in the map, it means there is a prefix whose XOR with the current prefix is `k`.
- Also check if the current prefix XOR itself is `k`.
- Use a map to keep the frequency of each prefix XOR seen so far.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value    | Description                          |
|------------------|----------|--------------------------------------|
| 🕒 Time          | O(N)     | Process each element once            |
| 📦 Space         | O(N)     | Storing prefix XORs in map           |

Where `N` is the size of the array.

---

## 🎯 Constraints

- 1 ≤ arr.length ≤ 10<sup>5</sup>
- 0 ≤ arr[i] ≤ 10<sup>5</sup>
- 0 ≤ k ≤ 10<sup>5</sup>

---

## 💻 Code

```java
class Solution {
    public long subarrayXor(int arr[], int k) {
        Map<Integer, Integer> map = new HashMap<>();
        long ans = 0;
        int xor = 0;
        for(int i: arr){
            xor = xor ^ i;
            ans += map.getOrDefault(xor ^ k, 0);
            if(xor == k){
                ans++;
            }
            map.put(xor, map.getOrDefault(xor, 0) + 1);
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. **Prefix XOR Concept:**
    - Calculate the XOR of all elements from the start to the current element.
    - If `prefix XOR ^ k` exists in the map, it indicates that the XOR from that point to the current index is `k`.

2. **HashMap Usage:**
    - The key is the prefix XOR.
    - The value is the number of times this XOR has occurred.
    - This allows fast lookups to check for matching subarrays.

3. **Counting Logic:**
    - If `xor ^ k` exists in map, add its frequency to the answer.
    - If current `xor` is equal to `k`, increment the answer directly.

4. **Efficiency:**
    - By using prefix XOR and map, we avoid checking all subarrays using brute force, reducing time to linear.

---

> Made with ❤️ by Milan Haria
