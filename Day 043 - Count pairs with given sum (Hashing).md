<h1 align="center">🔗 Count Pairs with Given Sum 🔗</h1>

---

## 📝 Problem Statement

Given an array `arr[]` and an integer `target`, count the **number of pairs** in the array that sum up to the given target.  
Each pair is counted based on occurrences, **even if elements are repeated**.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [1, 5, 7, -1, 5], target = 6
```
**Output:**
```
3
```
**Explanation:**  
Valid pairs are: (1, 5), (7, -1), (1, 5) → 3 pairs.

---

### ✅ Example 2:
**Input:**
```
arr = [1, 1, 1, 1], target = 2
```
**Output:**
```
6
```
**Explanation:**  
All pairs formed with (1,1) → C(4,2) = 6 pairs.

---

### ✅ Example 3:
**Input:**
```
arr = [10, 12, 10, 15, -1], target = 125
```
**Output:**
```
0
```
**Explanation:**  
No pair sums to 125.

---

## 🧠 Approach

- Use a **HashMap** to count occurrences of each number.
- Iterate through the array:
  - For each element `i`, check if `(target - i)` exists in the map.
  - If it does, add the count of `(target - i)` to the answer.
  - Then increment the count of the current element in the map.
- This way, we avoid duplicate counting and ensure each pair is counted based on occurrences.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                                      |
|------------------|-----------|--------------------------------------------------|
| 🕒 Time          | `O(n)`    | Traverse array once with constant-time operations |
| 📦 Space         | `O(n)`    | Extra space for hashmap to store frequencies     |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`
- `-10⁴ ≤ arr[i] ≤ 10⁴`
- `1 ≤ target ≤ 10⁴`

---

## 💻 Code

```java
class Solution {

    int countPairs(int arr[], int target) {
        Map<Integer, Integer> map = new HashMap<>();
        int ans = 0;
        for(int i: arr){
            if(map.containsKey(target - i)){
                ans += map.get(target - i);
            }
            map.put(i, map.getOrDefault(i, 0) + 1);
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- A `HashMap` is used to store the frequency of elements encountered so far.
- For each element `i` in the array:
  - If `target - i` is already in the map, it means we can form that many pairs with `i`.
  - We increment the count of valid pairs accordingly.
- Finally, we return the total number of valid pairs found.

---

> Made with ❤️ by Milan Haria
