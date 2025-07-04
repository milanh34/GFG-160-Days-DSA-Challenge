<h1 align="center">✅ Parenthesis Checker ✅</h1>

---

## 📝 Problem Statement

Given a string `s` containing **'('**, **')'**, **'{'**, **'}'**, **'['**, **']'**, check if the **brackets are well-formed** and **balanced**.

A valid string must satisfy:
1. **Open brackets** must be closed by the **same type of brackets**.
2. Open brackets must be closed in the **correct order**.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s = "[{()}]"
```

**Output:**  
```
true
```

**Explanation:**  
All brackets are properly nested and closed.

---

### ✅ Example 2:
**Input:**  
```
s = "[()()]{}"
```

**Output:**  
```
true
```

**Explanation:**  
Multiple valid bracket pairs.

---

### ✅ Example 3:
**Input:**  
```
s = "([]"
```

**Output:**  
```
false
```

**Explanation:**  
Unclosed '(' → missing ')'.

---

### ✅ Example 4:
**Input:**  
```
s = "([{]})"
```

**Output:**  
```
false
```

**Explanation:**  
Wrong order → '[' closed before '{'.

---

## 🧠 Approach

- Use a **stack**.
- Push open brackets **(, {, [**.
- For closing brackets:
  - Check if the stack top matches the correct opening bracket.
  - If yes, pop it.
  - If not, return false.
- After processing, stack must be empty for a valid expression.

---

## ⏱️ Time and Space Complexity

| Complexity | Value      | Description                       |
|------------|------------|-----------------------------------|
| Time       | O(n)       | Each char processed once          |
| Space      | O(n)       | Stack stores unmatched brackets   |

---

## 🎯 Constraints

- `1 ≤ s.size() ≤ 10⁶`
- `s[i] ∈ {'{', '}', '(', ')', '[', ']'}`

---

## 💻 Code

```java
class Solution {
    static boolean isBalanced(String s) {
        Stack<Character> stack = new Stack<>();
        for(char c: s.toCharArray()){
            switch(c){
                case ')':
                    if(!stack.isEmpty() && stack.peek() == '('){
                        stack.pop();
                    } else{
                        return false;
                    }
                    break;
                case ']':
                    if(!stack.isEmpty() && stack.peek() == '['){
                        stack.pop();
                    } else{
                        return false;
                    }
                    break;
                case '}':
                    if(!stack.isEmpty() && stack.peek() == '{'){
                        stack.pop();
                    } else{
                        return false;
                    }
                    break;
                default:
                    stack.push(c);
                    break;
            }
        }
        return stack.isEmpty();
    }
}
```

---

> Made with ❤️ by Milan Haria
