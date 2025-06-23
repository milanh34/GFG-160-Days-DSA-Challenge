<h1 align="center">🧮 K Sum Paths 🧮</h1>

---

## 📝 Problem Statement

Given a binary tree and an integer `k`, find the number of **downward-only paths** where the **sum of node values** in the path equals `k`.

- A path can start and end at any node in the tree.
- The path must always go from **parent to child** (downward).

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
k = 7
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700575/Web/Other/blobid0_1738924888.webp"> </img>

**Output:**  
```
3
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700575/Web/Other/blobid0_1722330388.jpg"> </img>

There are 3 downward paths where the sum of values equals 7.

---

### ✅ Example 2:

**Input:**  
```
k = 3
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700575/Web/Other/blobid0_1739181818.jpg"> </img>

**Output:**  
```
2
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700575/Web/Other/blobid1_1739181850.jpg"> </img>

- Path 1: `1 → 2` (sum = 3)  
- Path 2: `3` (sum = 3)

---

## 🧠 Approach

### Key Observations:
- We need to track the sum of paths from root down to leaves.
- Use prefix sum technique to check how many subpaths sum to `k`.

### Steps:
1. Use a helper function `getPaths(node, k, map, sum)`:
   - `sum` keeps track of the running sum.
   - If `sum - k` exists in map, then there's a path ending at this node with sum `k`.
2. Use a map to store prefix sums and their frequencies.
3. Recurse through the tree and update the map accordingly.
4. Backtrack after each recursive call to maintain correct prefix sums.

---

## ⏱️ Time and Space Complexity

| Complexity | Value        | Description                                   |
|------------|--------------|-----------------------------------------------|
| Time       | O(n)         | Each node is visited once                     |
| Space      | O(h + n)     | h = recursion stack, n = prefix sum map       |

---

## 🎯 Constraints

- `1 ≤ number of nodes ≤ 10⁴`
- `-100 ≤ node value ≤ 100`
- `-10⁹ ≤ k ≤ 10⁹`

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
    public int getPaths(Node node, int k, Map<Integer, Integer> map, int sum){
        if(node == null){
            return 0;
        }
        sum += node.data;
        int paths = 0;
        if(sum == k){
            paths++;
        }
        paths += map.getOrDefault(sum - k, 0);
        map.put(sum, map.getOrDefault(sum, 0) + 1);
        paths += getPaths(node.left, k, map, sum);
        paths += getPaths(node.right, k, map, sum);
        map.put(sum, map.get(sum) - 1);
        return paths;
    }
    public int sumK(Node root, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        return getPaths(root, k, map, 0);
    }
}
```

---

## 📝 Explanation of Code

- sumK(root, k):
  Starts DFS traversal with an empty prefix sum map.

- getPaths(node, k, map, sum):
  → Increment the running sum.
  → If `sum == k`, increment path count.
  → Check `map.get(sum - k)` to find valid prefix sums.
  → Recur for left and right children.
  → Backtrack by decrementing current sum's frequency in map.

---

> Made with ❤️ by Milan Haria
