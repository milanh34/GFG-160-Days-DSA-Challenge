<h1 align="center">🔍 Find H-Index 🔍</h1>

---

## 📝 Problem Statement

Given an integer array `citations[]`, where `citations[i]` is the number of citations a researcher received for the ith paper, the task is to find the **H-index**.

### What is the H-Index?
The **H-Index** is the largest value such that the researcher has at least **H papers** that have been cited at least **H times**.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
citations[] = [3, 0, 5, 3, 0]
```

**Output:**  
```
3
```

**Explanation:**  
There are at least 3 papers (with citation counts 3, 5, and 3) that have at least 3 citations.

---

### ✅ Example 2:
**Input:**  
```
citations[] = [5, 1, 2, 4, 1]
```

**Output:**  
```
2
```

**Explanation:**  
There are 3 papers with citation counts of 5, 2, and 4 that have at least 2 citations. However, the H-Index cannot be 3 because there aren't 3 papers with 3 or more citations.

---

### ✅ Example 3:
**Input:**  
```
citations[] = [0, 0]
```

**Output:**  
```
0
```

**Explanation:**  
There are no papers with any citations, so the H-Index is 0.

---

## 🧠 Approach

To calculate the H-index, we need to find the largest integer **H** such that the researcher has at least **H papers** with **at least H citations**.

### Steps:
1. **Count the Citations**: 
   We first count the occurrences of each citation count using a frequency array.
   
2. **Find the H-Index**:
   We then calculate the H-index by iterating through the frequency array from the largest possible citation count, checking if the number of papers with citations greater than or equal to the current index is greater than or equal to the current index.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     | Description                               |
|------------------|-----------|-------------------------------------------|
| 🕒 Time          | `O(n)`    | We iterate over the array once to count citations and again to find the H-index. |
| 📦 Space         | `O(n)`    | We use an auxiliary array to count citation occurrences. |

---

## 🎯 Constraints

- `1 ≤ citations.size() ≤ 10⁶`
- `0 ≤ citations[i] ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    public int hIndex(int[] citations) {
        int n = citations.length, sum = 0;
        int[] count = new int[n + 1];
        for(int i: citations){
            if(i >= n){
                count[n]++;
            } else{
                count[i]++;
            }
        }
        while(n >= 0){
            sum += count[n];
            if(sum >= n){
                return n;
            }
            n--;
        }
        return 0;
    }
}
```

---

## 📝 Explanation of Code

- **Step 1**: We create an array `count[]` to store the frequency of citations.
    - If a citation count is greater than or equal to the length of the array (i.e., greater than or equal to `n`), we increment the count at `count[n]`.
    - Otherwise, we increment the count at the index equal to the citation count.
  
- **Step 2**: We iterate through the `count[]` array in reverse order, keeping track of the sum of the papers with at least `n` citations.
    - As soon as the sum is greater than or equal to `n`, we return `n` as the H-index.

---


> Made with ❤️ by Milan Haria
