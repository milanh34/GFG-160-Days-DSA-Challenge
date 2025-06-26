<h1 align="center">🌳 Pair Sum in BST 🌳</h1>

---

## 📝 Problem Statement

Given a **Binary Search Tree (BST)** and a **target value**, determine whether there exists a **pair of nodes** in the BST such that the **sum of their values equals the target**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**
```
root = [7, 3, 8, 2, 4, N, 9]
target = 12
```

**Output:**
```
True
```

**Explanation:**

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240821183540/bst.webp"> </img>

Nodes with values `4` and `8` exist, and `4 + 8 = 12`.

---

### ✅ Example 2:

**Input:**
```
root = [9, 5, 10, 2, 6, N, 12]
target = 23
```

**Output:**
```
False
```

**Explanation:**

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20240821184007/bst-3.webp"> </img>

No pair in the BST sums to 23.

---

## 🧠 Approach

### Strategy:
- We perform a **level-order traversal** of the BST.
- For each node:
  - We check if the **complement** (`target - current node value`) already exists in a set.
  - If yes, we return `true`.
  - Otherwise, we add the current value to the set and continue.

### Why this works:
- We only need one valid pair.
- Using a `HashSet` gives **O(1)** average time for lookup and insertion.

---

## ⏱️ Time and Space Complexity

| Complexity | Value     | Description                          |
|------------|-----------|--------------------------------------|
| Time       | O(n)      | Visit each node once                |
| Space      | O(n)      | For storing visited node values     |

---

## 🎯 Constraints

- `1 ≤ Number of Nodes ≤ 10⁵`
- `1 ≤ target ≤ 10⁶`

---

## 💻 Code

```java
/*
class Node {
    int data;
    Node left, right;

    public Node(int d) {
        data = d;
        left = right = null;
    }
}
*/
class Solution {
    Set<Integer> set;
    boolean findTarget(Node root, int target) {
        set = new HashSet<>();
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()){
            Node a = queue.poll();
            if(set.contains(target - a.data)){
                return true;
            }
            set.add(a.data);
            if(a.left != null){
                queue.offer(a.left);
            }
            if(a.right != null){
                queue.offer(a.right);
            }
        }
        return false;
    }
}
```

---

> Made with ❤️ by Milan Haria
