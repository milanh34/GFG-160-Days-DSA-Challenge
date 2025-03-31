<h1 align="center">🔄 Rotate Array 🔄</h1>

---

## 🧩 Problem Statement

Given an array `arr[]`, rotate it to the **left (counter-clockwise)** by `d` steps.  
You must perform the operation **in-place** — no allocating new arrays (as much as possible)!

> 🌀 Consider the array as **circular** — once you reach the end, you loop back to the beginning.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```java
arr[] = [1, 2, 3, 4, 5], d = 2
```

**Output:**  
```
[3, 4, 5, 1, 2]
```

**Explanation:**  
- After 1st rotation: [2, 3, 4, 5, 1]  
- After 2nd rotation: [3, 4, 5, 1, 2]

---

### ✅ Example 2:
**Input:**  
```java
arr[] = [2, 4, 6, 8, 10, 12, 14, 16, 18, 20], d = 3
```

**Output:**  
```
[8, 10, 12, 14, 16, 18, 20, 2, 4, 6]
```

**Explanation:**  
When rotated by 3 elements, it becomes 8, 10, 12, 14, 16, 18, 20, 2, 4, 6.

---

### ✅ Example 3:
**Input:**  
```java
arr[] = [7, 3, 9, 1], d = 9
```

**Output:**  
```
[3, 9, 1, 7]
```

**Explanation:**  
Rotation count exceeds array size — but since it's circular, we take `d % n = 9 % 4 = 1` rotation.

---

## 🧠 Approach

> 💡 **Idea:**  
Instead of moving elements one-by-one, we can directly **map each element** to its **new position** using a temporary copy and modular arithmetic.

> ⚙️ **Steps:**
1. Clone the original array for reference.
2. For each index `i`, place the element from `copy[(i + d) % n]` into `arr[i]`.
3. This gives the left-rotated result in one pass.

🌀 This logic ensures that even if `d > n`, it still works seamlessly!

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Reason |
|------------|-------|--------|
| 🕒 Time     | `O(n)` | Every element is accessed once |
| 📦 Space    | `O(n)` | Due to the use of a cloned copy of the array |

📌 **Note:** If strict in-place is required (no extra space), this solution could be optimized using the **reverse approach**, which uses `O(1)` space.

---

## 🎯 Constraints

- `1 ≤ arr.length, d ≤ 10⁵`  
- `0 ≤ arr[i] ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    static void rotateArr(int arr[], int d) {
        int[] copy = arr.clone();
        int n = arr.length;
        for(int i = 0; i < n; i++){
            arr[i] = copy[(i + d) % n];
        }
    }
}
```

---

> Made with ❤️ by Milan Haria
