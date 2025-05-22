<h1 align="center">🔢 Count Distinct Elements in Every Window 🔢</h1>

---

## 📝 Problem Statement

Given an integer array `arr[]` and a number `k`, find the **number of distinct elements** in **every window of size k** in the array.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
arr = [1, 2, 1, 3, 4, 2, 3], k = 4
```

**Output:**  
```
[3, 4, 4, 3]
```

**Explanation:**  
- Window 1: [1, 2, 1, 3] → 3 distinct elements (1, 2, 3)  
- Window 2: [2, 1, 3, 4] → 4 distinct elements (1, 2, 3, 4)  
- Window 3: [1, 3, 4, 2] → 4 distinct elements (1, 2, 3, 4)  
- Window 4: [3, 4, 2, 3] → 3 distinct elements (2, 3, 4)  

---

### ✅ Example 2:

**Input:**  
```
arr = [4, 1, 1], k = 2
```

**Output:**  
```
[2, 1]
```

**Explanation:**  
- Window 1: [4, 1] → 2 distinct elements (4, 1)  
- Window 2: [1, 1] → 1 distinct element (1)  

---

### ✅ Example 3:

**Input:**  
```
arr = [1, 1, 1, 1, 1], k = 3
```

**Output:**  
```
[1, 1, 1]
```

**Explanation:**  
- Window 1: [1, 1, 1] → 1 distinct element (1)  
- Window 2: [1, 1, 1] → 1 distinct element (1)  
- Window 3: [1, 1, 1] → 1 distinct element (1)  

---

## 🧠 Approach

- Use a **frequency array** or HashMap to track the number of times each element appears in the current window.
- Start by processing the first `k` elements and count the unique ones.
- Slide the window one step at a time:
  - Decrease frequency of the element going out of the window.
  - Increase frequency of the element coming into the window.
  - Adjust the count of distinct elements accordingly.

---

## ⏱️ Time & Space Complexity

| Complexity       | Description                                                                 | Value     |
|------------------|-----------------------------------------------------------------------------|-----------|
| 🕒 Time          | Traverse each element once and update frequency array                       | O(N)      |
| 📦 Space         | Frequency array of size 100001 (as arr[i] ≤ 10⁵)                            | O(1)      |

---

## 🎯 Constraints

- 1 ≤ k ≤ arr.length ≤ 10⁵  
- 1 ≤ arr[i] ≤ 10⁵

---

## 💻 Code

```java
class Solution {
    ArrayList<Integer> countDistinct(int arr[], int k) {
        int n = arr.length, unique = 0;
        int[] freq = new int[100001];
        for(int i = 0; i < k; i++){
            freq[arr[i]]++;
            if(freq[arr[i]] == 1){
                unique++;
            }
        }
        ArrayList<Integer> ans = new ArrayList<>();
        ans.add(unique);
        for(int i = k; i < n; i++){
            freq[arr[i - k]]--;
            if(freq[arr[i - k]] == 0){
                unique--;
            }
            freq[arr[i]]++;
            if(freq[arr[i]] == 1){
                unique++;
            }
            ans.add(unique);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
