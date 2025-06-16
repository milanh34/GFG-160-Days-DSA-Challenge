<h1 align="center">🌲 Height of Binary Tree 🌲</h1>

---

## 📝 Problem Statement

Given the `root` of a binary tree, return its **height**.

- The **height** of a binary tree is the **number of edges** on the longest path from the root to a **leaf node**.
- A **leaf node** is one with no left or right children.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
root = [12, 8, 18, 5, 11]
```  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700164/Web/Other/blobid0_1732510207.png"> </img>

**Output:**  
```
2
```  

**Explanation:**  
- One longest path is: `12 → 8 → 5`  
- This path has 2 edges (so height = 2)

---

### ✅ Example 2:

**Input:**  
```
root = [1, 2, 3, 4, N, N, 5, N, N, 6, 7]
```  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700164/Web/Other/blobid0_1732510207.png"> </img>

**Output:**  
```
3
```  

**Explanation:**  
- One longest path is: `1 → 2 → 4 → 6`  
- It contains 3 edges (so height = 3)

---

## 🧠 Approach

### Level-Order (BFS) Based Approach:
We use a **queue** to perform a level-order traversal, counting how many **levels** exist from the root to the bottom.

### Steps:
1. Initialize a queue and insert the root node.
2. While the queue is not empty:
   - For each level, process all nodes at that level.
   - Add their children (if any) to a temporary queue.
   - Increase level count.
3. Return `levelCount - 1` as height = number of edges.

---

## ⏱️ Time and Space Complexity

| Complexity | Value        | Description               |
|------------|--------------|---------------------------|
| Time       | O(n)         | Each node is visited once |
| Space      | O(n)         | For storing levels in queue |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10^5`
- `0 ≤ node->data ≤ 10^5`

---

## 💻 Code

```java
/*
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}
 */

class Solution {
    // Function to find the height of a binary tree.
    int height(Node node) {
        Queue<Node> queue = new LinkedList<>();
        queue.offer(node);
        int ans = 0;
        while(!queue.isEmpty()){
            Queue<Node> temp = new LinkedList<>();
            while(!queue.isEmpty()){
                Node a = queue.poll();
                if(a.left != null){
                    temp.offer(a.left);
                }
                if(a.right != null){
                    temp.offer(a.right);
                }
            }
            queue = temp;
            ans++;
        }
        return ans - 1;
    }
}
```

---

> Made with ❤️ by Milan Haria
