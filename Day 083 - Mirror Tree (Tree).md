<h1 align="center">🌲 Mirror Tree 🌲</h1>

---

## 📝 Problem Statement

Given a binary tree, your task is to **convert it into its mirror tree**.

- The mirror of a binary tree is a tree where the **left and right children of every non-leaf node are swapped**.
- The structure of the tree remains the same; only the links between children change.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
root = [1, 2, 3, N, N, 4]
```

**Output:**
```
[1, 3, 2, N, 4]
```

**Explanation:**

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700155/Web/Other/blobid0_1736926809.png"> </img>

In the inverted tree, every non-leaf node has its left and right child interchanged.

---

### ✅ Example 2:

**Input:**
```
root = [1, 2, 3, 4, 5]
```

**Output:**
```
[1, 3, 2, N, N, 5, 4]
```

**Explanation:**

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700155/Web/Other/blobid1_1736926809.png"> </img>

In the inverted tree, every non-leaf node has its left and right child interchanged.

---

## 🧠 Approach

Use **postorder traversal** (left → right → root) to recursively swap the left and right children of each node.
1. Recursively call `mirror()` on the left and right subtrees.
2. Swap the left and right children of the current node.

---

## ⏱️ Time and Space Complexity

| Complexity | Value      | Description                              |
|------------|------------|------------------------------------------|
| Time       | O(n)       | Visit every node once                    |
| Space      | O(h)       | Recursion stack space (h = tree height)  |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10⁵`
- `1 ≤ node->data ≤ 10⁵`

---

## 💻 Code

```java
/* A Binary Tree node
class Node
{
    int data;
    Node left, right;
   Node(int item)
   {
        data = item;
        left = right = null;
    }
} */
class Solution {
    void mirror(Node node) {
        if(node == null){
            return;
        }
        mirror(node.left);
        mirror(node.right);
        Node temp = node.left;
        node.left = node.right;
        node.right = temp;
    }
}
```

---

> Made with ❤️ by Milan Haria
