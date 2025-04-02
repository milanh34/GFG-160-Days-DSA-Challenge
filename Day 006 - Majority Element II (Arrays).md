<h1 align="center">✨ Majority Element II ✨</h1>

---

## 🧩 Problem Statement

You are given an array `arr[]` of integers, where each number represents a vote for a candidate. Your task is to return the candidates who have votes greater than **one-third of the total votes**. If no such candidates exist, return an empty array.

> 📊 **Note:** The answer should be sorted in increasing order.

---

## 🧪 Examples

### ✅ Example 1:
**Input:**  
```
arr = [2, 1, 5, 5, 5, 5, 6, 6, 6, 6, 6]
```

**Output:**  
```
[5, 6]
```

**Explanation:**  
Both `5` and `6` occur more than `n/3` times in the array, so they are returned as the majority elements.

---

### ✅ Example 2:
**Input:**  
```
arr = [1, 2, 3, 4, 5]
```

**Output:**  
```
[]
```

**Explanation:**  
No candidate occurs more than `n/3` times, so we return an empty array.

---

## 🧠 Approach

### 🧮 Key Idea:

To find the majority element, we need to count the occurrences of each element and then check if any of them appears more than `n/3` times.

- **Step 1**: Count the frequency of each element in the array.
- **Step 2**: Check if any element's frequency is greater than `n/3`.
- **Step 3**: Return the candidates in ascending order.

> 🔍 **Optimized Approach**:  
Instead of using a brute force approach, we can use a **hash map** to count occurrences efficiently.

---

### 🧑‍💻 Detailed Steps:

1. **Count Frequencies**:  
   We can use a `HashMap` to count the frequency of each element. For each element in the array, we'll update its count in the map.

2. **Filter Candidates**:  
   After counting the frequencies, we iterate through the map to check if any element’s count exceeds `n/3`. If it does, we add it to our result list.

3. **Sort the Result**:  
   Since the output needs to be sorted in increasing order, we sort the result list before returning it.

---

## ⏱️ Time & Space Complexity

| Complexity | Value             | Reason                         |
|------------|-------------------|--------------------------------|
| 🕒 Time     | `O(n log n)`       | `n` for iterating through array and `log n` for sorting the result. |
| 📦 Space    | `O(n)`             | Space for storing counts in the `HashMap`. |

> 🔍 **Note:** The time complexity could be optimized to `O(n)` for the counting part if we use a more sophisticated approach, but here we sort the result for simplicity.

---

## 🎯 Constraints

- `1 ≤ arr.size() ≤ 10⁶`
- `-10⁹ ≤ arr[i] ≤ 10⁹`

---

## 💻 Code

```java
import java.util.*;

class Solution {
    public List<Integer> findMajority(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        int oneThird = nums.length / 3;
        List<Integer> ans = new ArrayList<>();
        for(int i: nums){
            map.put(i, map.getOrDefault(i, 0) + 1);
        }
        for(int i: map.keySet()){
            if(map.get(i) > oneThird){
                ans.add(i);
            }
        }
        Collections.sort(ans);
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
