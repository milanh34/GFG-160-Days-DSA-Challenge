<h1 align="center">➕ Find All Triplets with Zero Sum ➕</h1>

---

## 📝 Problem Statement

Given an array `arr[]`, find all possible **triplets of indices** `(i, j, k)` such that:

- `arr[i] + arr[j] + arr[k] = 0`
- `i < j < k`

Each triplet should be returned as a list of indices in ascending order.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [0, -1, 2, -3, 1]
```
**Output:**
```
[[0, 1, 4], [2, 3, 4]]
```
**Explanation:**  
Triplets with zero sum:
- arr[0] + arr[1] + arr[4] = 0 + (-1) + 1 = 0  
- arr[2] + arr[3] + arr[4] = 2 + (-3) + 1 = 0

---

### ✅ Example 2:
**Input:**
```
arr = [1, -2, 1, 0, 5]
```
**Output:**
```
[[0, 1, 2]]
```
**Explanation:**  
Only one valid triplet: arr[0] + arr[1] + arr[2] = 1 + (-2) + 1 = 0

---

### ✅ Example 3:
**Input:**
```
arr = [2, 3, 1, 0, 5]
```
**Output:**
```
[[]]
```
**Explanation:**  
No triplets found with sum 0.

---

## 🧠 Approach

- Use a **HashMap** to store all elements and their indices seen so far.
- For each pair `(i, j)` where `i < j`, calculate the number needed to make the sum zero.
- If the required number exists in the map with index `< i`, we form a valid triplet `(x, i, j)` where `x` is retrieved from the map.
- Add all such triplets to the result list.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value      | Description                                       |
|------------------|------------|---------------------------------------------------|
| 🕒 Time          | `O(n²)`    | Two nested loops plus constant-time map lookups   |
| 📦 Space         | `O(n)`     | HashMap to store seen elements and their indices  |

---

## 🎯 Constraints

- `3 ≤ arr.length ≤ 10³`
- `-10⁴ ≤ arr[i] ≤ 10⁴`

---

## 💻 Code

```java
class Solution {
    public List<List<Integer>> findTriplets(int[] arr) {
        HashMap<Integer, ArrayList<Integer>> map = new HashMap<>();
        int n = arr.length;
        List<List<Integer>> ans = new ArrayList<>();
        for(int i = 1; i < n; i++){
            if(!map.containsKey(arr[i - 1])){
                map.put(arr[i - 1], new ArrayList<>());
            }
            map.get(arr[i - 1]).add(i - 1);
            for(int j = i + 1; j < n; j++){
                int num = -arr[i] - arr[j];
                if(map.containsKey(num)){
                    for(int x: map.get(num)){
                        List<Integer> l = new ArrayList<>();
                        l.add(x);
                        l.add(i);
                        l.add(j);
                        ans.add(l);
                    }
                }
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- For every index `i`, we track all previous elements using a hashmap.
- Then for each index `j > i`, we check if there exists an index `x < i` such that `arr[x] + arr[i] + arr[j] == 0`.
- If yes, we form a valid sorted triplet `(x, i, j)` and add it to the result.
- The internal structure ensures `i < j < k`, and all such combinations are explored.

---

> Made with ❤️ by Milan Haria
