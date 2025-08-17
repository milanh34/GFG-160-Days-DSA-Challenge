<h1 align="center">📊 Topological Sort 📊</h1>

---

## 📝 Problem Statement
You are given a **Directed Acyclic Graph (DAG)** with `V` vertices (0 to V-1) and `E` edges.  
Each edge is represented as `edges[i] = [u, v]` which means a directed edge `u → v`.

Your task is to return a **Topological Sort** of the graph.  
A Topological Ordering ensures that for every directed edge `u → v`, node `u` comes **before** `v` in the ordering.

> If multiple topological orders exist, returning any one valid ordering is acceptable.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
V = 4, E = 3
edges = [[3, 0], [1, 0], [2, 0]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700255/Web/Other/blobid0_1744196747.jpg"> </img>

**Output:**
```
[3, 2, 1, 0]
```

**Explanation:**  
Some valid topological orders are:
- [3, 2, 1, 0]  
- [1, 2, 3, 0]  
- [2, 3, 1, 0]
---


### ✅ Example 2:

**Input:**
```
V = 6, E = 6
edges = [[1, 3], [2, 3], [4, 1], [4, 0], [5, 0], [5, 2]]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700255/Web/Other/blobid1_1744196789.jpg"> </img>

**Output:**
```
[4, 5, 0, 1, 2, 3]  
```

**Explanation:**  
Valid topological orders include:
- [4, 5, 0, 1, 2, 3]  
- [5, 2, 4, 0, 1, 3]  

---

## 🧠 Approach 

### Kahn’s Algorithm – BFS
1. Build an **adjacency list** from the given edges.  
2. Compute the **in-degree** of each node (number of incoming edges).  
3. Initialize a queue with all nodes having `inDegree = 0`.  
4. Process nodes from the queue:
   - Add them to the result ordering.  
   - Decrease the in-degree of their neighbors.  
   - If a neighbor’s in-degree becomes 0, push it into the queue.  
5. Continue until all nodes are processed.  

This ensures nodes are placed **before their dependencies**.

---

## ⏱️ Time and Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(V + E) | Each vertex and edge is processed once |
| Space      | O(V + E) | Adjacency list + queue + result storage |

---

## 🎯 Constraints
- 2 ≤ `V` ≤ 5000  
- 1 ≤ `E` ≤ min(10⁵, `V × (V - 1) / 2`)  

---

## 💻 Code
```java
class Solution {
    public static ArrayList<Integer> topoSort(int V, int[][] edges) {
        List<List<Integer>> adj = new ArrayList<>();
        ArrayList<Integer> ans = new ArrayList<>();
        int[] inDegree = new int[V];
        for(int i = 0; i < V; i++){
            adj.add(new ArrayList<>());
        }
        for(int[] i: edges){
            adj.get(i[0]).add(i[1]);
            inDegree[i[1]]++;
        }
        Queue<Integer> queue = new LinkedList<>();
        for(int i = 0; i < V; i++){
            if(inDegree[i] == 0){
                queue.offer(i);
            }
        }
        while(!queue.isEmpty()){
            int a = queue.poll();
            ans.add(a);
            for(int i: adj.get(a)){
                inDegree[i]--;
                if(inDegree[i] == 0){
                    queue.offer(i);
                }
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- **`inDegree[]`** → tracks dependencies of each node.
- **Queue** → holds all nodes that can be processed immediately (no remaining dependencies).
- Process nodes in queue, reduce dependencies of neighbors, and enqueue them if ready.
- Resulting list `ans` is a valid Topological Order.

---

> Made with ❤️ by Milan Haria
