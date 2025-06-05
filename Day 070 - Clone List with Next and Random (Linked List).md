<h1 align="center">🔗 Clone List with Next and Random 🔗</h1>

---

## 📝 Problem Statement

You are given a special linked list with `n` nodes where each node has:

- a `next` pointer, which points to the next node in the list.
- a `random` pointer, which can point to **any node** in the list (including itself or `NULL`).

Your task is to **construct a deep copy** of this linked list. The new list should have:

- Exactly the same node values and structure.
- New `next` and `random` pointers that **do not reference** the original nodes.
- The original list must remain **unchanged**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
head = [[1, 3], [3, 3], [5, NULL], [9, 3]]
```

**Output:**  
```
[[1, 3], [3, 3], [5, NULL], [9, 3]]
```

**Explanation:**

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/885813/Web/Other/blobid2_1737541602.jpg"> </img>

- Node 1: next → Node 2, random → Node 3  
- Node 2: next → Node 3, random → Node 3  
- Node 3: next → Node 4, random → NULL  
- Node 4: next → NULL, random → Node 3  

---

### ✅ Example 2:

**Input:**  
```
head = [[1, 3], [2, 1], [3, 5], [4, 3], [5, 2]]
```

**Output:**  
```
[[1, 3], [2, 1], [3, 5], [4, 3], [5, 2]]
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700186/Web/Other/blobid2_1735042710.jpg"> </img>

The cloned list has identical next/random relationships as the original, but with all new node instances.

---

## 🧠 Approach

1. Use a **HashMap** to keep track of the mapping from original nodes to newly created nodes.
2. First pass:
   - Create new nodes and copy the `data` field.
   - Establish the `next` linkage.
   - Store the mapping between original and new nodes.
3. Second pass:
   - Use the mapping to assign the correct `random` pointers to new nodes.

---

## ⏱️ Time and Space Complexity

| Complexity | Value  | Description                    |
|------------|--------|--------------------------------|
| Time       | O(N)   | Each node is visited twice     |
| Space      | O(N)   | HashMap for node references    |

---

## 🎯 Constraints

- 1 ≤ n ≤ 100  
- 0 ≤ node->data ≤ 1000  

---

## 💻 Code

```java
/*linked list node
class Node {
    int data;
    Node next;
    Node random;

    Node(int x) {
        data = x;
        next = null;
        random = null;
    }
}
*/
class Solution {
    public Node cloneLinkedList(Node head) {
        Map<Node, Node> map = new HashMap<>();
        Node start = new Node(head.data);
        map.put(head, start);
        Node prev = start, curr = head;
        while(curr.next != null){
            curr = curr.next;
            Node newNode = new Node(curr.data);
            prev.next = newNode;
            prev = newNode;
            map.put(curr, newNode);
        }
        Node pointer = start;
        pointer.random = map.get(head.random);
        while(head.next != null){
            head = head.next;
            pointer = pointer.next;
            pointer.random = map.get(head.random);
        }
        return start;
    }
}
```

---

## 📝 Explanation of Code

- **Step 1**: Create new nodes with same values using a HashMap to map original → clone.
- **Step 2**: In a second pass, use the map to assign the `random` pointers.
- **Safety Check**: Return null if the head is null.
- **Final Result**: Return the cloned head node which is the deep copy of the original.

---

> Made with ❤️ by Milan Haria
