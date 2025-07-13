<h1 align="center">📈 K Sized Subarray Maximum 📈</h1>

---

## 📝 Problem Statement

Given an array `arr[]` of integers and an integer `k`, find the **maximum value** for each **contiguous subarray of size k**.

Return an array where each element is the **maximum of a subarray**.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
arr = [1, 2, 3, 1, 4, 5, 2, 3, 6], k = 3
```

**Output:**  
```
[3, 3, 4, 5, 5, 5, 6]
```

**Explanation:**  
- Subarrays and max values:
  - `[1, 2, 3]` → 3  
  - `[2, 3, 1]` → 3  
  - `[3, 1, 4]` → 4  
  - `[1, 4, 5]` → 5  
  - `[4, 5, 2]` → 5  
  - `[5, 2, 3]` → 5  
  - `[2, 3, 6]` → 6

---

### ✅ Example 2

**Input:**  
```
arr = [8, 5, 10, 7, 9, 4, 15, 12, 90, 13], k = 4
```

**Output:**  
```
[10, 10, 10, 15, 15, 90, 90]
```

**Explanation:**  
- `[8, 5, 10, 7]` → 10  
- `[5, 10, 7, 9]` → 10  
- `[10, 7, 9, 4]` → 10  
- `[7, 9, 4, 15]` → 15  
- `[9, 4, 15, 12]` → 15  
- `[4, 15, 12, 90]` → 90  
- `[15, 12, 90, 13]` → 90

---

### ✅ Example 3

**Input:**  
```
arr = [5, 1, 3, 4, 2, 6], k = 1
```

**Output:**  
```
[5, 1, 3, 4, 2, 6]
```

**Explanation:**  
Each element is its own subarray when `k = 1`.

---

## 🧠 Approach

### Key Idea:
- Use a **deque** to store **indexes** of useful elements for each window.
- The deque always stores indexes in **decreasing order of their values**.
- For each new element:
  - Remove smaller elements from the back.
  - Remove elements out of the window from the front.
  - The front of the deque holds the **maximum** for the window.

---

## ⏱️ Time and Space Complexity

| Complexity | Value  | Description                           |
|------------|--------|---------------------------------------|
| Time       | O(n)   | Each element is added and removed once |
| Space      | O(k)   | Deque stores at most k elements        |

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10⁶`
- `1 ≤ k ≤ arr.size()`
- `0 ≤ arr[i] ≤ 10⁹`

---

## 💻 Code

```java
class Solution {
    static ArrayList<Integer> maxOfSubarrays(int[] arr, int k) {
        ArrayList<Integer> ans = new ArrayList<>();
        Deque<Integer> deque = new ArrayDeque<>();
        int n = arr.length;
        for(int i = 0; i < k; i++){
            while(!deque.isEmpty() && arr[deque.peekLast()] <= arr[i]){
                deque.pollLast();
            }
            deque.addLast(i);
        }
        for(int i = k; i < n; i++){
            ans.add(arr[deque.peekFirst()]);
            while(!deque.isEmpty() && i - k >= deque.peekFirst()){
                deque.pollFirst();
            }
            while(!deque.isEmpty() && arr[deque.peekLast()] <= arr[i]){
                deque.pollLast();
            }
            deque.addLast(i);
        }
        ans.add(arr[deque.peekFirst()]);
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- Initialize a deque to hold indexes.
- Process the first k elements to build the first window.
- For remaining elements:
   - Add the max of the last window.
   - Remove elements out of the window.
   - Remove smaller elements from the back.
   - Add current index.
- Add max of last window.
- Return the result.

---

> Made with ❤️ by Milan Haria
