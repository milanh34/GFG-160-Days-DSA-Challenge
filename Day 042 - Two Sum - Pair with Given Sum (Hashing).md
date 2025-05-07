<h1 align="center">➕ Two Sum - Pair with Given Sum ➕</h1>

---

## 📝 Problem Statement

You are given an array `arr[]` of **positive integers** and a target integer `target`.  
Determine if there exist **two distinct indices** such that the **sum of their elements is equal to the target**.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr = [1, 4, 45, 6, 10, 8], target = 16
```
**Output:**  
```
true
```
**Explanation:**  
The pair `6 + 10 = 16` exists at indices 3 and 4.

---

### ✅ Example 2:
**Input:**  
```
arr = [1, 2, 4, 3, 6], target = 11
```
**Output:**  
```
false
```
**Explanation:**  
No two numbers sum up to 11.

---

### ✅ Example 3:
**Input:**  
```
arr = [11], target = 11
```
**Output:**  
```
false
```
**Explanation:**  
Only one number exists. A pair is not possible.

---

## 🧠 Approach

- Use a **HashSet** to store the numbers we’ve seen so far.
- For each number `i` in the array, check whether `(target - i)` exists in the set.
- If it does, we found a valid pair.
- If not, add the current number to the set and move on.

This approach ensures we only traverse the array once and check for complements in constant time.

---

## ⏱️ Time & Space Complexity

| Type       | Complexity | Description                                                                      |
|------------|------------|----------------------------------------------------------------------------------|
| Time       | O(n)       | Single pass through the array where n is the number of elements.                |
| Space      | O(n)       | At most, all elements are stored in the HashSet in the worst case.              |

---

## 🔒 Constraints

- 1 ≤ `arr.length` ≤ 10⁵  
- 1 ≤ `arr[i]` ≤ 10⁵  
- 1 ≤ `target` ≤ 2 × 10⁵  

---

## 💻 Code

```java
class Solution {
    boolean twoSum(int arr[], int target) {
        Set<Integer> set = new HashSet<>();
        for(int i : arr) {
            if(set.contains(target - i)) {
                return true;
            }
            set.add(i);
        }
        return false;
    }
}
```

---

## 📘 Explanation of Code

- We initialize an empty set to keep track of previously seen elements.
- For each element in the array:
  - We check if the **complement** (`target - current element`) exists in the set.
  - If it does, return `true` because we found a pair.
  - If not, we add the current element to the set.
- After checking all elements, if no such pair is found, return `false`.

---

> Made with ❤️ by Milan Haria
