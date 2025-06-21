<h1 align="center">🌳 Tree Boundary Traversal 🌳</h1>

---

## 📝 Problem Statement

Given a **Binary Tree**, your task is to print its **Boundary Traversal** in the following order:

1. **Left Boundary** (excluding leaves)
2. **All Leaf Nodes** (from left to right)
3. **Reverse Right Boundary** (excluding leaves and root)

> If the root does not have a left or right subtree, then it is considered part of the boundary.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
root = [1, 2, 3, 4, 5, 6, 7, N, N, 8, 9, N, N, N, N]
```

**Output:**  
```
[1, 2, 4, 8, 9, 6, 7, 3]
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700204/Web/Other/blobid6_1749213679.webp"> </img>

- Left Boundary: 1 → 2 → 4  
- Leaf Nodes: 8, 9, 6, 7  
- Right Boundary (reversed): 3  

---

### ✅ Example 2:

**Input:**  
```
root = [1, 2, N, 4, 9, 6, 5, N, 3, N, N, N, N, 7, 8]
```

**Output:**  
```
[1, 2, 4, 6, 5, 7, 8]
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700204/Web/Other/blobid2_1749213505.webp"> </img>

- Root has no right subtree, so no right boundary.
- Leaves are 6, 5, 7, 8.

---

### ✅ Example 3:

**Input:**  
```
root = [1, N, 2, N, 3, N, 4, N, N]
```

**Output:**  
```
[1, 4, 3, 2]
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700204/Web/Other/blobid3_1749213560.webp"> </img>

- Left Boundary: only root = 1  
- Leaf: 4  
- Right Boundary (reversed): 3 → 2

---

## 🧠 Approach

1. **Left Boundary Traversal (`goLeft`)**
   - Keep going left.
   - If no left, try right.
   - Exclude leaves.

2. **Leaf Node Collection (`traverse`)**
   - Inorder traversal to pick all leaves.

3. **Right Boundary Traversal (`goRight`)**
   - Keep going right.
   - If no right, try left.
   - Exclude leaves.
   - **Add nodes after recursive calls** for reverse order.

---

## ⏱️ Time and Space Complexity

| Complexity | Value        | Description                         |
|------------|--------------|-------------------------------------|
| Time       | O(n)         | Each node is visited once           |
| Space      | O(h)         | Recursion stack for tree height `h` |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10⁵`
- `1 ≤ node->data ≤ 10⁵`

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
    ArrayList<Integer> ans;
    void traverse(Node node){
        if(node == null){
            return;
        }
        if(node.left == null && node.right == null){
            ans.add(node.data);
            return;
        }
        traverse(node.left);
        traverse(node.right);
    }
    void goLeft(Node node){
        if(node.left == null){
            if(node.right == null){
                return;
            }
            ans.add(node.data);
            goLeft(node.right);
        } else{
            ans.add(node.data);
            goLeft(node.left);
        }
    }
    void goRight(Node node){
        if(node.right == null){
            if(node.left == null){
                return;
            }
            goRight(node.left);
        } else{
            goRight(node.right);
        }
        ans.add(node.data);
    }
    ArrayList<Integer> boundaryTraversal(Node node) {
        ans = new ArrayList<>();
        ans.add(node.data);
        if(node.left != null){
            goLeft(node.left);
        }
        traverse(node.left);
        traverse(node.right);
        if(node.right != null){
            goRight(node.right);
        }
        return ans;
    }
}
```

---

## 📝 Explanation of Code

1. **boundaryTraversal**():
   - Starts with adding root node.
   - Calls goLeft() to collect left boundary (excluding leaves).
   - Calls traverse() to collect all leaf nodes in DFS manner.
   - Calls goRight() to collect right boundary in reverse order.

2. **goLeft(node)**:
   - Adds non-leaf nodes from the left side preferring left child.
   - Skips leaves.

3. **traverse(node)**:
   - Simple DFS that adds nodes that are leaves.

4. **goRight(node)**:
   - Recursively moves down right (preferring right child).
   - Skips leaves.
   - Adds nodes **after** recursion to get reverse order.

---

> Made with ❤️ by Milan Haria
