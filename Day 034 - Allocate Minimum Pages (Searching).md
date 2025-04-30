<h1 align="center">📚 Allocate Minimum Pages 📚</h1>

---

## 📝 Problem Statement

You are given an array `arr[]`, where each element represents the **number of pages in a book**.  
There are `k` students, and you need to **allocate books to these students** such that:

1. **Each student gets at least one book.**
2. **Books assigned to a student must be in a contiguous block** (i.e., consecutive elements in the array).
3. **No book is assigned to more than one student.**
4. Your goal is to **minimize the maximum number of pages assigned to any student**.

If it's not possible to allocate the books under the above conditions, return `-1`.

---

## ✅ Examples

### ✅ Example 1:
**Input:**  
```
arr = [12, 34, 67, 90], k = 2
```
**Output:**  
```
113
```
**Explanation:**  
Possible allocations:
- [12] and [34, 67, 90] → max pages = 191
- [12, 34] and [67, 90] → max pages = 157
- [12, 34, 67] and [90] → max pages = 113 ✅

The goal is to minimize the **maximum pages** given to any student. So, the optimal answer is `113`.

---

### ✅ Example 2:
**Input:**  
```
arr = [15, 17, 20], k = 5
```
**Output:**
```
-1
```
**Explanation:**  
You only have 3 books and 5 students. Since every student must get **at least one book**, allocation is **not possible**.

---

## 🧠 Approach

This is a classic **Binary Search on Answer** problem:

1. **Minimum pages** a student must read = max(arr) (a student must take the largest book).
2. **Maximum pages** a student might read = sum(arr) (1 student reads all books).
3. Use binary search to find the minimum **maximum pages**:
   - For each `mid`, simulate assigning books to students.
   - If we can do it with ≤ `k` students, try a smaller value.
   - Otherwise, increase the lower bound.

### 🧪 Steps:

1. **Start the binary search:**
   - `low = max(arr)` → because no student can get less than the largest book.
   - `high = sum(arr)` → because one student reading all books is the worst case.
2. **Mid-check logic:**
   - Traverse the array and simulate allocation.
   - If current book pages + running sum exceeds `mid`, allocate to a new student.
   - Count how many students are required.
3. **Adjust binary search:**
   - If number of students needed > `k`: `mid` is too small, increase `low`.
   - Else: Try better (smaller) `mid` by reducing `high`.

---

## ⏱️ Time & Space Complexity

| Complexity | Value                     | Description                                           |
|------------|---------------------------|--------------------------------------------------------------|
| 🕒 Time     | `O(N log(sum - max))`     | Binary search on the range [max(arr), sum(arr)] |
| 📦 Space    | `O(1)`                    | No extra space used apart from a few variables               |

---

## 🔒 Constraints

- `1 ≤ arr.length ≤ 10⁶`
- `1 ≤ arr[i] ≤ 10³`
- `1 ≤ k ≤ 10³`

---

## 💻 Code

```java
class Solution {
    public static int findPages(int[] arr, int k) {
        int n = arr.length, beg = 0, end = 0;
        if(n < k){
            return -1;
        }
        for(int i: arr){
            if(i > beg){
                beg = i;
            }
            end += i;
        }
        while(beg < end){
            int mid = beg + (end - beg) / 2;
            int count = 1, sum = 0;
            for(int i: arr){
                if(i + sum > mid){
                    sum = i;
                    count++;
                } else{
                    sum += i;
                }
            }
            if(count > k){
                beg = mid + 1;
            } else{
                end = mid;
            }
        }
        return beg;
    }
}
```

---

## 🧠 Code Explanation

- **`if (n < k) return -1;`**  
  Not enough books to assign at least one per student.

- **Binary Search Range:**
  - `beg`: Highest single book page count (minimum possible max).
  - `end`: Sum of all pages (maximum possible max).

- **Binary Search Loop:**
  - `mid`: Candidate max page value.
  - Loop through books:
    - If adding a book exceeds `mid`, assign to next student.
    - Count how many students are needed.
  - If `count > k`, increase `beg` (mid is too small).
  - Else, try smaller `mid` by updating `end`.

- **Return `beg`**:  
  Smallest possible value of maximum pages that can be assigned.

---

> Made with ❤️ by Milan Haria
