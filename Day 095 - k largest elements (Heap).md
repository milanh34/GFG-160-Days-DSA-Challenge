<h1 align="center">🔢 K Largest Elements 🔢</h1>

---

## 📝 Problem Statement

Given an array of positive integers `arr[]` and an integer `k`, return the **k largest elements** in **decreasing order**.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
arr[] = [12, 5, 787, 1, 23], k = 2
```

**Output:**  
```
[787, 23]
```

**Explanation:**  
- 1st largest: 787  
- 2nd largest: 23

---

### ✅ Example 2

**Input:**  
```
arr[] = [1, 23, 12, 9, 30, 2, 50], k = 3
```

**Output:**  
```
[50, 30, 23]
```

**Explanation:**  
- Top 3 largest: 50, 30, 23

---

### ✅ Example 3

**Input:**  
```
arr[] = [12, 23], k = 1
```

**Output:**  
```
[23]
```

**Explanation:**  
- 1st largest: 23

---

## 🧠 Approach

- Use a **Max Heap** (`PriorityQueue` with custom comparator).
- Add all elements to the Max Heap.
- Extract the top `k` elements.

---

## ⏱️ Time and Space Complexity

| Complexity | Value         | Description                        |
|------------|---------------|------------------------------------|
| Time       | O(n log n)    | Insert all elements into heap      |
| Space      | O(n)          | Heap stores all elements           |

---

## 🎯 Constraints

- `1 ≤ k ≤ arr.size() ≤ 10⁶`
- `1 ≤ arr[i] ≤ 10⁶`

---

## 💻 Code

```java
class Solution {
    public ArrayList<Integer> kLargest(int[] arr, int k) {
        PriorityQueue<Integer> queue = new PriorityQueue<>((a, b) -> b - a);
        for(int i: arr){
            queue.offer(i);
        }
        ArrayList<Integer> list = new ArrayList<Integer>();
        while(k > 0){
            list.add(queue.poll());
            k--;
        }
        return list;
    }
}
```

---

> Made with ❤️ by Milan Haria
