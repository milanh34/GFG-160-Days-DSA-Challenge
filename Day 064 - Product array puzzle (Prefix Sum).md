<h1 align="center">🧮 Product Array Puzzle 🧮</h1>

---

## 📝 Problem Statement

Given an array `arr[]`, construct and return a **product array `res[]`** such that `res[i]` is equal to the **product of all elements** in the array **except** `arr[i]`.

> **Note**: The result for each `res[i]` must lie within the 32-bit signed integer range.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [10, 3, 5, 6, 2]
```

**Output:**  
```
[180, 600, 360, 300, 900]
```

**Explanation:**  
- res[0] = 3 * 5 * 6 * 2 = 180  
- res[1] = 10 * 5 * 6 * 2 = 600  
- res[2] = 10 * 3 * 6 * 2 = 360  
- res[3] = 10 * 3 * 5 * 2 = 300  
- res[4] = 10 * 3 * 5 * 6 = 900

---

### ✅ Example 2:

**Input:**  
```
arr = [12, 0]
```

**Output:**  
```
[0, 12]
```

**Explanation:**  
- res[0] = 0  
- res[1] = 12 (since product of all non-zero elements)

---

## 🧠 Approach

### Optimized Math-Based Method:

1. Count how many zeros are in the array.
2. If there are **more than 1 zero**, the result array is filled with `0`s.
3. If there is **exactly 1 zero**, only the index with `0` will get the product of the remaining elements, rest will be `0`.
4. If **no zeros**, simply compute total product and divide each element from the product to get result.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                           |
|------------|--------|---------------------------------------|
| Time       | O(N)   | One pass for product, one for result  |
| Space      | O(N)   | Output array `res[]`                  |

---

## 🎯 Constraints

- 2 ≤ arr.length ≤ 10⁵  
- -100 ≤ arr[i] ≤ 100  

---

## 💻 Code

```java
class Solution {
    public static int[] productExceptSelf(int arr[]) {
        int n = arr.length, product = 1, zeros = 0, zeroProduct = 1;
        for(int i: arr){
            if(i == 0){
                zeros++;
                if(zeros > 1){
                    break;
                }
                zeroProduct = product;
                continue;
            }
            if(zeros == 1){
                zeroProduct *= i;
            } else{
                product *= i;
            }
        }
        int[] ans = new int[n];
        if(zeros > 1){
            for(int i = 0; i < n; i++){
                ans[i] = 0;
            }
        } else if(zeros == 1){
            for(int i = 0; i < n; i++){
                if(arr[i] == 0){
                    ans[i] = zeroProduct;
                } else{
                    ans[i] = 0;
                }
            }
        } else{
            for(int i = 0; i < n; i++){
                ans[i] = product / arr[i];
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **Initialization:**  
  - We use `product` to keep track of the product of all non-zero elements and `zeros` to count the number of zero elements.  
  - If there's exactly one zero, we also track `zeroProduct`, the product of all other elements.

- **First Loop (counting and computing product):**  
  - Count how many zeros are present.
  - If more than one zero, no non-zero product is possible.
  - If only one zero, calculate product of all non-zero elements.
  - Otherwise, compute product of entire array.

- **Second Phase (build result array):**  
  - If more than one zero: all results will be zero.
  - If exactly one zero: only the position with the zero gets the `zeroProduct`, all others get 0.
  - If no zero: divide total product by `arr[i]` to get `res[i]`.

---

> Made with ❤️ by Milan Haria
