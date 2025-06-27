<h1 align="center">🛠️ Fixing Two Nodes of a BST 🛠️</h1>

---

## 📝 Problem Statement

Given the **root of a Binary Search Tree (BST)** where **exactly two nodes** have been **swapped by mistake**, fix the BST by **swapping them back**.  
**Do not change the structure of the tree.**

> It is guaranteed that except for these two swapped nodes, the given input forms a valid BST.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
root = [10, 5, 8, 2, 20]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886490/Web/Other/blobid0_1738654776.png"> </img>

**Output:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886490/Web/Other/blobid1_1738654776.png"> </img>

**Explanation:**  
Nodes `8` and `20` were swapped by mistake. After fixing, the tree becomes a valid BST.

---

### ✅ Example 2

**Input:**  
```
root = [5, 10, 20, 2, 8]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886490/Web/Other/blobid2_1738654931.png"> </img>

**Output:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886490/Web/Other/blobid3_1738654931.png"> </img>

**Explanation:**  
Nodes `5` and `10` were swapped by mistake. After fixing, the tree is valid.

---

## 🧠 Approach

### Observation:
- An **in-order traversal** of a BST should produce a **sorted sequence**.
- If two nodes are swapped:
  - There will be **one or two points** in the in-order traversal where `prev.data > current.data`.
  - We must find these points to locate the incorrect nodes.

### Steps:
1. Perform **in-order traversal**.
2. Whenever `prev.data > current.data`:
   - Store the offending nodes in a list.
3. After traversal:
   - If there are **2 pairs (4 nodes)**, swap the **first and last**.
   - If there is **1 pair (2 nodes)**, swap them directly.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description                       |
|------------|-------|-----------------------------------|
| Time       | O(n)  | Visit each node once             |
| Space      | O(h)  | Stack space for recursion (h = height) |

---

## 🎯 Constraints

- `1 ≤ Number of nodes ≤ 10³`

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
    Node prev;
    List<Node> list;
    void traverse(Node node){
        if(node == null){
            return;
        }
        traverse(node.left);
        if(prev != null && prev.data > node.data){
            list.add(prev);
            list.add(node);
        }
        prev = node;
        traverse(node.right);
    }
    void correctBST(Node root) {
        prev = null;
        list = new ArrayList<>();
        traverse(root);
        int n = list.size();
        if(n == 4){
            int temp = list.get(0).data;
            list.get(0).data = list.get(3).data;
            list.get(3).data = temp;
        } else{
            int temp = list.get(0).data;
            list.get(0).data = list.get(1).data;
            list.get(1).data = temp;
        }
    }
}
```

---

> Made with ❤️ by Milan Haria
