<h1 align="center">➡️ Next Greater Element ➡️</h1>

---

## 📝 Problem Statement

Given an array `arr[]` of integers, find the **next greater element** for each element in order of their appearance.

- **Next greater element:** Nearest element on the **right** which is **greater** than the current element.
- If there is **no greater element**, return `-1`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr = [1, 3, 2, 4]
```
**Output:**  
```
[3, 4, 4, -1]
```
**Explanation:**  
- Next greater for `1` is `3`
- Next greater for `3` is `4`
- Next greater for `2` is `4`
- `4` has no greater → `-1`

---

### ✅ Example 2:
**Input:**  
```
arr = [6, 8, 0, 1, 3]
```
**Output:**  
```
[8, -1, 1, 3, -1]
```
**Explanation:**  
- Next greater for `6` is `8`
- `8` → no greater → `-1`
- `0` → next greater is `1`
- `1` → next greater is `3`
- `3` → no greater → `-1`

---

### ✅ Example 3:
**Input:**  
```
arr = [10, 20, 30, 50]
```
**Output:**  
```
[20, 30, 50, -1]
```
**Explanation:**  
Sorted ascending → next element is next greater.

---

### ✅ Example 4:
**Input:**  
```
arr = [50, 40, 30, 10]
```
**Output:**  
```
[-1, -1, -1, -1]
```
**Explanation:**  
Sorted descending → no next greater elements.

---

## 🧠 Approach

- Use a **stack** to keep track of elements whose next greater is yet to be found.
- Traverse **from right to left**:
  - Pop elements **smaller or equal** to current.
  - If stack is not empty → its top is the next greater.
  - Push current element onto the stack.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                      |
|------------|-------|----------------------------------|
| Time       | O(n)  | Each element pushed & popped once|
| Space      | O(n)  | Stack + answer array             |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁶`
- `0 ≤ arr[i] ≤ 10⁹`

---

## 💻 Code

```java
class Solution {
    public ArrayList<Integer> nextLargerElement(int[] arr) {
        int n = arr.length;
        ArrayList<Integer> ans = new ArrayList<>();
        for(int i = 0; i < n; i++){
            ans.add(-1);
        }
        Stack<Integer> stack = new Stack<>();
        for(int i = n - 1; i >= 0; i--){
            while(!stack.isEmpty() && arr[i] >= stack.peek()){
                stack.pop();
            }
            if(!stack.isEmpty()){
                ans.set(i, stack.peek());
            }
            stack.push(arr[i]);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
