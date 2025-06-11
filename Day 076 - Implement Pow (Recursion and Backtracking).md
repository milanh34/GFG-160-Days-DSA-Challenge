<h1 align="center">⚡ Implement Pow ⚡</h1>

---

## 📝 Problem Statement

Implement the function `power(b, e)`, which calculates **b raised to the power of e** (i.e. b<sup>e</sup>).  
The function must handle:
- Negative and positive exponents.
- Fractional bases.
- Large exponent values efficiently.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
b = 3.00000, e = 5
```

**Output:**  
```
243.00000
```

**Explanation:**  
3^5 = 3 * 3 * 3 * 3 * 3 = 243

---

### ✅ Example 2:

**Input:**  
```
b = 0.55000, e = 3
```

**Output:**  
```
0.16638
```

**Explanation:**  
0.55^3 = 0.55 * 0.55 * 0.55 = 0.166375 ≈ 0.16638

---

### ✅ Example 3:

**Input:**  
```
b = -0.67000, e = -7
```

**Output:**  
```
-16.49971
```

**Explanation:**  
-0.67^-7 = 1 / (-0.67^7) ≈ -16.49971

---

## 🧠 Approach

- Use **divide and conquer** (Exponentiation by Squaring) to compute power efficiently.
- Handle:
  - **Base case:** `e == 0` → return 1.
  - **Negative exponents:** return `1 / power(b, -e)`.
  - **Even exponent:** recursively compute `b^(e/2)` and square it.
  - **Odd exponent:** compute `b * (b^(e/2))^2`.

This reduces the time complexity from `O(e)` to `O(log e)`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value     | Description                            |
|------------|-----------|----------------------------------------|
| Time       | O(log e)  | Divide-and-conquer recursion           |
| Space      | O(log e)  | Recursive call stack (can be O(1) with iteration) |

---

## 🎯 Constraints

- `-100.0 < b < 100.0`
- `-10^9 <= e <= 10^9`
- Either `b ≠ 0` or `e > 0`
- `-10^4 <= b^e <= 10^4`

---

## 💻 Code

```java
class Solution {
    double power(double b, int e) {
        if(e == 0){
            return 1;
        }
        if(e < 0){
            return 1 / power(b, -e);
        }
        double pow = power(b, e / 2);
        if((e & 1) == 0){
            return pow * pow;
        } else{
            return b * pow * pow;
        }
    }
}
```

---

> Made with ❤️ by Milan Haria
