<h1 align="center">🔁 Reverse a Linked List 🔁</h1>

---

## 📝 Problem Statement

Given the **head** of a singly linked list, **reverse the list** and return the new head of the reversed list.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
head: 1 -> 2 -> 3 -> 4 -> NULL
```

**Output:**  
```
4 -> 3 -> 2 -> 1 -> NULL
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700005/Web/Other/blobid0_1736947674.png"> </img>

---

### ✅ Example 2:

**Input:**  
```
head: 2 -> 7 -> 10 -> 9 -> 8 -> NULL
```

**Output:**  
```
8 -> 9 -> 10 -> 7 -> 2 -> NULL
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700005/Web/Other/blobid1_1736947674.png"> </img>

---

### ✅ Example 3:

**Input:**  
```
head: 2 -> NULL
```

**Output:**  
```
2 -> NULL
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700005/Web/Other/blobid2_1736947674.png"> </img>

---

## 🧠 Approach

The recursive approach works as follows:

1. **Base Case:**  
   If the list has only one node, return it.

2. **Recursive Case:**  
   - Traverse the list recursively until reaching the last node.
   - While unwinding the recursion, reverse the `next` pointer of each node.

3. **Post-Traversal:**  
   - Set the `head.next` to `null` to terminate the reversed list.
   - Return the last node as the new head.

---

## ⏱️ Time and Space Complexity

| Complexity | Value      | Description                        |
|------------|------------|------------------------------------|
| Time       | O(N)       | Traverse each node once            |
| Space      | O(N)       | Recursion stack for N nodes        |

---

## 🎯 Constraints

- 1 ≤ number of nodes ≤ 10⁵  
- 1 ≤ data of nodes ≤ 10⁵  

---

## 💻 Code

```java
/* linked list node class:

class Node {
    int data;
    Node next;
    Node(int value) {
        this.value = value;
    }
}

*/

class Solution {
    Node last;
    public void traverse(Node node1, Node node2){
        if(node2 == null){
            last = node1;
            return;
        }
        traverse(node2, node2.next);
        node2.next = node1;
    }
    Node reverseList(Node head) {
        if(head.next == null){
            return head;
        }
        traverse(head, head.next);
        head.next = null;
        return last;
    }
}
```

---

## 📝 Explanation of Code

- **`traverse(node1, node2)`** is a recursive helper function:
  - It recursively goes to the end of the list.
  - On returning, it sets `node2.next = node1` to reverse the link.

- **`last`** stores the new head of the reversed list (last node before reversal).

- The main function `reverseList(head)` checks if the list has only one node. If not, it calls `traverse`.

- After recursion, the original head is made to point to `null`, making it the last node in the reversed list.

---

> Made with ❤️ by Milan Haria
