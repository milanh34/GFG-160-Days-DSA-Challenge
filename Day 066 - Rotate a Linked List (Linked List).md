<h1 align="center">🔄 Rotate a Linked List 🔄</h1>

---

## 📝 Problem Statement

Given the **head of a singly linked list**, the task is to **left rotate** the linked list **k times**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
head = 10 -> 20 -> 30 -> 40 -> 50, k = 4
```

**Output:**  
```
50 -> 10 -> 20 -> 30 -> 40
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/885669/Web/Other/blobid0_1737098802.webp"> </img>

- Rotate 1: 20 → 30 → 40 → 50 → 10  
- Rotate 2: 30 → 40 → 50 → 10 → 20  
- Rotate 3: 40 → 50 → 10 → 20 → 30  
- Rotate 4: 50 → 10 → 20 → 30 → 40 

---

### ✅ Example 2:

**Input:**  
```
head = 10 -> 20 -> 30 -> 40, k = 6
```

**Output:**  
```
30 -> 40 -> 10 -> 20
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/885669/Web/Other/blobid3_1737099041.webp"> </img>

- 6 % 4 = 2  
- Rotate 1: 20 → 30 → 40 → 10  
- Rotate 2: 30 → 40 → 10 → 20  

---

## 🧠 Approach

1. **Calculate the length** `n` of the linked list and store the **last node**.
2. Compute the **effective rotations** as `k % n`. If 0, return head as-is.
3. Move to the node **just before** the new head (i.e., after `k` rotations).
4. Set `last.next = head` to create a circular list.
5. Set the **new head** and break the circle by setting `node.next = null`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value     | Description                       |
|------------|-----------|-----------------------------------|
| Time       | O(N)      | One traversal to get length + 1   |
| Space      | O(1)      | No extra space used               |

---

## 🎯 Constraints

- 1 ≤ number of nodes ≤ 10⁵  
- 0 ≤ k ≤ 10⁹  
- 0 ≤ data of node ≤ 10⁹  

---

## 💻 Code

```java
/* node of linked list:

class Node{
    int data;
    Node next;
    Node(int d){
        data=d;
        next=null;
    }
}

*/

class Solution {
    public Node last;
    public int n;
    public void traverse(Node node){
        if(node.next == null){
            last = node;
            return;
        }
        n++;
        traverse(node.next);
    }
    public Node rotate(Node head, int k) {
        n = 1;
        traverse(head);
        int end = k % n;
        if(end == 0){
            return head;
        }
        Node node = head;
        for(int i = 1; i < end; i++){
            node = node.next;
        }
        last.next = head;
        Node ans = node.next;
        node.next = null;
        return ans;
    }
}
```

---

## 📝 Explanation of Code

- The `traverse` method finds:
  - `n` — the total number of nodes.
  - `last` — the last node of the list.
- `rotate` method:
  - Computes effective rotations using modulo.
  - Finds the node at position `k % n`.
  - Connects `last` to `head` to make the list circular.
  - Cuts the link at the correct spot to return the rotated list.

---

> Made with ❤️ by Milan Haria
