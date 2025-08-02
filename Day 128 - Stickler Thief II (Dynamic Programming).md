<h1 align="center">🏠 Stickler Thief II 🏠</h1>

---

## 📝 Problem Statement

You are given an array `arr[]` which represents houses arranged in a **circle**, where each house has a certain value.  
A thief aims to **maximize the total stolen value** without robbing two **adjacent** houses.  
Since the houses are in a circle, the **first and last houses are also adjacent**.

Your task is to determine the **maximum amount** the thief can steal.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [2, 3, 2]
```

**Output:**  
```
3
```

**Explanation:**  
- House 0 and 2 are adjacent (circular).  
- Only option is to rob house 1 → total = 3.

---

### ✅ Example 2:

**Input:**  
```
arr = [1, 2, 3, 1]
```

**Output:**  
```
4
```

**Explanation:**  
- Option 1: Rob house 0 and 2 → 1 + 3 = 4  
- Option 2: Rob house 1 and 3 → 2 + 1 = 3  
- Maximum = 4

---

### ✅ Example 3:

**Input:**  
```
arr = [2, 2, 3, 1, 2]
```

**Output:**  
```
5
```

**Explanation:**  
- Option 1: Rob house 0 and 2 → 2 + 3 = 5  
- Option 2: Rob house 2 and 4 → 3 + 2 = 5  
- Maximum = 5

---

## 🧠 Approach

Since the array is circular, house 0 and house n−1 are adjacent.  
So, the thief cannot rob both first and last house in the same run.  
We break it into two separate linear problems:

1. Rob houses from index **0 to n−2** (excluding last)
2. Rob houses from index **1 to n−1** (excluding first)

Then take the **maximum** of both results.

Each subproblem is solved using dynamic programming:
- Maintain two variables:
  - `prev1`: max loot till previous house
  - `prev2`: max loot till house before previous
- At each index `i`, compute:
  ```
  curr = max(prev1, prev2 + arr[i])
  ```

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                        |
|------------|-------|------------------------------------|
| Time       | O(N)  | Traverse the array twice           |
| Space      | O(1)  | Constant space used                |

---

## 🎯 Constraints

- 2 ≤ `arr.length` ≤ 10⁵  
- 0 ≤ `arr[i]` ≤ 10⁴

---

## 💻 Code

```java
class Solution {
    int rob(int[] arr, int beg, int end){
        int prev1 = 0, prev2 = 0;
        for(int i = beg; i <= end; i++){
            int max = Math.max(prev1, prev2 + arr[i]);
            prev2 = prev1;
            prev1 = max;
        }
        return prev1;
    }
    int maxValue(int[] arr) {
        int n = arr.length;
        return Math.max(rob(arr, 0, n - 2), rob(arr, 1, n - 1));
    }
}
```

---

## 📝 Explanation of Code

- `rob()` handles the linear House Robber problem using two variables:
  - `prev1` keeps track of the max stolen value till the previous house.
  - `prev2` keeps track of the value till the house before that.
- For each house from `beg` to `end`, it calculates the optimal max by deciding whether to rob the current house or skip it.
- `maxValue()` solves the circular problem by calling `rob()` twice:
  1. Excluding the **last** house (range `0 to n−2`)
  2. Excluding the **first** house (range `1 to n−1`)
- It returns the **maximum** of both calls.

---

> Made with ❤️ by Milan Haria
