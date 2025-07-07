<h1 align="center">📈 Stock Span Problem 📈</h1>

---

## 📝 Problem Statement

Given an array `arr[]` representing **daily stock prices**, calculate the **stock span** for each day.

**Stock Span:**  
For any day `i`, span is defined as the **maximum number of consecutive days** before day `i` (including day `i` itself) for which the price of stock was **less than or equal to its price on day `i`**.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr[] = [100, 80, 60, 70, 60, 75, 85]
```

**Output:**  
```
[1, 1, 1, 2, 1, 4, 6]
```

**Explanation:**  
- Day 0: price `100` → span `1`
- Day 1: price `80` → span `1`
- Day 2: price `60` → span `1`
- Day 3: price `70` → span `2` (`60` and `70`)
- Day 4: price `60` → span `1`
- Day 5: price `75` → span `4` (`60, 70, 60, 75`)
- Day 6: price `85` → span `6`

---

### ✅ Example 2:
**Input:**  
```
arr[] = [10, 4, 5, 90, 120, 80]
```

**Output:**  
```
[1, 1, 2, 4, 5, 1]
```

**Explanation:**  
- Day 0: `10` → span `1`
- Day 1: `4` → span `1`
- Day 2: `5` → span `2`
- Day 3: `90` → span `4`
- Day 4: `120` → span `5`
- Day 5: `80` → span `1`

---

## 🧠 Approach

### Observation:
To efficiently find the span for each day, use a **stack** to store indices of prices in **decreasing order**.

### Steps:
1. Initialize an empty stack.
2. Loop through each price:
   - Pop elements from stack while `arr[stack.peek()] <= arr[i]`.
   - If stack is empty → span = `i + 1`
   - Else → span = `i - stack.peek()`
   - Push current index `i` onto stack.
3. Add span to answer.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                  |
|------------|-------|------------------------------|
| Time       | O(n)  | Each element is pushed/popped once |
| Space      | O(n)  | Stack storage                |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`
- `1 ≤ arr[i] ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public ArrayList<Integer> calculateSpan(int[] arr) {
        int n = arr.length;
        Stack<Integer> stack = new Stack<>();
        ArrayList<Integer> ans = new ArrayList<>();
        for(int i = 0; i < n; i++){
            int val = arr[i];
            while(!stack.isEmpty() && arr[stack.peek()] <= val){
                stack.pop();
            }
            ans.add(stack.isEmpty() ? i + 1 : i - stack.peek());
            stack.push(i);
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

### For each day i:
  - Pop prices from stack until we find a price greater than current.
  - If stack empty → all previous are smaller → span is i+1.
  - Else → span is distance to previous greater price.
  - Push current index to stack.

---

> Made with ❤️ by Milan Haria
