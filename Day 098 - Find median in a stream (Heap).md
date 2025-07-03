<h1 align="center">📈 Find Median in a Stream 📈</h1>

---

## 📝 Problem Statement

Given a **data stream** `arr[]` where integers are read one by one, your task is to determine the **median** of the elements seen so far **after each new integer is read**.

> **Rules:**
> 1. If the count of elements is **odd**, the **middle element** is the median.
> 2. If the count is **even**, the **median** is the **average of the two middle elements**.

---

## ✅ Examples

### ✅ Example 1

**Input:**
```
arr[] = [5, 15, 1, 3, 2, 8]
```

**Output:**
```
[5.0, 10.0, 5.0, 4.0, 3.0, 4.0]
```

**Explanation:**
- After reading [5] → median = 5.0  
- After [5, 15] → median = (5+15)/2 = 10.0  
- After [5, 15, 1] → median = 5.0  
- After [5, 15, 1, 3] → median = (3+5)/2 = 4.0  
- After [5, 15, 1, 3, 2] → median = 3.0  
- After [5, 15, 1, 3, 2, 8] → median = (3+5)/2 = 4.0  

---

### ✅ Example 2

**Input:**
```
arr[] = [2, 2, 2, 2]
```

**Output:**
```
[2.0, 2.0, 2.0, 2.0]
```

**Explanation:**
- After each element, the median stays 2.0.

---

## 🧠 Approach

### Key Idea:
1. Use two heaps:
- **Max Heap** for the **smaller half** of elements.
- **Min Heap** for the **larger half** of elements.
2. The heaps maintain balance:
- `max` heap always has the same number or **one more element** than `min` heap.

### Steps:
1. Insert new number into `max` heap.
2. Move the largest in `max` to `min` to maintain order.
3. Balance sizes so `max` never has fewer elements than `min`.
4. Compute median:
   - If `max` is larger → median is `max.peek()`.
   - If sizes are equal → median is average of `max.peek()` and `min.peek()`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value     | Description              |
|------------|-----------|--------------------------|
| Time       | O(n log n)| For insertion in heaps   |
| Space      | O(n)      | To store heap elements   |

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10⁵`
- `1 ≤ x ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    public ArrayList<Double> getMedian(int[] arr) {
        PriorityQueue<Integer> max = new PriorityQueue<>((a, b) -> b - a), min = new PriorityQueue<>();
        ArrayList<Double> ans = new ArrayList<>();
        for(int i: arr){
            max.offer(i);
            min.offer(max.poll());
            if(max.size() < min.size()){
                max.offer(min.poll());
            }
            ans.add(max.size() > min.size() ? (double)max.peek() : (double)(max.peek() + min.peek()) / 2);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
