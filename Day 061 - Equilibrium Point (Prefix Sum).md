<h1 align="center">⚖️ Equilibrium Point ⚖️</h1>

---

## 📝 Problem Statement

Given an array `arr[]`, find the first **equilibrium index** such that the **sum of elements before** it is equal to the **sum of elements after** it.  
If no such index exists, return `-1`.

> **Note:** The equilibrium index is based on **0-based indexing**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [1, 2, 0, 3]
```

**Output:**  
```
2
```

**Explanation:**  
- Left of index 2: 1 + 2 = 3  
- Right of index 2: 3  
- Both sums are equal, so index 2 is the equilibrium point.

---

### ✅ Example 2:

**Input:**  
```
arr = [1, 1, 1, 1]
```

**Output:**  
```
-1
```

**Explanation:**  
- No index satisfies the equilibrium condition.

---

### ✅ Example 3:

**Input:**  
```
arr = [-7, 1, 5, 2, -4, 3, 0]
```

**Output:**  
```
3
```

**Explanation:**  
- Left of index 3: -7 + 1 + 5 = -1  
- Right of index 3: -4 + 3 + 0 = -1  
- Index 3 is the equilibrium point.

---

## 🧠 Approach

### Prefix Sum Method:

1. Create two auxiliary arrays:
   - `left[i]` → sum of elements from index `0` to `i`
   - `right[i]` → sum of elements from index `i` to `n-1`
2. Traverse `left[]` from start:
   - `left[i] = left[i-1] + arr[i]`
3. Traverse `right[]` from end:
   - `right[i] = right[i+1] + arr[i]`
4. Finally, for each index `i`, if `left[i] == right[i]`, return `i`.
5. If no match found, return `-1`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value     | Description               |
|------------|------------|---------------------------|
| Time       | O(N)      | Three passes over the array |
| Space      | O(N)      | Two extra arrays of size N |

---

## 🎯 Constraints

- 3 ≤ arr.length ≤ 10⁵  
- -10⁴ ≤ arr[i] ≤ 10⁴

---

## 💻 Code

```java
class Solution {
    public static int findEquilibrium(int arr[]) {
        int n = arr.length;
        int[] left = new int[n], right = new int[n];
        left[0] = arr[0];
        right[n - 1] = arr[n - 1];
        for(int i = 1; i < n; i++){
            left[i] = left[i - 1] + arr[i];
        }
        for(int i = n - 2; i >= 0; i--){
            right[i] = right[i + 1] + arr[i];
        }
        for(int i = 0; i < n; i++){
            if(left[i] == right[i]){
                return i;
            }
        }
        return -1;
    }
}
```

---

> Made with ❤️ by Milan Haria
