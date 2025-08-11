<h1 align="center">🌐 DFS of Graph 🌐</h1>

---

## 📝 Problem Statement
Given a **connected undirected graph** with `V` vertices represented as a 2D adjacency list `adj[][]`,  
perform a **Depth First Search (DFS)** traversal starting from vertex **0**.  
The traversal must **visit vertices in the same order** as they appear in the adjacency list.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
adj = [[2, 3, 1], [0], [0, 4], [0], [2]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700203/Web/Other/blobid0_1728647807.jpg" width="540"></img>

**Output:**
```
[0, 2, 4, 3, 1]
```

**Explanation:**  
1. Start at vertex 0 → Visit `0`  
2. First neighbor is `2` → Visit `2`  
3. First neighbor of `2` is `4` → Visit `4`  
4. Backtrack to `2`, then `0` → Visit `3`  
5. Backtrack to `0` → Visit `1`  

---


### ✅ Example 2:

**Input:**
```
adj = [[1, 2], [0, 2], [0, 1, 3, 4], [2], [2]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700203/Web/Other/blobid1_1728648013.jpg" width="540"></img>

**Output:**
```
[0, 1, 2, 3, 4]
```

**Explanation:**  
- Start at `0` → Visit `1` → Visit `2` → Visit `3` → Backtrack → Visit `4`

---

## 🧠 Approach
1. Use a **stack** to simulate the recursive DFS process.  
2. Maintain a **visited[]** array to avoid revisiting vertices.  
3. Start with vertex `0` in the stack.  
4. For each popped vertex:  
   - Mark it visited and add to the result list.  
   - Push its neighbors in reverse order so that they are visited in the correct order.  
5. Continue until all vertices are visited.

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Description |
|------------|-------|-------------|
| Time       | O(V + E) | Visit each vertex once and traverse all edges |
| Space      | O(V) | Visited array + stack |

---

## 🎯 Constraints
- 1 ≤ `V` ≤ 10⁴  
- 1 ≤ `adj[i][j]` ≤ 10⁴  

---

## 💻 Code
```java
class Solution {
    public ArrayList<Integer> dfs(ArrayList<ArrayList<Integer>> adj) {
        int n = adj.size(), count = 0;
        ArrayList<Integer> ans = new ArrayList<>();
        boolean[] visited = new boolean[n];
        Stack<Integer> stack = new Stack<>();
        stack.push(0);
        while(count < n && !stack.isEmpty()){
            int a = stack.pop();
            if(!visited[a]){
                ans.add(a);
                visited[a] = true;
                count++;
                Stack<Integer> st = new Stack<>();
                for(int i: adj.get(a)){
                    st.push(i);
                }
                while(!st.isEmpty()){
                    stack.push(st.pop());
                }
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **`visited[]`** → Tracks which vertices have been visited.
- **`stack`** → Stores vertices for DFS traversal.
- For each popped vertex:
    - If not visited, add it to the answer.
    - Push neighbors in **reverse order** using a temporary stack to maintain original adjacency order.

---

> Made with ❤️ by Milan Haria
