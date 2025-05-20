<h1 align="center"> 🔺 Count the Number Of Possible Triangles 🔺</h1>

---

## 📝 Problem Statement

Given an array `arr[]` of integers representing side lengths, **count the number of triplets** (i, j, k) such that:

```
arr[i] + arr[j] > arr[k]
arr[i] + arr[k] > arr[j]
arr[j] + arr[k] > arr[i]
```

That is, the **three elements** can form a valid triangle.

---

## ✅ Examples

### ✅ Example 1
**Input:**  
```
arr = [4, 6, 3, 7]
```  
**Output:**  
```
3
```  
**Explanation:**  
Possible triangles:  
- [3, 4, 6]  
- [4, 6, 7]  
- [3, 6, 7]

---

### ✅ Example 2
**Input:**  
````
arr = [10, 21, 22, 100, 101, 200, 300]
````  
**Output:**  
```
6
```  
**Explanation:**  
Valid triangles include:  
- [10, 21, 22]  
- [21, 100, 101]  
- [22, 100, 101]  
- [10, 100, 101]  
- [100, 101, 200]  
- [101, 200, 300]

---

### ✅ Example 3
**Input:**  
```
arr = [1, 2, 3]
```  
**Output:**  
```
0
```  
**Explanation:**  
No valid triangles can be formed.

---

## 🧠 Approach

1. **Sort the array** to make triangle condition checking easier.
2. For each index `i` from 2 to `n-1`, use two pointers from the start up to `i-1`.
3. If `arr[beg] + arr[end] > arr[i]`, then **all pairs from beg to end-1** also form valid triangles.
4. Move `end` back to check new combinations.
5. If not, move `beg` forward.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value     |
|------------------|-----------|
| 🕒 Time          | O(n²)     |
| 📦 Space         | O(1)      |

---

## 🎯 Constraints

- 1 ≤ arr.length ≤ 10³  
- 0 ≤ arr[i] ≤ 10⁵

---

## 💻 Java Code

```java
class Solution {
    static int countTriangles(int arr[]) {
        Arrays.sort(arr);
        int n = arr.length, ans = 0;
        for(int i = 2; i < n; i++){
            int beg = 0, end = i - 1;
            while(beg < end){
                if(arr[beg] + arr[end] > arr[i]){
                    ans += end - beg;
                    end--;
                } else{
                    beg++;
                }
            }
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
