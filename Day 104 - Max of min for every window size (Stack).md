<h1 align="center">📏 Max of Min for Every Window Size 📏</h1>

---

## 📝 Problem Statement

Given an integer array `arr[]`, your task is to find the **maximum of minimums** for every possible window size in the array, where the window size ranges from `1` to `n` (size of the array).

For each window size `k` (1 <= k <= `arr.size()`):
1. Find all subarrays (windows) of size `k`.
2. For each window, find its minimum.
3. Among these minimums, find the maximum.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr[] = [10, 20, 30, 50, 10, 70, 30]
```

**Output:**  
```
[70, 30, 20, 10, 10, 10, 10]
```

**Explanation:**  
- Window size 1: Min of [10], [20], [30], [50], [10], [70], [30] → max = 70
- Window size 2: Min of [10,20], [20,30], [30,50], [50,10], [10,70], [70,30] → max = 30
- Window size 3: Min of [10,20,30], [20,30,50], [30,50,10], [50,10,70], [10,70,30] → max = 20  
- Window size 4: Min of [10,20,30,50], [20,30,50,10], [30,50,10,70], [50,10,70,30] → max = 10  
- Window size 5: Min of [10,20,30,50,10], [20,30,50,10,70], [30,50,10,70,30] → max = 10  
- Window size 6: Min of [10,20,30,50,10,70], [20,30,50,10,70,30] → max = 10  
- Window size 7: Min of [10,20,30,50,10,70,30] → max = 10 

---

### ✅ Example 2:
**Input:**  
```
arr[] = [10, 20, 30]
```

**Output:**  
```
[30, 20, 10]
```

**Explanation:**  
- Window size 1: Max of mins = 30
- Window size 2: Max of mins = 20
- Window size 3: Max of mins = 10

---

## 🧠 Approach

### Idea:
- For each element, determine **maximum window length** where it is **minimum**.
- Use **Nearest Smaller to Left (NSL)** and **Nearest Smaller to Right (NSR)**.
- `length = NSR - NSL - 1`.

### Steps:
1. Use a **monotonic stack** to find window lengths.
2. For each element, record its contribution:  
   - It is the minimum for window size = `length`.
3. Update answers so that smaller windows inherit larger results:
   - Iterate from back: `ans[i] = max(ans[i], ans[i+1])`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                              |
|------------|-------|------------------------------------------|
| Time       | O(n)  | Each index processed once for NSL/NSR    |
| Space      | O(n)  | Stack + Answer array                     |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`
- `1 ≤ arr[i] ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    public ArrayList<Integer> maxOfMins(int[] arr) {
        int n = arr.length;
        ArrayList<Integer> ans = new ArrayList<>();
        Stack<Integer> stack = new Stack<>();
        int[] lengths = new int[n];
        for(int i = 0; i < n; i++){
            ans.add(0);
        }
        for(int i = 0; i <= n; i++){
            while(!stack.isEmpty() && (i == n || arr[stack.peek()] >= arr[i])){
                int a = stack.pop();
                lengths[a] = stack.isEmpty() ? i : i - stack.peek() - 1;
            }
            if(i < n){
                stack.push(i);
            }
        }
        for(int i = 0; i < n; i++){
            ans.set(lengths[i] - 1, Math.max(ans.get(lengths[i] - 1), arr[i]));
        }
        for(int i = n - 2; i >= 0; i--){
            ans.set(i, Math.max(ans.get(i), ans.get(i + 1)));
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. **The goal**: For each possible window size k (from 1 to n), find the maximum of all minimums of all subarrays of size k.

2. **The idea**:
    - For each element arr[i], find:
        - How big a window can arr[i] be the minimum for?
    - This is done using:
        - NSL (Nearest Smaller to Left)
        - NSR (Nearest Smaller to Right)
    - Example:
    For arr = [10, 20, 30, 50, 10, 70, 30],
   - For 20, NSL is 10 (left side smaller) and NSR is 10 (right side smaller).
   - So, window size = NSR index - NSL index - 1.

3. **How the code does it**:
    - It loops through arr using a monotonic stack to find NSL and NSR in **one pass**.
    - Whenever a smaller element is found (or end is reached), the popped element gets its NSR at current i.
    - The NSL is the stack's peek after popping.

   So, the final window length for arr[i] is:
     length = right - left - 1

4. **Once you know how big a window each element controls**:
    - It means arr[i] is the minimum of all windows of size = length.
    - So, you can record: `ans[length-1] = max(ans[length-1], arr[i])`

5. **Fill the gaps**:
    - Some window sizes may have no direct minimum assigned.
    - To fix this, scan backwards:
    - ans[i] = max(ans[i], ans[i+1])
    - This means: smaller window inherits maximum from larger window.

6. **Result**:
    - The ans list now has, for each window size: the maximum of minimums for that window size.

7. **Return ans**.

---

> Made with ❤️ by Milan Haria
