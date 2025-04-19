<h1 align="center">🔢 Count Inversions 🔢</h1>

---

## 📝 Problem Statement

Given an array of integers `arr[]`, find the **Inversion Count** in the array.

### What is an Inversion?
Two elements `arr[i]` and `arr[j]` form an inversion if `arr[i] > arr[j]` and `i < j`.

### Inversion Count:
- The inversion count indicates how far (or close) the array is from being sorted. 
- If the array is already sorted, the inversion count is 0.
- If the array is sorted in reverse order, the inversion count is the maximum.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr[] = [2, 4, 1, 3, 5]
```

**Output:**  
```
3
```

**Explanation:**  
The sequence has three inversions:  
- (2, 1)
- (4, 1)
- (4, 3)

---

### ✅ Example 2:
**Input:**  
```
arr[] = [2, 3, 4, 5, 6]
```

**Output:**  
```
0
```

**Explanation:**  
Since the sequence is already sorted, the inversion count is 0.

---

### ✅ Example 3:
**Input:**  
```
arr[] = [10, 10, 10]
```

**Output:**  
```
0
```

**Explanation:**  
All elements are the same, so there are no inversions.

---

## 🧠 Approach

We can solve the problem using **Merge Sort**, as it helps in counting inversions during the merge process.

### Steps:
1. **Divide** the array into two halves.
2. **Recursively sort** the two halves while counting inversions in each half.
3. During the **merge step**, count the inversions:
   - If an element from the right half is smaller than an element from the left half, it contributes inversions.
4. The number of inversions is the sum of:
   - Inversions in the left half.
   - Inversions in the right half.
   - Inversions caused during merging.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                               |
|------------------|-----------|-------------------------------------------|
| 🕒 Time          | `O(n log n)` | Merge Sort works in `O(n log n)` time.    |
| 📦 Space         | `O(n)`    | We use an extra array for merging.        |

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10⁵`
- `1 ≤ arr[i] ≤ 10⁴`

---

## 💻 Code

```java
class Solution {
    static int merge(int[] arr, int[] nums, int beg, int mid, int end){
        int ans = 0, i = beg, j = mid + 1, k = beg;
        while(i <= mid && j <= end){
            if(arr[i] > arr[j]){
                nums[k] = arr[j];
                k++;
                j++;
                ans += (mid - i + 1);
            } else{
                nums[k] = arr[i];
                k++;
                i++;
            }
        }
        while(i <= mid){
            nums[k] = arr[i];
            k++;
            i++;
        }
        while(j <= end){
            nums[k] = arr[j];
            k++;
            j++;
        }
        for(i = beg; i <= end; i++){
            arr[i] = nums[i];
        }
        return ans;
    }
    static int mergeSort(int[] arr, int[] nums, int beg, int end){
        if(beg >= end){
            return 0;
        }
        int ans = 0, mid = beg + (end - beg) / 2;
        ans += mergeSort(arr, nums, beg, mid);
        ans += mergeSort(arr, nums, mid + 1, end);
        ans += merge(arr, nums, beg, mid, end);
        return ans;
    }
    static int inversionCount(int arr[]) {
        return mergeSort(arr, new int[arr.length], 0, arr.length - 1);
    }
}
```

---

## 📝 Explanation of Code

- **merge()**:
  - Merges two sorted halves while counting the inversions.
  - If an element from the right half is smaller than an element from the left half, it forms an inversion with all the remaining elements in the left half.

- **mergeSort()**:
  - Recursively divides the array into two halves.
  - Calls the `merge()` function to merge the two halves and count the inversions.

- **inversionCount()**:
  - Initializes the merge process and returns the total number of inversions.

---


> Made with ❤️ by Milan Haria
