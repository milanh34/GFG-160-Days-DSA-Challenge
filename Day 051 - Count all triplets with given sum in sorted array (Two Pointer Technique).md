<h1 align="center">🔢 Count All Triplets With Given Sum In Sorted Array 🔢</h1>

---

## 📝 Problem Statement

Given a **sorted array** `arr[]` and a target value, count the number of triplets `(i, j, k)` with **distinct indices** such that:

```
arr[i] + arr[j] + arr[k] == target
```
Where `i < j < k`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [-3, -1, -1, 0, 1, 2], target = -2
```
**Output:**
```
4
```
**Explanation:**
Triplets:
- `(-3) + 0 + 1 = -2`
- `(-3) + (-1) + 2 = -2` (occurs twice with duplicate -1s)
- `(-1) + (-1) + 0 = -2`

---

### ✅ Example 2:
**Input:**
```
arr = [-2, 0, 1, 1, 5], target = 1
```
**Output:**
```
0
```
**Explanation:**
No such triplet exists.

---

## 🧠 Approach

- Use **hash map + two pointers** logic.
- Fix one element and use a map to check if the remaining two elements form the target sum.
- Since the array is **sorted**, we can avoid duplicates efficiently.
- Iterate with `i` and `j`, then look for `(target - arr[i] - arr[j])` in map of previous elements.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                     |
|------------------|-----------|---------------------------------|
| 🕒 Time          | O(N²)     | Nested loops for pairs          |
| 📦 Space         | O(N)      | HashMap for previous elements   |

---

## 🎯 Constraints

- 3 ≤ arr.length ≤ 10⁴  
- -10⁵ ≤ arr[i], target ≤ 10⁵

---

## 💻 Code

```java
class Solution {
    public int countTriplets(int[] arr, int target) {
        int n = arr.length, ans = 0;
        Map<Integer, Integer> map = new HashMap<>();
        map.put(arr[0], 1);
        for(int i = 1; i < n; i++){
            int a = arr[i];
            for(int j = i + 1; j < n; j++){
                if(map.containsKey(target - arr[j] - a)){
                    ans += map.get(target - arr[j] - a);
                }
            }
            map.put(a, map.getOrDefault(a, 0) + 1);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
