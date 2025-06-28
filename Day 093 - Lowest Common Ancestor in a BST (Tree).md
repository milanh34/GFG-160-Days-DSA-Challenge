<h1 align="center">🌳 Lowest Common Ancestor in a BST 🌳</h1>

---

## 📝 Problem Statement

Given a **Binary Search Tree** (BST) with **unique values** and **two nodes `n1` and `n2`** (`n1 != n2`), find their **Lowest Common Ancestor (LCA)**.  
You can assume **both nodes exist** in the tree.

**Definition:**  
The **LCA** between `n1` and `n2` is the **lowest node** in the BST that has **both `n1` and `n2` as descendants** (a node can be a descendant of itself).

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
root = [5, 4, 6, 3, N, N, 7, N, N, N, 8], n1 = 7, n2 = 8
```

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700236/Web/Other/blobid0_1738413634.png"> </img>

**Output:**  
```
7
```

**Explanation:**  
- The LCA for nodes `7` and `8` is `7`.

---

### ✅ Example 2

**Input:**  
```
root = [20, 8, 22, 4, 12, N, N, N, N, 10, 14], n1 = 8, n2 = 14
```

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700236/Web/Other/blobid1_1739265251.png"> </img>

**Output:**  
```
8
```

**Explanation:**  
- The LCA for nodes `8` and `14` is `8`.

---

### ✅ Example 3

**Input:**  
```
root = [2, 1, 3], n1 = 1, n2 = 3
```

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700236/Web/Other/blobid1_1738413633.png"> </img>

**Output:**  
```
2
```

**Explanation:**  
- The LCA for nodes `1` and `3` is `2`.

---

## 🧠 Approach

### Observation:
- The simplest way is to **trace paths** from the **root** to both nodes.
- The **last common node** in both paths is the LCA.

### Steps:
1. **Traverse the tree** from the root to find the path to `n1` and `n2`.
2. Store each path in a list.
3. **Compare paths** from the root: The last common node in both paths is the LCA.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description |
|------------|-------|--------------|
| Time       | O(n)  | Visiting each node for both paths |
| Space      | O(h)  | Stack space for recursion (h = height) + Lists for paths |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10⁵`
- `1 ≤ node->data ≤ 10⁵`
- `1 ≤ n1, n2 ≤ 10⁵`

---

## 💻 Code

```java
/*
class Node
{
    int data;
    Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}
*/

class Solution {
    boolean traverse(Node node, Node n, List<Node> list){
        if(node == null){
            return false;
        }
        if(node == n){
            list.add(node);
            return true;
        }
        if(traverse(node.left, n, list)){
            list.add(node);
            return true;
        }
        if(traverse(node.right, n, list)){
            list.add(node);
            return true;
        }
        return false;
    }
    Node LCA(Node root, Node n1, Node n2) {
        List<Node> list1 = new ArrayList<>(), list2 = new ArrayList<>();
        traverse(root, n1, list1);
        traverse(root, n2, list2);
        Node ans = root;
        int l1 = list1.size() - 1, l2 = list2.size() - 1;
        while(l1 >= 0 && l2 >= 0){
            if(list1.get(l1) == list2.get(l2)){
                ans = list1.get(l1);
            } else{
                break;
            }
            l1--;
            l2--;
        }
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
