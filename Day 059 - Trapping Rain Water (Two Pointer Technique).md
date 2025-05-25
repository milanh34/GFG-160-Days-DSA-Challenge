<h1 align="center">🌧️ Trapping Rain Water 🌧️</h1>

---

## 📝 Problem Statement

You are given an array `arr[]` representing the height of blocks. Each block has a width of 1.  
Compute how much **rainwater** can be trapped between the blocks after raining.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [3, 0, 1, 0, 4, 0, 2]
```

**Output:**  
```
10
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/701211/Web/Other/blobid0_1741784862.png"> </img>
- Water at index 1 = 3  
- Water at index 2 = 2  
- Water at index 3 = 3  
- Water at index 5 = 2  
Total = `3 + 2 + 3 + 2 = 10`

---

### ✅ Example 2:

**Input:**  
```
arr = [3, 0, 2, 0, 4]
```

**Output:**  
```
7
```

**Explanation:**  
- Water at index 1 = 3  
- Water at index 2 = 1  
- Water at index 3 = 3  
Total = `3 + 1 + 3 = 7`

---

### ✅ Example 3:

**Input:**  
```
arr = [1, 2, 3, 4]
```

**Output:**  
```
0
```

**Explanation:**  
No water can be trapped as there is no block bounded on both sides.

---

### ✅ Example 4:

**Input:**  
```
arr = [2, 1, 5, 3, 1, 0, 4]
```

**Output:**  
```
9
```

**Explanation:**  
- Water at index 1 = 1  
- Water at index 3 = 1  
- Water at index 4 = 3  
- Water at index 5 = 4  
Total = `1 + 1 + 3 + 4 = 9`

---

## 🧠 Approach

### Two-Pointer Technique:

We move two pointers from both ends (`beg` from left and `end` from right) while maintaining:
- `max1` – the highest block seen from the left
- `max2` – the highest block seen from the right

At each step:
- If the block at `beg` is smaller than the one at `end`, the trapped water depends on the left side (`max1`).
  - If `arr[beg]` is less than `max1`, then water can be trapped at this index: `max1 - arr[beg]`.
  - Move `beg` to the right.
- Else, we process from the right.
  - If `arr[end]` is less than `max2`, then water can be trapped at this index: `max2 - arr[end]`.
  - Move `end` to the left.

This continues until `beg` and `end` meet.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description              |
|------------|--------|--------------------------|
| Time       | O(N)   | Linear traversal         |
| Space      | O(1)   | Constant extra space     |

---

## 🎯 Constraints

- 2 ≤ arr.length < 10⁵  
- 0 < arr[i] < 10³

---

## 💻 Code

```java
class Solution {
    public int maxWater(int arr[]) {
        int beg = 0, end = arr.length - 1, ans = 0, max1 = 0, max2 = 0;
        while(beg < end){
            if(arr[beg] < arr[end]){
                max1 = Math.max(max1, arr[beg]);
                ans += max1 - arr[beg];
                beg++;
            } else{
                max2 = Math.max(max2, arr[end]);
                ans += max2 - arr[end];
                end--;
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- `beg` and `end` are pointers starting from the left and right of the array.
- `max1` keeps track of the maximum height seen so far from the left.
- `max2` keeps track of the maximum height seen so far from the right.
- `ans` stores the total water trapped.

### Working:

1. While `beg < end`:
   - If `arr[beg] < arr[end]`:
     - Update `max1` to be the maximum of itself and `arr[beg]`.
     - Water at index `beg` is `max1 - arr[beg]`.
     - Move `beg` to the right.
   - Else:
     - Update `max2` to be the maximum of itself and `arr[end]`.
     - Water at index `end` is `max2 - arr[end]`.
     - Move `end` to the left.
2. Continue this until `beg` and `end` meet.

This ensures we are always considering the minimum of the two max heights (left and right) as the boundary.

---

> Made with ❤️ by Milan Haria
