<h1 align="center">🌳 Check for Binary Search Tree (BST) 🌳</h1>

---

## 📝 Problem Statement

Given the root of a binary tree, check whether it is a **Binary Search Tree (BST)** or not.

### Rules for a BST:
- The **left subtree** of a node contains only nodes with **keys less than** the node’s key.
- The **right subtree** contains only nodes with **keys greater than** the node’s key.
- **No duplicate** keys are allowed.
- Both left and right subtrees must also be **BSTs**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
root = [2, 1, 3, N, N, N, 5]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700149/Web/Other/blobid0_1739182093.jpg"> </img>

**Output:**
```
true
```

**Explanation:**  
All nodes follow BST properties.

---

### ✅ Example 2:

**Input:**
```
root = [2, N, 7, N, 6, N, 9]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700149/Web/Other/blobid2_1739182131.jpg"> </img>

**Output:**
```
false
```

**Explanation:**  
Node 6 is in the right subtree of 2 and should be > 2 and < 7, but it's not, so it's invalid.

---

### ✅ Example 3:

**Input:**
```
root = [10, 5, 20, N, N, 9, 25]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700149/Web/Other/blobid3_1739182159.jpg"> </img>

**Output:**
```
false
```

**Explanation:**  
Node 9 is in the right subtree of 10 but has a smaller value, violating BST rules.

---

## 🧠 Approach

Use recursion and **min/max boundaries** to validate if each node satisfies BST properties.

### Steps:
1. Start from root, initialize range as `(-∞, ∞)`.
2. For each node:
   - Check if `node.data` is between `(min, max)`.
   - Recurse left with new max as `node.data`.
   - Recurse right with new min as `node.data`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value          | Description                           |
|------------|----------------|---------------------------------------|
| Time       | O(n)           | Each node is visited once             |
| Space      | O(h)           | Recursive stack (h = height of tree)  |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10⁵`
- `1 ≤ node->data ≤ 10⁹`

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
    boolean traverse(Node node, int min, int max){
        return node == null || (node.data > min && node.data < max && traverse(node.left, min, node.data) && traverse(node.right, node.data, max));
    }
    boolean isBST(Node root) {
        return traverse(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }
}
```

---

## 📝 Explanation of Code

- isBST() starts by calling traverse with range (MIN_VALUE, MAX_VALUE)
- traverse(node, min, max):
  → If node is null: valid by default
  → If node's value violates BST range: return false
  → Recursively check left subtree with updated max
  → Recursively check right subtree with updated min

---

> Made with ❤️ by Milan Haria
