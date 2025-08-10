<h1 align="center">⛽ Gas Station ⛽</h1>

---

## 📝 Problem Statement
You are given:
- `gas[]` → amount of gas available at each station.
- `cost[]` → gas needed to travel to the next station.

You start with an **empty tank** and can begin from **any station**.  
Your task is to find the **index of the starting station** from which you can **travel around the circuit once** without running out of gas.  

If no such starting station exists, return `-1`.  
If a solution exists, it is **guaranteed to be unique**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
gas  = [4, 5, 7, 4]  
cost = [6, 6, 3, 5]  
```

**Output:**  
```
2  
```

**Explanation:**  
- Start at station 2 → Gas = `0 + 7 = 7`  
- Go to station 3 → Gas = `7 - 3 + 4 = 8`  
- Go to station 0 → Gas = `8 - 5 + 4 = 7`  
- Go to station 1 → Gas = `7 - 6 + 5 = 6`  
- Return to station 2 → Gas = `6 - 6 = 0` ✅ Possible.

---

### ✅ Example 2:

**Input:**  
```
gas  = [1, 2, 3, 4, 5]  
cost = [3, 4, 5, 1, 2]  
```

**Output:**  
```
3  
```

**Explanation:**  
- Start at station 3 → Gas = `0 + 4 = 4`  
- Go to station 4 → Gas = `4 - 1 + 5 = 8`  
- Go to station 0 → Gas = `8 - 2 + 1 = 7`  
- Go to station 1 → Gas = `7 - 3 + 2 = 6`  
- Go to station 2 → Gas = `6 - 4 + 3 = 5`  
- Return to station 3 → Gas = `5 - 5 = 0` ✅ Possible.

---

### ✅ Example 3:

**Input:**  
```
gas  = [3, 9]  
cost = [7, 6]  
```

**Output:**  
```
-1  
```

**Explanation:**  
There’s no starting point where the trip can be completed.

---

## 🧠 Approach
We use a **greedy** approach:

1. Traverse stations from left to right, keeping track of the current gas balance (`prefix`).
2. If the gas balance becomes negative, **reset the start point** to the next station and set `prefix = 0`.
3. After finding a candidate starting point, check if completing the loop is possible.
4. If yes, return the starting index; else return `-1`.

---

## ⏱️ Time and Space Complexity
| Complexity | Value  | Description |
|------------|--------|-------------|
| Time       | O(N)   | Two passes over the array |
| Space      | O(1)   | No extra space used |

---

## 🎯 Constraints
- 1 ≤ `gas.length`, `cost.length` ≤ 10⁶  
- 1 ≤ `gas[i]`, `cost[i]` ≤ 10³  

---

## 💻 Code
```java
class Solution {
    public int startStation(int[] gas, int[] cost) {
        int n = gas.length, prefix = 0, beg = 0;
        for(int i = 0; i < n; i++){
            prefix += gas[i] - cost[i];
            if(prefix < 0){
                beg = i + 1;
                prefix = 0;
            }
        }
        prefix = 0;
        for(int i = 0; i < n; i++){
            int j = (beg + i) % n;
            prefix += gas[j] - cost[j];
            if(prefix < 0){
                return -1;
            }
        }
        return beg;
    }
}
```

---

## 📝 Explanation of Code

- **First loop**: Determines a candidate starting station by resetting when gas goes negative.
- **Second loop**: Checks if the trip is possible starting from that station.
- **Return**: The valid starting index or `-1` if impossible.

---

> Made with ❤️ by Milan Haria
