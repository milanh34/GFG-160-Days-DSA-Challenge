<h1 align="center">🔀 Merge Without Extra Space 🔀</h1>

---

## 📝 Problem Statement

You are given two **sorted arrays** `a[]` and `b[]` of sizes `n` and `m`, respectively. Your task is to **merge them in-place** (without using extra space) so that:

- `a[]` contains the **first n** elements of the final sorted sequence
- `b[]` contains the **last m** elements of the final sorted sequence

Both arrays should remain sorted after modification.

---

## ✅ Examples

### Example 1
**Input:**  
```
a = [2, 4, 7, 10]
b = [2, 3]
```

**Output:**  
```
a = [2, 2, 3, 4]
b = [7, 10]
```

**Explanation:**  
Merged and sorted: `[2, 2, 3, 4, 7, 10]`. First 4 go to `a`, rest go to `b`.

---

### Example 2
**Input:**  
```
a = [1, 5, 9, 10, 15, 20]
b = [2, 3, 8, 13]
```

**Output:**  
```
a = [1, 2, 3, 5, 8, 9]
b = [10, 13, 15, 20]
```

**Explanation:**  
Merged: `[1, 2, 3, 5, 8, 9, 10, 13, 15, 20]`. First 6 in `a`, next 4 in `b`.

---

### Example 3
**Input:**  
```
a = [0, 1]
b = [2, 3]
```

**Output:**  
```
a = [0, 1]
b = [2, 3]
```

**Explanation:**  
Already in proper order.

---

## 🧠 Approach

1. Start with pointers at the **end** of `a[]` and the **start** of `b[]`.
2. Swap elements if `a[i] > b[j]` — the larger one moves to `b`, and the smaller one to `a`.
3. After the loop, sort both arrays individually to finalize the result.

> 💡 This works because we push larger values to `b[]` and smaller ones to `a[]`, ensuring final separation of small and large values between the arrays.

---

## ⏱️ Time & Space Complexity

| Type       | Complexity   | Explanation                              |
|------------|--------------|------------------------------------------|
| 🕒 Time     | O((n + m) log(n + m)) | Due to sorting both arrays at the end   |
| 📦 Space    | O(1)         | Done in-place without any extra space    |

---

## 🎯 Constraints

- `1 ≤ a.length, b.length ≤ 10⁵`
- `0 ≤ a[i], b[i] ≤ 10⁷`

---

## 💻 Code

```java
class Solution {
    public void mergeArrays(int a[], int b[]) {
        int n1 = a.length, n2 = b.length;
        int i = n1 - 1, j = 0;
        while(i >= 0 && j < n2){
            if(a[i] > b[j]){
                int t = a[i];
                a[i] = b[j];
                b[j] = t;
                i--;
                j++;
            } else{
                break;
            }
        }
        Arrays.sort(a);
        Arrays.sort(b);
    }
}

```

---

> Made with ❤️ by Milan Haria
