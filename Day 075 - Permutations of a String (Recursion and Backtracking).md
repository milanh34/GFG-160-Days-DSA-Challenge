<h1 align="center">🔁 Permutations of a String 🔁</h1>

---

## 📝 Problem Statement

Given a string `s`, which may contain **duplicate characters**, your task is to generate and return an array of **all unique permutations** of the string.  
You can return the answer in **any order**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
s = "ABC"
```

**Output:**  
```
["ABC", "ACB", "BAC", "BCA", "CAB", "CBA"]
```

**Explanation:**  
- "ABC" has 3 unique characters.
- Total unique permutations = 3! = 6.
- All combinations are returned.

---

### ✅ Example 2:

**Input:**  
```
s = "ABSG"
```

**Output:**  
```
["ABGS", "ABSG", "AGBS", "AGSB", "ASBG", "ASGB", "BAGS", "BASG", "BGAS", "BGSA", "BSAG", "BSGA", "GABS", "GASB", "GBAS", "GBSA", "GSAB", "GSBA", "SABG", "SAGB", "SBAG", "SBGA", "SGAB", "SGBA"]
```

**Explanation:**  
- "ABSG" has 4 unique characters.
- Total unique permutations = 4! = 24.
- Since all characters are distinct, all 24 permutations are unique and returned.

---

### ✅ Example 3:

**Input:**  
```
s = "AAA"
```

**Output:**  
```
["AAA"]
```

**Explanation:**  
- All characters are the same.
- Only one unique permutation is possible → "AAA".

---

## 🧠 Approach

- Use **Backtracking** to explore all possible arrangements of the characters.
- Maintain a `visited[]` array to ensure each character is used only once per path.
- Use a **HashSet** to store only **unique** permutations (to avoid duplicates).
- A `StringBuilder` is used to build strings efficiently.
- After generating all permutations, convert the set to an `ArrayList` and return it.

---

## ⏱️ Time and Space Complexity

| Complexity | Value                    | Description                              |
|------------|--------------------------|------------------------------------------|
| Time       | O(N! × N)                | N! permutations × O(N) for building each |
| Space      | O(N!)                    | For storing all unique permutations      |

---

## 🎯 Constraints

- `1 <= s.length <= 9`  
- `s` contains only **uppercase English alphabets**

---

## 💻 Code

```java
class Solution {
    public void getAnswers(String s, boolean[] visited, Set<String> set, StringBuilder sb, int n, int i){
        if(i == n){
            set.add(sb.toString());
            return;
        }
        for(int j = 0; j < n; j++){
            if(!visited[j]){
                visited[j] = true;
                sb.append(s.charAt(j));
                getAnswers(s, visited, set, sb, n, i + 1);
                visited[j] = false;
                sb.deleteCharAt(sb.length() - 1);
            }
        }
    }
    public ArrayList<String> findPermutation(String s) {
        int n = s.length();
        boolean[] visited = new boolean[n];
        Set<String> set = new HashSet<>();
        StringBuilder sb = new StringBuilder();
        getAnswers(s, visited, set, sb, n, 0);
        return new ArrayList<>(set);
    }
}
```

---

> Made with ❤️ by Milan Haria
