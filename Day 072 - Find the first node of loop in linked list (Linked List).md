<h1 align="center">🔁 Find the First Node of Loop in Linked List 🔁</h1>

---

## 📝 Problem Statement

You are given the **head of a singly linked list**. If a **loop** exists in the list, return the **first node of the loop**, otherwise return `null`.

**Custom Input Format:**  
- A linked list and a `pos` (1-based index) representing the node that the last node links back to.
- If `pos = 0`, the list has **no loop**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
head = 1 -> 3 -> 2 -> 4 -> 5
pos = 2
```

**Output:**  
```
3
```

**Explanation:**  

<img src ="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/713150/Web/Other/blobid0_1723112915.png"> </img>

The last node (5) links back to node 2 having the value 3, creating a loop starting at node 2.

---

### ✅ Example 2:

**Input:**  
```
head = 1 -> 3 -> 2 -> 1
pos = 0
```

**Output:**  
```
-1
```

**Explanation:**  

<img src = "https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/713150/Web/Other/blobid1_1723112944.png"> </img>

There is no loop in the list.

---

## 🧠 Approach

- Use a **HashSet** to store visited nodes.
- While traversing:
  - If a node's next is already in the set, it's the **start of the loop**.
  - If you reach `null`, there's **no loop**.

---

## ⏱️ Time and Space Complexity

| Complexity | Value       | Description                     |
|------------|-------------|---------------------------------|
| Time       | O(N)        | Traverse each node once         |
| Space      | O(N)        | To store visited nodes in set   |

---

## 🎯 Constraints

- 1 ≤ number of nodes ≤ 10⁶  
- 1 ≤ node->data ≤ 10⁶  

---

## 💻 Code

```java
/* class Node
{
    int data;
    Node next;

    Node(int x)
    {
        data = x;
        next = null;
    }
}*/

class Solution {
    public static Node findFirstNode(Node head) {
        Set<Node> set = new HashSet<>();
        while(head != null){
            set.add(head);
            if(head.next != null && set.contains(head.next)){
                return head.next;
            }
            head = head.next;
        }
        return null;
    }
}
```

---

> Made with ❤️ by Milan Haria
