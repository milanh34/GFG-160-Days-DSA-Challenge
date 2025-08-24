<h1 align="center">🧩 Clone an Undirected Graph 🧩</h1>

---

## 📝 Problem Statement
Given a **connected undirected graph** represented by adjacency list, `adjList[][]` with `n` nodes, having a **distinct label** from `0` to `n-1`, where each `adj[i]` represents the list of vertices connected to vertex `i`.

Create a **clone** of the graph, where each node in the graph contains an integer `val` and an array (`neighbors`) of nodes, containing nodes that are adjacent to the current node.

```java
class Node {
    int val;
    ArrayList<Node> neighbors;
}
```

Your task is to complete the function `cloneGraph( )` which takes a starting node of the graph as input and returns the **copy of the given node** as a reference to the cloned graph.

> Note: If you return a **correct copy** of the given graph, then the driver code will print `true`; and if an incorrect copy is generated or when you return the original node, the driver code will print `false`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
n = 4
adjList = [[1, 2], [0, 2], [0, 1, 3], [2]]

```

**Output:**
```
true
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893038/Web/Other/blobid0_1744464094.jpg" width="720"> </img>

The cloned graph is identical to the original one, so the driver prints true. 

---

### ✅ Example 2:

**Input:**
```
n = 3
adjList = [[1, 2], [0], [0]]

```

**Output:**
```
true
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/893038/Web/Other/blobid1_1744465861.jpg" width="720"> </img>

The cloned graph is structurally identical.

---

## 🧠 Approach
We solve this problem using **BFS traversal**:

1. Create a **map** to store mapping from original nodes → cloned nodes.
2. Initialize a `queue` for BFS, starting with the given node.
3. For each `node`:
    - If a `neighbor` is not cloned, create its clone and add to `queue`.
    - Add the cloned neighbor to the current cloned node’s adjacency list.
4. Continue until all nodes are cloned.
5. This ensures that all nodes and edges are **deep-copied**.

---

## ⏱️ Time & Space Complexity
| Complexity | Value | Explanation |
|------------|-------|-------------|
| Time       | O(V + E) | Each vertex and edge processed once |
| Space      | O(V) | HashMap + Queue + cloned graph |

---

## 🎯 Constraints
- 1 ≤ `n` ≤ 10⁴
- 0 ≤ no. of edges ≤ 10⁵  
- 0 ≤ `adjList[i][j]` < `n` 

---

## 💻 Code
```java
/*
    class Node{
        int val;
        ArrayList<Node> neighbors;
        public Node(){
            val = 0;
            neighbors = new ArrayList<>();
        }

        public Node(int val){
            this.val = val;
            neighbors = new ArrayList<>();
        }

        public Node(int val, ArrayList<Node> neighbors){
            this.val = val;
            this.neighbors = neighbors;
        }
    }
*/
class Solution {
    Node cloneGraph(Node node) {
        Node ans = new Node(node.val);
        Map<Node, Node> map = new HashMap<>();
        map.put(node, ans);
        Queue<Node> queue = new LinkedList<>();
        queue.offer(node);
        while(!queue.isEmpty()){
            Node a = queue.poll();
            for(Node i: a.neighbors){
                if(!map.containsKey(i)){
                    queue.offer(i);
                    map.put(i, new Node(i.val));
                }
                map.get(a).neighbors.add(map.get(i));
            }
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. **Base Case**: If `node == null`, return `null`.
2. **Clone root node**: Create a new node `ans` for the starting node.
3. **HashMap**: Store mapping `original → clone`.
4. **BFS traversal**:
    - For each node, check neighbors.
    - If neighbor is not yet cloned, clone it and push to queue.
    - Add the cloned neighbor to the cloned node’s adjacency list.
5. **Return cloned graph** starting node.

This guarantees a **deep copy** of the graph.

---

> Made with ❤️ by Milan Haria
