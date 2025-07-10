<h1 align="center">🗂️ Get Min from Stack 🗂️</h1>

---

## 📝 Problem Statement

Given `q` queries, implement a stack supporting **4 operations**:
- `push(x)`: Insert `x` onto the stack.
- `pop()`: Remove the top element.
- `peek()`: Return the top element. If empty, return `-1`.
- `getMin()`: Retrieve the minimum element in **O(1)** time. If empty, return `-1`.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
q = 7  
queries = [[1, 2], [1, 3], [3], [2], [4], [1, 1], [4]]
```

**Output:**  
```
[3, 2, 1]
```

**Explanation:**  
- `push(2)` → Stack: `[2]`
- `push(3)` → Stack: `[2, 3]`
- `peek()` → Top = `3`
- `pop()` → Stack: `[2]`
- `getMin()` → Min = `2`
- `push(1)` → Stack: `[2, 1]`
- `getMin()` → Min = `1`

---

### ✅ Example 2

**Input:**  
```
q = 4  
queries = [[1, 4], [1, 2], [4], [3]]
```

**Output:**  
```
[2, 2]
```

**Explanation:**  
- `push(4)` → Stack:  `[4]`
- `push(2)` → Stack:  `[4, 2]`
- `getMin()` → Min: `2`
- `peek()` → Top: `2`

---

### ✅ Example 3

**Input:**  
```
q = 5  
queries = [[1, 10], [4], [1, 5], [4], [2]]
```

**Output:**  
```
[10, 5]
```

**Explanation:**  
- `push(10)` → Stack:  `[10]`
- `getMin()` → Min: `10`
- `push(5)` → Stack:  `[10, 5]`
- `getMin()` → Min: `5`
- `pop()` → Stack: `[10]`

---

## 🧠 Approach

- Use **one stack** to maintain stack operations (`push`, `pop`, `peek`).
- Use a **min-heap (PriorityQueue)** to efficiently track the **current minimum element**.
- On `push`: Add to both `stack` and `PriorityQueue`.
- On `pop`: Remove from both `stack` and `PriorityQueue`.
- On `peek`: Return top of `stack`.
- On `getMin`: Return `peek` of `PriorityQueue`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                                 |
|------------|-------|---------------------------------------------|
| Time       | O(log n) | For `push` and `pop` due to `PriorityQueue` |
| Space      | O(n)  | Additional min-heap for minimum tracking    |

---

## 🎯 Constraints

- `1 ≤ q ≤ 10⁵`
- `0 ≤ x ≤ 10⁹`

---

## 💻 Code

```java
class Solution {
    public Solution() {}
    
    Stack<Integer> stack = new Stack<>();
    PriorityQueue<Integer> queue = new PriorityQueue<>();

    // Add an element to the top of Stack
    public void push(int x) {
        stack.push(x);
        queue.offer(x);
    }

    // Remove the top element from the Stack
    public void pop() {
        if(!stack.isEmpty()){
            int a = stack.pop();
            queue.remove(a);
        }
    }

    // Returns top element of the Stack
    public int peek() {
        if(!stack.isEmpty()){
            return stack.peek();
        }
        return -1;
    }
    
    // Finds minimum element of Stack
    public int getMin() {
        if(!stack.isEmpty()){
            return queue.peek();
        }
        return -1;
    }
}
```

---

> Made with ❤️ by Milan Haria