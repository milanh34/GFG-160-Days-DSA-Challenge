<h1 align="center">🔁 Intersection of Two Arrays with Duplicate Elements 🔁</h1>

---

## 📝 Problem Statement

Given two integer arrays `a[]` and `b[]`, find the **intersection** of these arrays.  
The intersection should:

- Contain only elements that are **common in both arrays**.
- **Avoid duplicates** in the output (i.e., include each common element only once).
- Result can be in any order.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
a = [1, 2, 1, 3, 1]
b = [3, 1, 3, 4, 1]
```
**Output:**
```
[1, 3]
```
**Explanation:**  
The common elements are `1` and `3`, and duplicates are ignored.

---

### ✅ Example 2:
**Input:**
```
a = [1, 1, 1]
b = [1, 1, 1, 1, 1]
```
**Output:**
```
[1]
```
**Explanation:**  
Only `1` is common and appears once in the result.

---

### ✅ Example 3:
**Input:**
```
a = [1, 2, 3]
b = [4, 5, 6]
```
**Output:**
```
[]
```
**Explanation:**  
There are no common elements.

---

## 🧠 Approach

- Use a **HashSet** to store all elements of array `a`.
- Iterate through array `b`, and for each element, check if it's in the set.
- Maintain a **second set** to avoid adding duplicates in the result.
- Add the element to result only if it has not been visited before.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value        | Description                                  |
|------------------|--------------|----------------------------------------------|
| 🕒 Time          | `O(n + m)`   | One pass for each array                      |
| 📦 Space         | `O(n)`       | Sets for storing elements and visited values |

---

## 🎯 Constraints

- `1 ≤ a.length, b.length ≤ 10⁵`
- `1 ≤ a[i], b[i] ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public ArrayList<Integer> intersectionWithDuplicates(int[] a, int[] b) {
        HashSet<Integer> set = new HashSet<>(), visited = new HashSet<>();
        for(int i: a){
            set.add(i);
        }
        ArrayList<Integer> ans = new ArrayList<>();
        for(int i: b){
            if(set.contains(i) && !visited.contains(i)){
                ans.add(i);
                visited.add(i);
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- `set` holds all unique elements from array `a`.
- For each element in `b`, check:
  - Is it in `set`? → it's a common element.
  - Has it been added already (`visited`)? → skip if yes.
- If both conditions are satisfied, add to result and mark as visited.

---

> Made with ❤️ by Milan Haria
