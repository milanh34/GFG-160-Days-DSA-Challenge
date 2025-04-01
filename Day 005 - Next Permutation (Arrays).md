<h1 align="center">✨ Next Permutation ✨</h1>

---

## 🧩 Problem Statement

Given an array `arr[]` representing a **permutation**, generate the **next lexicographically greater** permutation.  
If no such permutation exists (i.e., the current one is the last), return the **first permutation** (i.e., sorted in ascending order).

> 🎲 A permutation is simply a rearrangement of the array's elements.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
arr = [2, 4, 1, 7, 5, 0]
```

**Output:**  
```
[2, 4, 5, 0, 1, 7]
```

**Explanation:**  
The next lexicographical permutation after `[2, 4, 1, 7, 5, 0]` is `[2, 4, 5, 0, 1, 7]`. After swapping and rearranging the suffix, this is the next valid permutation.

---

### ✅ Example 2:
**Input:**  
```
arr = [3, 2, 1]
```

**Output:**  
```
[1, 2, 3]
```

**Explanation:**  
This is the last permutation in lexicographical order. So, we wrap around and return the first permutation, which is `[1, 2, 3]`.

---

### ✅ Example 3:
**Input:**  
```
arr = [3, 4, 2, 5, 1]
```

**Output:**  
```
[3, 4, 5, 1, 2]
```

**Explanation:**  
The next permutation after `[3, 4, 2, 5, 1]` is `[3, 4, 5, 1, 2]`. We swap and rearrange the suffix to get the next permutation in line.

---

## 🧠 Approach

> 💡 **Key Idea:**  
We need to find the **next lexicographically greater permutation**. This is done by finding the first index `i` from the end where the array stops being in decreasing order. After this index is found, we swap the element at `i - 1` with the smallest larger element after it, and then rearrange the elements after `i - 1` in ascending order to get the smallest permutation.

### 🧮 Steps:

1. **Find the first pair where the order is violated:**
   - Start from the end of the array and find the first position `i` where `arr[i - 1] < arr[i]`. This marks the position where we need to make a swap to get the next greater permutation.
   - If no such `i` exists, it means the array is in descending order, and we need to return the smallest permutation (i.e., sorted in ascending order).

2. **Find the smallest element larger than `arr[i - 1]`:**
   - Once the position `i` is found, we need to find the smallest element in the suffix (the part of the array after `arr[i - 1]`) that is larger than `arr[i - 1]`.
   - Swap `arr[i - 1]` with this element to create a larger permutation.

3. **Rearrange the suffix to get the smallest lexicographical order:**
   - After the swap, the suffix of the array (the part after `i - 1`) may still be in descending order. To ensure the next permutation is the smallest, we sort this suffix in ascending order.

> 🔁 **If no such index `i` is found (i.e., the array is in descending order),** simply sort the entire array to get the smallest possible permutation.

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Reason |
|------------|-------|--------|
| 🕒 Time     | `O(n log n)` | Due to sorting the suffix (`Arrays.sort`) |
| 📦 Space    | `O(1)` | Done in-place with no extra arrays |

⚠️ *Note:* You can optimize sorting to `O(n)` by reversing the suffix instead of using `Arrays.sort()` — since it's already in descending order.

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`  
- `0 ≤ arr[i] ≤ 10⁵`

---

## 💻 Code

```java
import java.util.Arrays;

class Solution {
    void nextPermutation(int[] arr) {
        int n = arr.length;
        int i = n - 1;
        while(i > 0 && arr[i] <= arr[i - 1]){
            i--;
        }
        if(i > 0){
            int j = n - 1;
            while(j >= i && arr[i - 1] >= arr[j]){
                j--;
            }
            int temp = arr[j];
            arr[j] = arr[i - 1];
            arr[i - 1] = temp;
        }
        Arrays.sort(arr, i, n);
    }
}
```

---

> Made with ❤️ by Milan Haria