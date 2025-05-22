<h1 align="center">🔍 Indexes of Subarray Sum 🔍</h1>

---

## 📝 Problem Statement

Given an array `arr[]` containing only **non-negative integers** and an integer `target`, find the **first continuous subarray** that sums to `target`.  
Return the **1-based** starting and ending indexes of this subarray.  
If no such subarray exists, return `[-1]`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  

```
arr = [1, 2, 3, 7, 5], target = 12
```  

**Output:**  

```
[2, 4]
```  

**Explanation:**  arr[1] + arr[2] + arr[3] = 2 + 3 + 7 = 12

---

### ✅ Example 2:
**Input:**  

```
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], target = 15
```  

**Output:**  

```
[1, 5]
```  

**Explanation:**  1 + 2 + 3 + 4 + 5 = 15

---

### ✅ Example 3:

**Input:**  

```
arr = [5, 3, 4], target = 2
```  

**Output:**  

```
[-1]
```  

**Explanation:**   No subarray with sum = 2

---

## 🧠 Approach

- Use **sliding window technique** with two pointers: `beg` and `end`.
- Start with `sum = arr[0]`, expand the window by increasing `end`.
- Shrink the window from the beginning (`beg`) when the `sum` exceeds the `target`.
- Stop as soon as the first valid subarray is found.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value   | Description                                      |
|------------------|---------|--------------------------------------------------|
| 🕒 Time          | O(N)   | Traverse the array at most once using two pointers |
| 📦 Space         | O(1)   | Only a few variables used; no extra data structure |

---

## 🎯 Constraints

- 1 ≤ arr.length ≤ 10⁶  
- 0 ≤ arr[i] ≤ 10³  
- 0 ≤ target ≤ 10⁹

---

## 💻 Code

```java
class Solution {
    static ArrayList<Integer> subarraySum(int[] arr, int target) {
        int n = arr.length;
        ArrayList<Integer> ans = new ArrayList<>();
        if(n == 1){
            if(arr[0] == target){
                ans.add(1);
                return ans;
            } else{
                ans.add(-1);
                return ans;
            }
        }
        int beg = 0, end = 0, sum = arr[0];
        while(end < n){
            if(sum == target){
                ans.add(beg + 1);
                ans.add(end + 1);
                return ans;
            } else if(sum < target){
                end++;
                if(end < n){
                    sum += arr[end];
                }
            } else{
                if(beg == end){
                    end++;
                    if(end < n){
                        sum += arr[end];
                    }
                }
                sum -= arr[beg];
                beg++;
            }
        }
        ans.add(-1);
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
