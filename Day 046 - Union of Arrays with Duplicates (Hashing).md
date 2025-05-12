<h1 align="center">🔗 Union of Arrays with Duplicates 🔗</h1>

---

## 📝 Problem Statement

Given two arrays `a[]` and `b[]`, find the **number of elements in their union**.

- The union contains all **distinct elements** from both arrays.
- If there are duplicate elements in the same array or across arrays, only one occurrence is considered.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
a = [1, 2, 3, 4, 5]
b = [1, 2, 3]
```
**Output:**
```
5
```
**Explanation:**  
Union is `{1, 2, 3, 4, 5}`.

---

### ✅ Example 2:
**Input:**
```
a = [85, 25, 1, 32, 54, 6]
b = [85, 2]
```
**Output:**
```
7
```
**Explanation:**  
Union is `{85, 25, 1, 32, 54, 6, 2}`.

---

### ✅ Example 3:
**Input:**
```
a = [1, 2, 1, 1, 2]
b = [2, 2, 1, 2, 1]
```
**Output:**
```
2
```
**Explanation:**  
Union is `{1, 2}`.

---

## 🧠 Approach

- Use a **HashSet** to store distinct elements from both arrays.
- Iterate both arrays and add all elements into the set.
- Since set automatically ignores duplicates, the size of the set will give the required result.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value        | Description                          |
|------------------|--------------|--------------------------------------|
| 🕒 Time          | `O(n + m)`   | One pass for each array              |
| 📦 Space         | `O(n + m)`   | Set for storing all unique elements  |

---

## 🎯 Constraints

- `1 ≤ a.length, b.length ≤ 10⁶`
- `0 ≤ a[i], b[i] ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public static int findUnion(int a[], int b[]) {
        HashSet<Integer> set = new HashSet<>();
        for(int i: a){
            set.add(i);
        }
        for(int i: b){
            set.add(i);
        }
        return set.size();
    }
}
```

---

## 📝 Explanation of Code

- The `HashSet` automatically ensures that only unique elements are stored.
- After adding all elements from both arrays, the size of the set will be the count of the union.

---

> Made with ❤️ by Milan Haria
