<h1 align="center">🌳 Level Order Traversal 🌳</h1>

---

## 📝 Problem Statement

Given the `root` of a binary tree, return its **level order traversal** as a list of lists.  
Level order traversal is also called **Breadth-First Search (BFS)** traversal, where we print nodes level by level from top to bottom.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
root = [1, 2, 3]
```  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700511/Web/Other/blobid0_1738405019.png"> </img>

**Output:**  
```
[[1], [2, 3]]
```  

**Explanation:**  
- Level 0 → 1  
- Level 1 → 2, 3

---

### ✅ Example 2:

**Input:**  

```
root = [10, 20, 30, 40, 50]
```  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700511/Web/Other/blobid2_1738405085.png"> </img>

**Output:**  

```
[[10], [20, 30], [40, 50]]
```  

**Explanation:**  
- Level 0 → 10  
- Level 1 → 20, 30  
- Level 2 → 40, 50

---

### ✅ Example 3:

**Input:**  
```
root = [1, 3, 2, N, N, N, 4, 6, 5]
```  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700511/Web/Other/blobid3_1738405128.png"> </img>

**Output:**  
```
[[1], [3, 2], [4], [6, 5]]
```  

**Explanation:**  
Some nodes are missing (`N`) and some go deeper. We still visit left-to-right level by level.

---

## 🧠 Approach

We use a **queue** (FIFO) to perform a Breadth-First Search traversal.

### Steps:
1. Initialize a queue and insert the root node.
2. While the queue is not empty:
   - Create a temporary list to store the current level's values.
   - Iterate over all nodes at the current level.
   - For each node:
     - Add its value to the level list.
     - Enqueue its left and right children (if they exist).
3. Add each level's list to the final result.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description |
|------------|-------|--------|
| Time       | O(n)  | Every node is visited once |
| Space      | O(n)  | Queue + result storage     |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10^5`
- `0 ≤ node->data ≤ 10^9`

---

## 💻 Code

```java
/*
class Node {
    int data;
    Node left, right;

    Node(int item) {
        data = item;
        left = right = null;
    }
}
*/
class Solution {
    public ArrayList<ArrayList<Integer>> levelOrder(Node root) {
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
        while(!queue.isEmpty()){
            ArrayList<Integer> list = new ArrayList<>();
            Queue<Node> temp = new LinkedList<>();
            while(!queue.isEmpty()){
                Node a = queue.poll();
                list.add(a.data);
                if(a.left != null){
                    temp.add(a.left);
                }
                if(a.right != null){
                    temp.add(a.right);
                }
            }
            queue = temp;
            ans.add(list);
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
