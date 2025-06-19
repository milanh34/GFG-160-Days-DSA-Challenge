<h1 align="center">🌳 Construct Tree from Inorder & Preorder 🌳</h1>

---

## 📝 Problem Statement

Given two arrays representing the **inorder** and **preorder** traversals of a binary tree, construct the original binary tree and return its **root node**.

> The final output must be in **postorder traversal** of the constructed tree.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
inorder = [1, 6, 8, 7]
preorder = [1, 6, 7, 8]
```

**Output:**
```
[8, 7, 6, 1]
```

**Explanation:**
The constructed binary tree will be:

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700586/Web/Other/blobid0_1738646717.png"> </img>

---

### ✅ Example 2:

**Input:**
```
inorder = [3, 1, 4, 0, 2, 5]
preorder = [0, 1, 3, 4, 2, 5]
```

**Output:**
```
[3, 4, 1, 5, 2, 0]
```

**Explanation:**
Constructed Tree:

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700586/Web/Other/blobid1_1738646749.png"> </img>

---

### ✅ Example 3:

**Input:**
```
inorder = [2, 5, 4, 1, 3]
preorder = [1, 2, 5, 4, 1, 3]
```

**Output:**
```
[2, 5, 4, 3, 1]
```

**Explanation:**
Constructed Tree:

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700586/Web/Other/blobid2_1738647091.png"> </img>

---

## 🧠 Approach

### Key Idea:
- In preorder: First element is always the **root**.
- In inorder: Left subtree values are on the **left of root**, and right subtree values on the **right**.

### Steps:
1. Find the **root** from preorder.
2. Locate root index in **inorder**.
3. Recursively:
   - Build left subtree using left part of inorder and next preorder elements.
   - Build right subtree using right part of inorder and corresponding preorder elements.

---

## ⏱️ Time and Space Complexity

| Complexity | Value     | Description                                  |
|------------|-----------|----------------------------------------------|
| Time       | O(n²)     | Due to linear search in inorder each time    |
| Space      | O(n)      | Recursive call stack                         |


---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10³`
- `0 ≤ node->data ≤ 10³`
- All values are **unique**

---

## 💻 Code

```java
/*
class Node {
    int data;
    Node left, right;

    Node(int key) {
        data = key;
        left = right = null;
    }
}
*/
class Solution {
    public static Node generateTree(int[] inorder, int[] preorder, int beg1, int end1, int beg2, int end2){
        if(end1 < beg1 || end2 < beg2){
            return null;
        }
        int rootVal = preorder[beg2], rootIdx = beg1;
        Node node = new Node(rootVal);
        while(rootIdx <= end1 && inorder[rootIdx] != rootVal){
            rootIdx++;
        }
        int sizeOfLeft = rootIdx - beg1;
        node.left = generateTree(inorder, preorder, beg1, rootIdx - 1, beg2 + 1, beg2 + sizeOfLeft);
        node.right = generateTree(inorder, preorder, rootIdx + 1, end1, beg2 + sizeOfLeft + 1, end2);
        return node;
    }
    public static Node buildTree(int inorder[], int preorder[]) {
        int n = inorder.length, rootVal = preorder[0];
        Node root = new Node(rootVal);
        int left = -1, right = -1;
        for(int i = 0; i < n; i++){
            if(inorder[i] == rootVal){
                left = i - 1;
                right = i + 1;
                break;
            }
        }
        root.left = generateTree(inorder, preorder, 0, left, 1, left + 1);
        root.right = generateTree(inorder, preorder, right, n - 1, left + 2, n - 1);
        return root;
    }
}
```

## 📝 Explanation of Code

- `buildTree()`:
  - Initializes the root using the first element in preorder.
  - Finds the left and right boundaries in inorder.
  - Calls `generateTree()` recursively to build the rest of the tree.

- `generateTree()`:
  - Recursively builds the subtree using preorder and inorder range boundaries.
  - The root of each subtree is always the first element in the current preorder segment.
  - The size of the left subtree determines how the ranges shift for recursive calls.

---

> Made with ❤️ by Milan Haria
