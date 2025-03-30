<h1 align="center">🔁 Reverse an Array 🔁</h1>

---

## 🧩 Problem Statement

You are given an array of integers `arr[]`.  
Your task is to **reverse** the given array **in place**.  
That means no extra array — just flip it inside out, right where it is! 🌀

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```java
arr = [1, 4, 3, 2, 6, 5]
```

**Output:**  
```
[5, 6, 2, 3, 4, 1]
```

**Explanation:**  
- Original array: `1 4 3 2 6 5`  
- After reversing: `5 6 2 3 4 1`  

---

### ✅ Example 2:
**Input:**  
```java
arr = [4, 5, 2]
```

**Output:**  
```
[2, 5, 4]
```

**Explanation:**  
- Start with two pointers: i = 0, j = 2
- Swap arr[0] and arr[2] → [2, 5, 4]
- Now i = 1, j = 1 (both meet at the center), so stop.
- Final result is the reversed array: [2, 5, 4]

---

### ✅ Example 3:
**Input:**  
```java
arr = [1]
```

**Output:**  
```
[1]
```

**Explanation:**  
Single element remains unchanged.

---

## 🧠 Approach

> 💡 **Idea:**  
We simply **swap** elements from both ends moving toward the center.

> ⚙️ **Steps:**
1. Start with two pointers — one at the beginning (`i`), and one at the end (`n - i - 1`).
2. Keep swapping these elements until you reach the middle.
3. Done! 🎉

This is the classic in-place reverse strategy — minimal and elegant!

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Reason |
|------------|-------|--------|
| 🕒 Time     | `O(n/2)` → `O(n)` | Half swaps, but still linear in nature |
| 📦 Space    | `O(1)` | In-place, no extra memory used |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`  
- `0 ≤ arr[i] ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public void reverseArray(int arr[]) {
        int n = arr.length;
        for(int i = 0; i < n / 2; i++){
            int temp = arr[n - i - 1];
            arr[n - i - 1] = arr[i];
            arr[i] = temp;
        }
    }
}
```

---

> Made with ❤️ by Milan Haria
