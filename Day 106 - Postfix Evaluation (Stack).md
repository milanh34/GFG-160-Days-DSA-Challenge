<h1 align="center">📌 Postfix Evaluation 📌</h1>

---

## 📝 Problem Statement

Given an array of string `arr[]` representing an arithmetic expression in **Reverse Polish Notation (Postfix Notation)**, evaluate the expression and return the resulting integer.

✅ Valid operators: `+`, `-`, `*`, `/`  
✅ Operands are valid integers  
✅ Division result is always rounded towards zero

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
arr = ["2", "3", "1", "*", "+", "9", "-"]
```

**Output:**  
```
-4
```

**Explanation:**  
Equivalent Infix: `2 + (3 * 1) - 9`  
Calculation: `2 + 3 = 5`, `5 - 9 = -4`

---

### ✅ Example 2

**Input:**  
```
arr = ["100", "200", "+", "2", "/", "5", "*", "7", "+"]
```

**Output:**  
```
757
```

**Explanation:**  
Equivalent Infix: `((100 + 200) / 2) * 5 + 7`  
Calculation: `300 / 2 = 150`, `150 * 5 = 750`, `750 + 7 = 757`

---

## 🧠 Approach

- Use a **stack** to evaluate the expression left to right.
- For each element:
  - If it’s a number → **push** it to the stack.
  - If it’s an operator → **pop** two elements, apply the operator, push the result.
- Return the remaining value on the stack.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description |
|------------|-------|--------------|
| Time       | O(n)  | We scan each token once; each stack operation is O(1) |
| Space      | O(n)  | In worst case all tokens are numbers → stored in the stack |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`
- Each element is an integer or `+`, `-`, `*`, `/`
- No division by zero

---

## 💻 Code

```java
class Solution {
    public int evaluate(String[] arr) {
        Stack<Integer> stack = new Stack<>();
        for(String i: arr){
            if(i.length() == 1 && i.charAt(0) <= '/'){
                int a = stack.pop();
                int b = stack.pop();
                switch(i.charAt(0)){
                    case '+':
                        stack.push(a + b);
                        break;
                    case '-':
                        stack.push(b - a);
                        break;
                    case '*':
                        stack.push(a * b);
                        break;
                    default:
                        stack.push(b / a);
                        break;
                }
            } else{
                stack.push(Integer.parseInt(i));
            }
        }
        return stack.pop();
    }
}
```

---

> Made with ❤️ by Milan Haria
