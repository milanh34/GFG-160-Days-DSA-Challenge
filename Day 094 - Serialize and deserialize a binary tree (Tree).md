<h1 align="center">🔗 Serialize and Deserialize a Binary Tree 🔗</h1>

---

## 📝 Problem Statement

**Serialization** is converting a binary tree to an array so it can be stored or transmitted.  
**Deserialization** is reconstructing the original tree from that array.

You must:
- Implement `serialize()` to store the tree in a list.
- Implement `deSerialize()` to rebuild the tree from the list.

**Note:** Node values are always positive integers.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
root = [1, 2, 3]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700281/Web/Other/blobid4_1739345069.png"> </img>

**Output:** (Inorder after deSerialize(serialize(root))):
```
[2, 1, 3]
```

---

### ✅ Example 2

**Input:**  
```
root = [10, 20, 30, 40, 60, N, N]
```

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700281/Web/Other/blobid5_1739345069.png"> </img>

**Output:** (Inorder after deSerialize(serialize(root)))
```
[40, 20, 60, 10, 30]
```

---

## 🧠 Approach

### Serialization
- Do a **level-order traversal**.
- For each node, store its value.
- For `null` children, store `0` as a marker.

###  Deserialization
- Use a queue:
  - Build the tree level by level.
  - Read values from the array.
  - For `0`, leave child as `null`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value | Description |
|------------|-------|--------------|
| Time       | O(n)  | Visit each node once |
| Space      | O(n)  | Store all nodes in array and queue |

---

## 🎯 Constraints

- `1 ≤ Number of nodes ≤ 10⁴`
- `1 ≤ Node data ≤ 10⁹`

---

## 💻 Code

```java
/*
Node is as follows:
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

class Tree {
    public ArrayList<Integer> serialize(Node root) {
        ArrayList<Integer> list = new ArrayList<>();
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()){
            Node a = queue.poll();
            if(a != null){
                list.add(a.data);
                queue.offer(a.left);
                queue.offer(a.right);
            } else{
                list.add(0);
            }
        }
        return list;
    }

    public Node deSerialize(ArrayList<Integer> arr) {
        int n = arr.size(), i = 0;
        Node root = new Node(arr.get(i));
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        i++;
        while(i < n && !queue.isEmpty()){
            Node a = queue.poll();
            int left = arr.get(i);
            i++;
            if(left != 0){
                a.left = new Node(left);
                queue.offer(a.left);
            }
            if(i < n){
                int right = arr.get(i);
                i++;
                if(right != 0){
                    a.right = new Node(right);
                    queue.offer(a.right);
                }
            }
        }
        return root;
    }
};
```

---

## 📝 Explanation of Code


### serialize():
   - Uses a queue for BFS.
   - Adds node value if not null, else adds 0.
   - Adds left and right children to queue.

### deSerialize():
   - Uses a queue to build tree level-by-level.
   - Reads next value for left and right.
   - If value is non-zero, creates child node and adds to queue.


---

> Made with ❤️ by Milan Haria
