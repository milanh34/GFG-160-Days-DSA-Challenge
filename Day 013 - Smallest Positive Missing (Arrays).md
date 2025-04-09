<h1 align="center">➕ Smallest Positive Missing ➕</h1>

---

## 🧩 Problem Statement

You are given an integer array `arr[]`. Your task is to find the **smallest positive number** that is **missing** from the array.

> Note: Positive numbers start from **1**. The array may contain **negative numbers**, **zeros**, and **duplicates**.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
arr = [2, -3, 4, 1, 1, 7]
```

**Output:**  
```
3
```

**Explanation:**  
The smallest missing positive number is `3`.

---

### ✅ Example 2:
**Input:**  
```
arr = [5, 3, 2, 5, 1]
```

**Output:**  
```
4
```

**Explanation:**  
The sequence 1, 2, 3, 5 is present. The smallest missing number is `4`.

---

### ✅ Example 3:
**Input:**  
```
arr = [-8, 0, -1, -4, -3]
```

**Output:**  
```
1
```

**Explanation:**  
All numbers are non-positive. So the smallest missing positive number is `1`.

---

## 🧠 Approach

### 🔍 Brute Force using HashSet

1. Insert all elements into a HashSet.
2. Start from 1 and keep checking if the number is in the set.
3. The first number not present in the set is the answer.

This method ensures that even with negative numbers and duplicates, the correct smallest positive missing number is found.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                            |
|------------------|-----------|----------------------------------------|
| 🕒 Time           | `O(n)`    | Insert + lookup through range          |
| 📦 Space          | `O(n)`    | Set to hold all unique values          |

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 10⁵`
- `-10⁶ ≤ arr[i] ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    public int missingNumber(int[] arr) {
        Set<Integer> set = new HashSet<>();
        for(int i: arr){
            set.add(i);
        }
        for(int i = 1; i < 1000001; i++){
            if(!set.contains(i)){
                return i;
            }
        }
        return 1000001; 
    }
}
```

---


> Made with ❤️ by Milan Haria
