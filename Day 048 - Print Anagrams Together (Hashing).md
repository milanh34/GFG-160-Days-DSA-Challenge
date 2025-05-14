<h1 align="center">🔤 Print Anagrams Together 🔤</h1>

---

## 📝 Problem Statement

Given an array of strings, group the anagrams together.  
The anagrams in the result should be grouped in the **order of their appearance** in the original array.

---

## ✅ Examples

### ✅ Example 1:
**Input:**
```
arr = ["act", "god", "cat", "dog", "tac"]
```
**Output:**
```
[["act", "cat", "tac"], ["god", "dog"]]
```
**Explanation:**
- Group 1: "act", "cat", "tac" are anagrams (`act`, `cat`, `tac` all sort to `"act"`).
- Group 2: "god", "dog" are anagrams (`god`, `dog` both sort to `"dgo"`).

---

### ✅ Example 2:
**Input:**
```
arr = ["no", "on", "is"]
```
**Output:**
```
[["is"], ["no", "on"]]
```
**Explanation:**
- "is" is alone.
- "no" and "on" are anagrams (`"no"` and `"on"` both sort to `"no"`).

---

### ✅ Example 3:
**Input:**
```
arr = ["listen", "silent", "enlist", "abc", "cab", "bac", "rat", "tar", "art"]
```
**Output:**
```
[["listen", "silent", "enlist"], ["abc", "cab", "bac"], ["rat", "tar", "art"]]
```
**Explanation:**
- Group 1: "listen", "silent", "enlist" are anagrams (`"eilnst"`).
- Group 2: "abc", "cab", "bac" are anagrams (`"abc"`).
- Group 3: "rat", "tar", "art" are anagrams (`"art"`).

---

## 🧠 Approach

- For each string, sort its characters to create a unique key that will be the same for all its anagrams.
- Use a list to store these sorted strings.
- Use a boolean array to keep track of which strings have already been visited and grouped.
- Iterate through the strings:
  - For each unvisited string, start a new group.
  - Compare its sorted form with the rest, and if any match and are unvisited, add them to the same group.
- This ensures the order of appearance is maintained.

---

## ⏱️ Time & Space Complexity

| Complexity       | Value                | Description                           |
|------------------|----------------------|---------------------------------------|
| 🕒 Time          | `O(n * m log m)`     | Sorting every string + comparison    |
| 📦 Space         | `O(n * m)`           | To store sorted keys and results      |

Where `n` is the number of strings and `m` is the maximum string length.

---

## 🎯 Constraints

- `1 ≤ arr.length ≤ 100`
- `1 ≤ arr[i].length ≤ 10`

---

## 💻 Code

```java
class Solution {
    public ArrayList<ArrayList<String>> anagrams(String[] arr) {
        int n = arr.length, c = 0;
        List<String> list = new ArrayList<>();
        for(String s: arr){
            char[] ch = s.toCharArray();
            Arrays.sort(ch);
            list.add(new String(ch));
        }
        boolean[] visited = new boolean[n];
        ArrayList<ArrayList<String>> ans = new ArrayList<>();
        for(int i = 0; i < n; i++){
            if(!visited[i]){
                ans.add(new ArrayList<>());
                c++;
                ans.get(c - 1).add(arr[i]);
                visited[i] = true;
                for(int j = i + 1; j < n; j++){
                    if(!visited[j] && list.get(i).equals(list.get(j))){
                        ans.get(c - 1).add(arr[j]);
                        visited[j] = true;
                    }
                }
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. **Sorting Each String:**
    - For each string, convert it to a character array, sort it, and store the sorted string in a `list`.
    - This sorted string serves as the **anagram signature**.

2. **Grouping Anagrams:**
    - Use a `visited` array to keep track of which strings have been grouped.
    - For each unvisited string, create a new group and add it to the result.
    - Then compare its sorted signature with the rest of the strings and group any matching anagrams.

3. **Ensuring Order of Appearance:**
    - The loop goes linearly from `i = 0` to `n - 1`.
    - This ensures groups are created in the order of first appearance.

---

> Made with ❤️ by Milan Haria
