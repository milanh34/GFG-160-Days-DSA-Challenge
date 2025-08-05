<h1 align="center">🧮 Boolean Parenthesization 🧮</h1>

---

## 📝 Problem Statement

You're given a boolean expression `s` containing the characters:
- `'T'` → represents `true`
- `'F'` → represents `false`

And operators:
- `'&'` → boolean AND
- `'|'` → boolean OR
- `'^'` → boolean XOR

Your task is to **count the number of ways to parenthesize** the expression such that the **evaluated result is `true`**.

> The answer is guaranteed to fit in a 32-bit integer.

---

## ✅ Examples

### ✅ Example 1:

**Input:**   
```
s = "T|T&F^T"
```

**Output:**  
```
4
```

**Explanation:**
There are 4 ways to parenthesize such that the expression evaluates to true:  
- ((T|T)&(F^T))  
- (T|(T&(F^T)))  
- (((T|T)&F)^T)  
- (T|((T&F)^T))

---

### ✅ Example 2:

**Input:**  
```
s = "T^F|F"
```

**Output:**  
```
2
```

The 2 valid ways are:  
- ((T^F)|F)  
- (T^(F|F))

---

## 🧠 Approach

We use **Dynamic Programming** with two DP tables:

- `True[i][j]` → Number of ways the subexpression `s[i...j]` evaluates to `true`
- `False[i][j]` → Number of ways the subexpression `s[i...j]` evaluates to `false`

**Steps:**

1. Initialize `True[i][i] = 1` if `s[i] == 'T'` and `False[i][i] = 1` if `s[i] == 'F'`  
2. Iterate over increasing subexpression lengths
3. For each partition, recursively calculate left and right `True/False` combinations based on the operator (`&`, `|`, `^`)
4. Sum up the valid ways depending on the operator and store in the tables.

---

## ⏱️ Time and Space Complexity

| Complexity | Value        | Description                            |
|------------|--------------|----------------------------------------|
| Time       | O(N³)        | Three nested loops                     |
| Space      | O(N²)        | Two 2D DP tables for true/false counts |

---

## 🎯 Constraints

- 1 ≤ `s.length()` ≤ 100  
- Expression contains only `'T'`, `'F'`, `'&'`, `'|'`, `'^'`

---

## 💻 Code

```java
class Solution {
    static int countWays(String s) {
        int n = s.length();
        int[][] True = new int[n][n], False = new int[n][n];
        for(int i = 0; i < n; i += 2){
            if(s.charAt(i) == 'T'){
                True[i][i] = 1;
            } else if(s.charAt(i) == 'F'){
                False[i][i] = 1;
            }
        }
        for(int i = 2; i < n; i += 2){
            for(int j = 0; j < n - i; j += 2){
                for(int k = j + i, l = j + 1; l < k; l += 2){
                    int leftT = True[j][l - 1], leftF = False[j][l - 1];
                    int rightT = True[l + 1][k], rightF = False[l + 1][k];
                    if(s.charAt(l) == '&'){
                        True[j][k] += leftT * rightT;
                        False[j][k] += leftT * rightF + leftF * rightT + leftF * rightF;
                    } else if(s.charAt(l) == '|'){
                        True[j][k] += leftT * rightT + leftT * rightF + leftF * rightT;
                        False[j][k] += leftF * rightF;
                    } else{
                        True[j][k] += leftT * rightF + leftF * rightT;
                        False[j][k] += leftT * rightT + leftF * rightF;
                    }
                }
            }
        }
        return True[0][n - 1];
    }
}
```

---

## 📝 Explanation of Code

- **Base Case**: Initialize `True[i][i] = 1` if `s[i] == 'T'`, otherwise `False[i][i] = 1`. These are the individual operands.
- **DP Filling**: For every possible substring length (even only), try every possible operator position `k`:
    - Calculate number of ways to form `true or false` using combinations of left and right subexpressions.
    - Use boolean logic for each operator:
        - `&`: true only when both are true
        - `|`: true when any one is true
        - `^`: true when one is true and one is false
- **Return**: The value at `True[0][n-1]` gives total ways to evaluate entire expression as true.

---

> Made with ❤️ by Milan Haria
