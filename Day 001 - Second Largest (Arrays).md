<h1 align="center">🚀 <span style="font-size: 2.5rem;">Second Largest</span> 🚀</h1>

---

## 🧩 Problem Statement

Given an array of **positive integers** `arr[]`, return the **second largest** element from the array.  
If the second largest element doesn't exist, return **-1**.

> 📝 **Note:**  
> The second largest element **must not** be equal to the largest element.

---

## 🧪 Examples

### ✅ Example 1:

**Input:**  
```java
arr[] = [12, 35, 1, 10, 34, 1]
```

**Output:**  
```
34
```

**Explanation:**  
- Largest = 35  
- Second Largest = 34  

---

### ✅ Example 2:

**Input:**  
```java
arr[] = [10, 5, 10]
```

**Output:**  
```
5
```

**Explanation:**  
- Largest = 10  
- Second Largest = 5  

---

### ✅ Example 3:

**Input:**  
```java
arr[] = [10, 10, 10]
```

**Output:**  
```
-1
```

**Explanation:**  
All elements are equal — there's no second distinct largest value.

---

## 🧠 Approach

> 💡 **Idea:**  
We traverse the array once, keeping track of:
- `max` → the current largest value
- `smax` → the current second largest (less than `max` but as large as possible)

> ⚙️ **Logic:**
- If the current number is greater than `max`, we update `smax` to `max`, and `max` to the current number.
- If it's not equal to `max` (i.e., to ensure it's distinct) **and** greater than `smax`, we update `smax`.

At the end, if `smax` is still `0`, that means no second largest exists. So we return `-1`.

---

## ⏱️ Time & Space Complexity

| Complexity | Value | Reason |
|------------|-------|--------|
| 🕒 Time     | `O(n)` | We scan the array once |
| 📦 Space    | `O(1)` | Only two variables `max` and `smax` |

---

## 🎯 Constraints

- `2 ≤ arr.length ≤ 10⁵`  
- `1 ≤ arr[i] ≤ 10⁵`

---

## 💻 Code

```java
class Solution {
    public int getSecondLargest(int[] arr) {
        int max = 0, smax = 0;
        for(int i: arr){
            if(max < i){
                smax = max;
                max = i;
            } else if(max != i && smax < i){
                smax = i;
            }
        }
        return smax == 0 ? -1 : smax;
    }
}
```

---

> Made with ❤️ by Milan Haria
