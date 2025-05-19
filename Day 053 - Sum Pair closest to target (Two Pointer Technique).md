<h1 align="center">🔍 Sum Pair Closest to Target 🔍</h1>

---

## 📝 Problem Statement

Given an array `arr[]` and a number `target`, find a **pair of elements** `(a, b)` in `arr[]`, where `a <= b`, such that their **sum is closest to the target**.

### Note:
- Return the pair in **sorted order**.
- If **multiple pairs** have the same closest sum, choose the pair with the **maximum absolute difference**.
- If **no such pair exists** (i.e., array length < 2), return an empty array.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = [10, 30, 20, 5], target = 25
```
**Output:**
```
[5, 20]
```
**Explanation:** 5 + 20 = 25, which is exactly the target.

---

### ✅ Example 2:
**Input:**
```
arr = [5, 2, 7, 1, 4], target = 10
```
**Output:**
```
[2, 7]
```
**Explanation:** 
- Both [4, 7] and [2, 7] are equally close to 10.
- [2, 7] has a higher absolute difference (5 > 3), so it is selected.

---

### ✅ Example 3:
**Input:**
```
arr = [10], target = 10
```
**Output:**
```
[]
```
**Explanation:** Array has only one element, so no pair exists.

---

## 🧠 Approach

1. **Sort the array**.
2. Use the **two-pointer technique** (`beg`, `end`) to try combinations from both ends.
3. Track the **closest sum** and **maximum absolute difference**.
4. Update result accordingly.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                    |
|------------------|-----------|--------------------------------|
| 🕒 Time          | O(N log N) | Due to sorting                 |
| 📦 Space         | O(1)      | Only a few variables used      |

---

## 🎯 Constraints

- 1 ≤ arr.length ≤ 2×10⁵  
- 0 ≤ target ≤ 2×10⁵  
- 0 ≤ arr[i] ≤ 10⁵  

---

## 💻 Code

```java
class Solution {
    public List<Integer> sumClosest(int[] arr, int target) {
         Arrays.sort(arr);
         int beg = 0, end = arr.length - 1, diff = Integer.MAX_VALUE;
         List<Integer> ans = new ArrayList<>();
         while(beg < end){
             int sum = arr[beg] + arr[end];
             if(Math.abs(target - sum) < diff){
                 diff = Math.abs(target - sum);
                 ans = Arrays.asList(arr[beg], arr[end]);
             }
             if(sum > target){
                 end--;
             } else if(sum < target){
                 beg++;
             } else{
                 return ans;
             }
         }
         return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
