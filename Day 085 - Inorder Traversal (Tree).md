<h1 align="center">🌿 Inorder Traversal 🌿</h1>

---

## 📝 Problem Statement

Given a **Binary Tree**, return its **inorder traversal**.

In an inorder traversal:
- Visit the **left** subtree.
- Visit the **current node**.
- Visit the **right** subtree.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
root = [1, 2, 3, 4, 5]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886461/Web/Other/blobid0_1738561309.png"> </img>

**Output:**  
```
[4, 2, 5, 1, 3]
```

**Explanation:**  
Inorder traversal:
- Traverse left of 1 → 2
- Traverse left of 2 → 4 → add
- Go to 2 → add
- Traverse right of 2 → 5 → add
- Go to 1 → add
- Right of 1 → 3 → add

---

### ✅ Example 2:

**Input:**  
```
root = [8, 1, 5, N, 7, 10, 6, N, 10, 6]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/886461/Web/Other/blobid1_1738561309.png"> </img>

**Output:**  
```
[1, 7, 10, 8, 6, 10, 5, 6]
```

**Explanation:**  
Inorder traversal visits all left nodes, then root, then right.

---

## 🧠 Approach

### Recursive Approach:

1. Traverse the **left subtree** recursively.
2. Add the **current node** to the result.
3. Traverse the **right subtree** recursively.

This uses implicit stack space from recursion.

---

## ⏱️ Time and Space Complexity

| Complexity | Value         | Description                         |
|------------|---------------|-------------------------------------|
| Time       | O(n)          | Visits each node exactly once       |
| Space      | O(h)          | Call stack in recursion (h = height of tree) |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10⁵`
- `0 ≤ node->data ≤ 10⁵`

---

## 💻 Code

```java
/* A Binary Tree node
class Node {
    int data;
    Node left, right;
   Node(int item)    {
        data = item;
        left = right = null;
    }
}
*/
class Solution {
    ArrayList<Integer> ans;
    void traverse(Node node){
        if(node != null){
            traverse(node.left);
            ans.add(node.data);
            traverse(node.right);
        }
    }
    ArrayList<Integer> inOrder(Node root) {
        ans = new ArrayList<>();
        traverse(root);
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
