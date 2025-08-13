<h1 align="center">🌐 BFS of Graph 🌐</h1>

---

## 📝 Problem Statement
Given a **connected undirected graph** with `V` vertices represented as a 2D adjacency list `adj[][]`,  
perform a **Breadth First Search (BFS)** traversal starting from vertex **0**.  
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
[0, 2, 3, 1, 4]
```

**Explanation:**  
1. Start at `0` → Visit `0`  
2. Add neighbors of `0` → `2, 3, 1`  
3. Visit `2` → Add neighbor `4`  
4. Visit `3` → No new neighbor  
5. Visit `1` → No new neighbor  
6. Visit `4` → No new neighbor 

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
- Start at `0` → Add `1, 2`  
- Visit `1` → Add `2` (already in queue)  
- Visit `2` → Add `3, 4`  
- Visit `3` → No new neighbor  
- Visit `4` → End  

---

## 🧠 Approach
1. Use a **queue** for BFS traversal.  
2. Maintain a **visited[]** array to avoid revisiting vertices.  
3. Start from vertex `0` and push it into the queue.  
4. For each dequeued vertex:  
   - Mark it visited and add it to the result list.  
   - Enqueue all its neighbors.  
5. Continue until all vertices are visited.

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Description |
|------------|-------|-------------|
| Time       | O(V + E) | Each vertex and edge is visited once |
| Space      | O(V) | Visited array + queue |

---

## 🎯 Constraints
- 1 ≤ `V` ≤ 10⁴  
- 1 ≤ `adj[i][j]` ≤ 10⁴  

---

## 💻 Code
```java
class Solution {
    public ArrayList<Integer> bfs(ArrayList<ArrayList<Integer>> adj) {
        int n = adj.size(), count = 0;
        ArrayList<Integer> ans = new ArrayList<>();
        Queue<Integer> queue = new LinkedList<>();
        boolean[] visited = new boolean[n];
        queue.offer(0);
        while(count < n && !queue.isEmpty()){
            int a = queue.poll();
            if(!visited[a]){
                visited[a] = true;
                count++;
                ans.add(a);
                for(int i: adj.get(a)){
                    queue.add(i);
                }
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **`visited[]`** → Prevents revisiting a vertex.
- **`queue`** → Maintains vertices to be processed in BFS order.
- For each dequeued vertex:
    - If not visited, mark as visited and add to output.
    - Enqueue all its neighbors in given adjacency list order.

---

> Made with ❤️ by Milan Haria
