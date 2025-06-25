<h1 align="center">🔍 K-th Smallest in BST 🔍</h1>

---

## 📝 Problem Statement

Given a **Binary Search Tree (BST)** and an integer `k`, find the **k-th smallest element** in the BST.

- If the `k`-th smallest element does not exist, return `-1`.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
root = [2, 1, 3], k = 2
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700236/Web/Other/blobid1_1738413633.png"> </img>

**Output:**
```
2
```

**Explanation:**
In-order traversal = [1, 2, 3] → 2 is the 2nd smallest.

---

### ✅ Example 2:

**Input:**
```
root = [2, 1, 3], k = 5
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700236/Web/Other/blobid1_1738413633.png"> </img>

**Output:**
```
-1
```

**Explanation:**
There are only 3 nodes. So, 5th smallest does not exist.

---

### ✅ Example 3:

**Input:**
```
root = [20, 8, 22, 4, 12, N, N, N, N, 10, 14], k = 3
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700498/Web/Other/blobid1_1736918049.jpg"> </img>

**Output:**
```
10
```

**Explanation:**
In-order traversal = [4, 8, 10, 12, 14, 20, 22] → 10 is the 3rd smallest.

---

## 🧠 Approach

### Observation:
- **In-order traversal** of a BST gives sorted elements.
- Keep a counter while traversing.
- When the counter reaches `k`, record the element.

### Steps:
1. Perform **in-order traversal** recursively.
2. Keep a global counter `i` and result `ans`.
3. When `i == k`, store the current node value as `ans`.
4. Return `ans` or `-1` if not found.

---

## ⏱️ Time and Space Complexity

| Complexity | Value        | Description                               |
|------------|--------------|-------------------------------------------|
| Time       | O(k)         | In worst case, we traverse `k` nodes      |
| Space      | O(h)         | Stack space for recursion (h = height)    |

---

## 🎯 Constraints

- `1 ≤ number of nodes, k ≤ 10⁵`
- `1 ≤ node->data ≤ 10⁵`

---

## 💻 Code

```java
// class Node
// {
//     int data;
//     Node left, right;

//     public Node(int d)
//     {
//         data = d;
//         left = right = null;
//     }
// }

class Solution {
    public int ans;
    public int i;
    public void traverse(Node node, int k){
        if(node == null || i > k){
            return;
        }
        traverse(node.left, k);
        i++;
        if(i == k){
            ans = node.data;
            return;
        }
        traverse(node.right, k);
    }
    public int kthSmallest(Node root, int k) {
        ans = -1;
        i = 0;
        traverse(root, k);
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- We define two class-level variables:
  → ans = -1 (default return value)
  → i = 0 (to track current rank)

- traverse():
  → Perform in-order traversal (left → root → right)
  → Increment `i` when visiting a node
  → If `i == k`, store node value in `ans`

- kthSmallest():
  → Initialize `ans` and `i`
  → Start traversal from the root
  → Return the final result

---

> Made with ❤️ by Milan Haria
