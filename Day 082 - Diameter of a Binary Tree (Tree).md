<h1 align="center">🌐 Diameter of a Binary Tree 🌐</h1>

---

## 📝 Problem Statement

Given a binary tree, the **diameter** (also known as width) is defined as the **number of edges** on the **longest path** between **any two leaf nodes** in the tree.

- The path **may or may not pass through the root**.
- Your task is to return the **diameter of the binary tree**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
root = [1, 2, 3]
```  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/897090/Web/Other/blobid0_1748677796.png" width="600"> </img>


**Output:**  
```
2
```  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/897090/Web/Other/blobid1_1748677796.png" width="600"> </img>

**Explanation:**  
- The longest path is: `2 → 1 → 3`  
- Number of edges = 2

---

### ✅ Example 2:

**Input:**  
```
root = [5, 8, 6, 3, 7, 9]
``` 

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/897090/Web/Other/blobid2_1748677797.png" width="600"> </img>

**Output:**  
```
4
```  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/897090/Web/Other/blobid3_1748677796.png" width="600"> </img>

**Explanation:**  
- Longest path: `3 → 8 → 5 → 6 → 9`  
- Number of edges = 4

---

## 🧠 Approach

### Observation:
- The **diameter** is the **sum of the heights** of left and right subtrees for **every node**, and we keep track of the **maximum**.

### Steps:
1. Use a recursive function `traverse(node, ans)`:
   - Compute height of left and right subtrees.
   - Update the global maximum diameter (`left + right`).
2. Return the stored maximum.

---

## ⏱️ Time and Space Complexity

| Complexity | Value      | Description                           |
|------------|------------|----------------------------------------|
| Time       | O(n)       | Each node is visited once             |
| Space      | O(h)       | Recursive stack space (h = tree height) |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10⁵`
- `0 ≤ node->data ≤ 10⁵`

---

## 💻 Code

```java
/*
class Node {
    int data;
    Node left;
    Node right;
    Node(int data) {
        this.data = data;
        left = null;
        right = null;
    }
}
*/
class Solution {
    int traverse(Node root, int[] ans){
        if(root == null){
            return 0;
        }
        int left = traverse(root.left, ans), right = traverse(root.right, ans);
        ans[0] = Math.max(ans[0], left + right);
        return 1 + Math.max(left, right);
    }
    int diameter(Node root) {
        int[] ans = new int[1];
        traverse(root, ans);
        return ans[0];
    }
}
```

---

> Made with ❤️ by Milan Haria
