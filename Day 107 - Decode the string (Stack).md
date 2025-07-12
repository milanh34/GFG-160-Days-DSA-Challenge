<h1 align="center">🔓 Decode the String 🔓</h1>

---

## 📝 Problem Statement

Given an **encoded string** `s`, decode it.

**Encoding Rule:**  
A substring is encoded as `k[encodedString]` — where the substring inside `[]` is repeated exactly `k` times.

- `k` is always a positive integer.
- `encodedString` contains only **lowercase English letters**.
- The length of the **decoded string** will never exceed `10⁵`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
s = "1[b]"
```

**Output:**  
```
"b"
```

**Explanation:**  
- `"b"` is repeated once → `"b"`.

---

### ✅ Example 2:
**Input:**  
```
s = "3[b2[ca]]"
```

**Output:**  
```
"bcacabcacabcaca"
```

**Explanation:**  
1. `2[ca]` → `"caca"`  
2. `3[bcaca]` → `"bcacabcacabcaca"`

---

## 🧠 Approach

### Idea:
- Use a **stack** to process characters.
- When `]` is found, pop and decode the innermost `[...]` block.
- Extract the **substring** and its **repeat count**.
- Push the expanded string back to the stack.

### Steps:
1. Iterate each character:
   - If not `]` → push to stack.
   - If `]` → pop until `[` to get substring.
   - Then, pop digits to get repeat count.
   - Expand substring and push characters back.
2. Build result by popping from stack.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description |
|------------|-------|--------------|
| Time       | O(n)  | Each char processed once |
| Space      | O(n)  | Stack for chars |

---

## 🎯 Constraints

- `1 ≤ |s| ≤ 10⁵`
- `1 ≤ k ≤ 100`

---

## 💻 Code

```java
class Solution {
    static String decodeString(String s) {
        Stack<Character> stack = new Stack<>();
        for(char c: s.toCharArray()){
            if(c != ']'){
                stack.push(c);
            } else{
                StringBuilder sb = new StringBuilder();
                while(!stack.isEmpty() && stack.peek() != '['){
                    sb.append(stack.pop());
                }
                sb.reverse();
                stack.pop();
                StringBuilder temp = new StringBuilder();
                while(!stack.isEmpty() && Character.isDigit(stack.peek())){
                    temp.append(stack.pop());
                }
                int num = Integer.parseInt(temp.reverse().toString());
                String str = sb.toString();
                for(int i = 1; i < num; i++){
                    sb.append(str);
                }
                for(char ch: sb.toString().toCharArray()){
                    stack.push(ch);
                }
            }
        }
        StringBuilder ans = new StringBuilder();
        while(!stack.isEmpty()){
            ans.append(stack.pop());
        }
        return ans.reverse().toString();
    }
}
```

---

> Made with ❤️ by Milan Haria
