<h1 align="center">📏 Longest Bounded-Difference Subarray 📏</h1>

---

## 📝 Problem Statement

Given an array of **positive integers** `arr[]` and a **non-negative integer** `x`, find the **longest contiguous subarray** such that the **absolute difference** between any two elements is **not greater than x**.

If multiple subarrays have the same maximum length, return the one that starts at the **smallest index**.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
arr = [8, 4, 2, 6, 7], x = 4
```

**Output:**  
```
[4, 2, 6]
```

**Explanation:**  
- Subarray `[4, 2, 6]` (index `1..3`) has no two elements with difference greater than 4.

---

### ✅ Example 2

**Input:**  
```
arr = [15, 10, 1, 2, 4, 7, 2], x = 5
```

**Output:**  
```
[2, 4, 7, 2]
```

**Explanation:**  
- Subarray `[2, 4, 7, 2]` (index `3..6`) has no pair with difference greater than 5.

---

## 🧠 Approach

### Key Idea:
- Use the **sliding window technique** with **deques** to efficiently maintain the **minimum and maximum** values in the current window.
- Expand the window (`j`) and shrink from the left (`i`) if the condition `max - min <= x` is violated.
- Track the **longest valid window**.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                                  |
|------------|-------|----------------------------------------------|
| Time       | O(n)  | Each index is pushed and popped at most once |
| Space      | O(n)  | For min and max deques                       |

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10⁵`
- `1 ≤ arr[i] ≤ 10⁹`
- `0 ≤ x ≤ 10⁹`

---

## 💻 Code

```java
class Solution {
    public ArrayList<Integer> longestSubarray(int[] arr, int x) {
        int n = arr.length, beg = 0, end = 0, i = 0, j = 0;
        Deque<Integer> min = new ArrayDeque<>(), max = new ArrayDeque<>();
        ArrayList<Integer> ans = new ArrayList<>();
        while(j < n){
            while(!min.isEmpty() && arr[j] < arr[min.peekLast()]){
                min.pollLast();
            }
            while(!max.isEmpty() && arr[j] > arr[max.peekLast()]){
                max.pollLast();
            }
            min.addLast(j);
            max.addLast(j);
            while(arr[max.peekFirst()] - arr[min.peekFirst()] > x){
                if(i == max.peekFirst()){
                    max.pollFirst();
                }
                if(i == min.peekFirst()){
                    min.pollFirst();
                }
                i++;
            }
            if(j - i > end - beg){
                beg = i;
                end = j;
            }
            j++;
        }
        for(int a = beg; a <= end; a++){
            ans.add(arr[a]);
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. **Variables**:
    - `i` : Left pointer of the window.
    - `j` : Right pointer of the window.
    - `min` : Monotonic increasing deque to keep track of the minimum value's index.
    - `max` : Monotonic decreasing deque to keep track of the maximum value's index.
    - `beg` and `end` : Mark the start and end index of the longest valid subarray.

2. **Sliding Window Expansion**:
    - For each new element `arr[j]`:
        - Remove elements from the back of `min` while they are greater than `arr[j]`.
        - Remove elements from the back of `max` while they are smaller than `arr[j]`.
        - Add `j` to both deques.

3. **Sliding Window Shrink**:
    - While the difference between the maximum and minimum in the current window is greater than `x`:
        - If the leftmost index in `min` or `max` is equal to `i`, remove it.
        - Move the left pointer `i` to the right.

4. **Update Result**:
    - If the current window `[i..j]` is longer than the previously recorded window `[beg..end]`, update `beg` and `end`.

5. **Construct Answer**:
    - After processing all elements, build the answer subarray using indices `[beg..end]`.
    
---

> Made with ❤️ by Milan Haria
