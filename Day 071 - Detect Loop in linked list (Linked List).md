<h1 align="center">🔁 Detect Loop in Linked List 🔁</h1>

---

## 📝 Problem Statement

You are given the **head of a singly linked list**. Your task is to determine **whether a loop exists** in the linked list.

A loop exists if any node's `next` pointer **points to an earlier node** in the list (including itself), instead of `null`.

You are also given a custom input format:
- `pos` (1-based index): the position to which the **last node** points.
- If `pos = 0`, the last node points to `null`, indicating no loop.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
head = 1 -> 3 -> 4, pos = 2
```

**Output:**  
```
true
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700099/Web/Other/blobid1_1718699705.png"> </img>

The last node (4) points to the second node (3), forming a loop.

---

### ✅ Example 2:

**Input:**  
```
head = 1 -> 8 -> 3 -> 4, pos = 0
```

**Output:**  
```
false
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700099/Web/Other/blobid2_1718699755.png"> </img>

There is no loop since the last node points to `null`.

---

### ✅ Example 3:

**Input:**  
```
head = 1 -> 2 -> 3 -> 4, pos = 1
```

**Output:**  
```
true
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700332/Web/Other/blobid2_1718609744.png"> </img>

The last node (4) points back to the first node (1), forming a loop.

---

## 🧠 Approach

1. Use a **HashSet** to keep track of visited nodes.
2. Traverse the linked list node by node.
3. If a node's `next` already exists in the set, then a loop exists.
4. If you reach the end (`null`), no loop is present.

---

## ⏱️ Time and Space Complexity

| Complexity | Value       | Description                |
|------------|-------------|----------------------------|
| Time       | O(N)        | Traverse each node once    |
| Space      | O(N)        | For storing visited nodes  |


---

## 🎯 Constraints

- 1 ≤ number of nodes ≤ 10⁴  
- 1 ≤ node->data ≤ 10³  
- 0 ≤ pos ≤ Number of nodes in Linked List  

---

## 💻 Code

```java
/* Node is defined as

class Node
{
    int data;
    Node next;
    Node(int d) {data = d; next = null; }
}

*/

class Solution {
    // Function to check if the linked list has a loop.
    public static boolean detectLoop(Node head) {
        Set<Node> set = new HashSet<>();
        while(head != null){
            set.add(head);
            if(head.next != null && set.contains(head.next)){
                return true;
            }
            head = head.next;
        }
        return false;
    }
}
```

---

## 📝 Explanation of Code

- We maintain a set to store references of visited nodes.
- If a node is **already present in the set**, it means a cycle is formed.
- Otherwise, we continue traversing.
- If we reach `null`, we confirm there’s **no loop**.

---

> Made with ❤️ by Milan Haria
