<h1 align="center">🧩 Longest Valid Parentheses 🧩</h1>

---

## 📝 Problem Statement

Given a string `s` consisting of `'('` and `')'`, find the **length** of the **longest valid parentheses substring**.

A valid parentheses string must:
- Have every opening `'('` matched with a closing `')'`.
- Closing brackets must appear **after** their matching opening bracket.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s = "((()"
```
**Output:**  
```
2
```
**Explanation:**  
- Longest valid: `"()"`  
- Length = 2

---

### ✅ Example 2:
**Input:**  
```
s = ")()())"
```
**Output:**  
```
4
```
**Explanation:**  
- Longest valid: `"()()"`  
- Length = 4

---

### ✅ Example 3:
**Input:**  
```
s = "())()"
```
**Output:**  
```
2
```
**Explanation:**  
- Longest valid: `"()"`  
- Length = 2

---

## 🧠 Approach

### Idea:
- Use a **stack** to track **indices** of unmatched `'('` or invalid `')'`.

### Steps:
1. Push `-1` to stack initially to handle base case.
2. For each character:
   - If `'('` → push its index.
   - If `')'` → pop top of stack.
     - If stack is empty → push current index as a new base.
     - Else → calculate valid length `i - stack.peek()` and update answer.
3. The maximum seen is the result.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description               |
|------------|-------|---------------------------|
| Time       | O(n)  | One pass through string   |
| Space      | O(n)  | Stack for storing indices |

---

## 🎯 Constraints

- `1 ≤ s.length() ≤ 10⁶`
- `s` consists of `'('` and `')'` only.

---

## 💻 Code

```java
class Solution {
    static int maxLength(String s) {
        int n = s.length(), ans = 0;
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        for(int i = 0; i < n; i++){
            if(s.charAt(i) == ')'){
                stack.pop();
                if(stack.isEmpty()){
                    stack.push(i);
                } else{
                    ans = Math.max(ans, i - stack.peek());
                }
            } else{
                stack.push(i);
            }
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
