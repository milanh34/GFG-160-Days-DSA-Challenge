<h1 align="center">📊 Subarrays with Sum K 📊</h1>

---

## 📝 Problem Statement

Given an unsorted array of integers, find the number of subarrays having sum exactly equal to a given number `k`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [10, 2, -2, -20, 10], k = -10
```
**Output:**
```
3
```
**Explanation:**
- Subarrays with sum `-10` are:
  - `[10, 2, -2, -20]` → Sum = 10 + 2 + (-2) + (-20) = -10.
  - `[2, -2, -20, 10]` → Sum = 2 + (-2) + (-20) + 10 = -10.
  - `[-20, 10]` → Sum = -20 + 10 = -10.

---

### ✅ Example 2:
**Input:**
```
arr = [9, 4, 20, 3, 10, 5], k = 33
```
**Output:**
```
2
```
**Explanation:**
- Subarrays with sum `33` are:
  - `[9, 4, 20]` → Sum = 9 + 4 + 20 = 33.
  - `[20, 3, 10]` → Sum = 20 + 3 + 10 = 33.

---

### ✅ Example 3:
**Input:**
```
arr = [1, 3, 5], k = 0
```
**Output:**
```
0
```
**Explanation:**
- There is no subarray with sum equal to `0`.

---

## 🧠 Approach

- Use a **prefix sum with hashmap** approach.
- Calculate cumulative sum while iterating.
- If `(current sum - k)` has appeared before, that means the subarray sum from that point to the current index is `k`.
- Keep counting such cases.

This approach uses **HashMap to store the frequency of prefix sums** seen so far, enabling O(1) lookups for checking if a subarray with sum `k` exists ending at current index.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value                | Description                           |
|------------------|----------------------|---------------------------------------|
| 🕒 Time          | O(N)                 | Process each element once            |
| 📦 Space         | O(N)                 | Storing prefix sums in map            |

Where `N` is the size of the array.

---

## 🎯 Constraints

- 1 ≤ arr.length ≤ 10<sup>5</sup>
- -10<sup>3</sup> ≤ arr[i] ≤ 10<sup>3</sup>
- -10<sup>7</sup> ≤ k ≤ 10<sup>7</sup>

---

## 💻 Code

```java
class Solution {
    public int countSubarrays(int arr[], int k) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);
        int ans = 0, sum = 0;
        for(int i: arr){
            sum += i;
            ans += map.getOrDefault(sum - k, 0);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. **Prefix Sum Concept:**
    - We calculate the sum of all elements from the start to the current element.
    - If `sum - k` exists in the map, then there exists a subarray ending at the current index whose sum is `k`.

2. **HashMap Usage:**
    - The key is the prefix sum.
    - The value is the number of times this sum has occurred.
    - This allows us to handle multiple cases where subarrays with the same sum start at different indices.

3. **Initialization:**
    - The map is initialized with `{0: 1}` to handle cases where the subarray starts from index `0`.

4. **Efficient Counting:**
    - Instead of checking all subarrays using nested loops, we use the map to count in `O(1)` time for each element.

---

> Made with ❤️ by Milan Haria
