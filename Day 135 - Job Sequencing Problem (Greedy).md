<h1 align="center">💼 Job Sequencing Problem 💼</h1>

---

## 📝 Problem Statement

You are given:  
- `deadline[]` → deadline of each job  
- `profit[]` → profit of each job  

Each job takes **1 unit of time** and only one job can be done at a time.  
You earn the profit for a job only if it is **completed within its deadline**.

**Your Task:**  
Find:
1. **Maximum number of jobs** that can be completed within deadlines.  
2. **Maximum total profit** earned from these jobs.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
deadline = [4, 1, 1, 1]
profit = [20, 10, 40, 30]
```

**Output:**
```
[2, 60]
```

**Explanation:**  
- Job 1 (deadline 4, profit 20)  
- Job 3 (deadline 1, profit 40)  
Total Profit = 20 + 40 = 60.  
Max Jobs = 2.

---

### ✅ Example 2:

**Input:**
```
deadline = [2, 1, 2, 1, 1]
profit = [100, 19, 27, 25, 15]
```

**Output:**
```
[2, 127]
```

**Explanation:**  
- Job 1 (deadline 2, profit 100)  
- Job 3 (deadline 2, profit 27)  
Total Profit = 100 + 27 = 127.  
Max Jobs = 2.

---

### ✅ Example 3:

**Input:**
```
deadline = [3, 1, 2, 2]
profit = [50, 10, 20, 30]
```

**Output:**
```
[3, 100]
```

**Explanation:**  
- Job 1 (deadline 3, profit 50)  
- Job 3 (deadline 2, profit 20)  
- Job 4 (deadline 2, profit 30)  
Total Profit = 100.  
Max Jobs = 3.

---

## 🧠 Approach

We can solve this problem using a **Greedy + Min-Heap** approach:

1. **Pair jobs** with their profits and deadlines.
2. **Sort** jobs by deadline in ascending order.  
   - If deadlines are equal, sort by profit in descending order.
3. Use a **Min-Heap (Priority Queue)** to store selected jobs' profits.
4. For each job:
   - If the number of selected jobs (`queue.size()`) is less than its deadline, add it to the heap.
   - Otherwise, if the smallest profit job in the heap is less than the current job's profit, replace it.
5. At the end:
   - Heap size = number of jobs completed.
   - Sum of heap elements = total profit.

---

## ⏱️ Time and Space Complexity

| Complexity | Value          | Description                                      |
|------------|---------------|--------------------------------------------------|
| Time       | O(N log N)    | Sorting + Heap operations                         |
| Space      | O(N)          | Heap storing selected jobs' profits               |

---

## 🎯 Constraints

- 1 ≤ `deadline.length` = `profit.length` ≤ 10⁵  
- 1 ≤ `deadline[i]` ≤ `deadline.length`  
- 1 ≤ `profit[i]` ≤ 500  

---

## 💻 Code

```java
class Solution {
    public ArrayList<Integer> jobSequencing(int[] deadline, int[] profit) {
        int n = deadline.length, p = 0;
        int[][] arr = new int[n][2];
        for(int i = 0; i < n; i++){
            arr[i][0] = profit[i];
            arr[i][1] = deadline[i];
        }
        Arrays.sort(arr, (a, b) -> {
            if(a[1] == b[1]){
                return b[0] - a[0];
            }
            return a[1] - b[1];
        });
        PriorityQueue<Integer> queue = new PriorityQueue<>();
        for(int[] i: arr){
            if(i[1] > queue.size()){
                queue.offer(i[0]);
            } else if(queue.peek() < i[0]){
                queue.poll();
                queue.offer(i[0]);
            }
        }
        ArrayList<Integer> ans = new ArrayList<>();
        ans.add(queue.size());
        while(!queue.isEmpty()){
            p += queue.poll();
        }
        ans.add(p);
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **Job Storage**: Jobs are stored in `arr[][]` with (`profit`, `deadline`) format for easy sorting.
- **Sorting**: Ensures we consider jobs with earlier deadlines first, prioritizing higher profits for same deadlines.
- **Heap Logic**: Maintains the best set of jobs that can be scheduled within deadlines.
- **Final Calculation**: The heap size gives the number of jobs completed, and summing heap elements gives the maximum profit.

---

> Made with ❤️ by Milan Haria
