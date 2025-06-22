<h1 align="center">🌟 Maximum Path Sum from Any Node 🌟</h1>

---

## 📝 Problem Statement

Given a binary tree, your task is to **find the maximum path sum**. The path **may start and end at any node** in the tree.

- The path must contain at least one node.
- Nodes in the path must be connected via parent-child connections.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
root = [10, 2, 10, 20, 1, N, -25, N, N, N, N, 3, 4]
```

**Output:**  
```
42
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700611/Web/Other/blobid3_1736948585.png"> </img>

Maximum path is: `20 → 2 → 10 → 10`  
Sum = `20 + 2 + 10 + 10 = 42`

---

### ✅ Example 2:

**Input:**  
```
root = [-17, 11, 4, 20, -2, 10]
```

**Output:**  
```
31
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700611/Web/Other/blobid1_1736947534.png"> </img>

Maximum path is: `20 → 11 → -17 → 4 → 10`  
Sum = `20 + 11 + (-17) + 4 + 10 = 28`,  
but since `-17` drops the sum, best path is: `20 → 11` and `4 → 10` separately. Final: `20 + 11 = 31`

---

## 🧠 Approach

### Key Observations:
- A path can start and end anywhere.
- The path must pass through parent-child connected nodes.
- We must explore both left and right subtrees to decide if including both in the path is better.

### Algorithm Steps:
1. Perform post-order traversal using `traverse(node)`.
2. For each node:
   - Calculate max path sum from left and right.
   - Ignore negative sums using `Math.max(0, value)`.
   - Update global max `ans` with: `left + right + node.data`.
3. Return the global `ans` as final result.

---

## ⏱️ Time and Space Complexity

| Complexity | Value        | Description                          |
|------------|--------------|--------------------------------------|
| Time       | O(n)         | Each node visited once               |
| Space      | O(h)         | Stack space for recursion (h = height) |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10³`
- `-10⁴ ≤ node->data ≤ 10⁴`

---

## 💻 Code

```java
/*
Node defined as
class Node{
    int data;
    Node left,right;
    Node(int d){
        data=d;
        left=right=null;
    }
}
*/
class Solution {
    int ans;
    int traverse(Node node){
        if(node == null){
            return 0;
        }
        int left = Math.max(0, traverse(node.left));
        int right = Math.max(0, traverse(node.right));
        ans = Math.max(ans, left + right + node.data);
        return Math.max(left, right) + node.data;
    }
    int findMaxSum(Node node) {
        ans = node.data;
        traverse(node);
        return ans;
    }
}
```

---

> Made with ❤️ by Milan Haria
