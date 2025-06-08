<h1 align="center">🧹 Remove Loop in Linked List 🧹</h1>

---

## 📝 Problem Statement

Given the **head of a singly linked list** that may contain a **loop**, your task is to **remove the loop** (if present) such that the linked list becomes linear. If there is no loop, the list remains unchanged.

**Custom Input Format:**  
A linked list and a `pos` (1-based index) which indicates the node the last node connects to.  
If `pos = 0`, the list ends normally with no loop.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
head = 1 -> 3 -> 4
pos = 2
```

**Output:**  
```
true
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700332/Web/Other/blobid0_1718609709.png"> </img>

A loop was present (node 4 linked back to node 3). It is now removed.

---

### ✅ Example 2:

**Input:**  
```
head = 1 -> 8 -> 3 -> 4
pos = 0
```

**Output:**  
```
true
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700332/Web/Other/blobid0_1718609876.png"> </img>

No loop exists. List remains unchanged.

---

### ✅ Example 3:

**Input:**  
```
head = 1 -> 2 -> 3 -> 4
pos = 1
```

**Output:**  
```
true
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700332/Web/Other/blobid2_1718609744.png"> </img>

A loop was present (node 4 linked back to node 1). The loop is removed successfully.

---

## 🧠 Approach

1. Traverse the list and maintain a `HashSet` of visited nodes.
2. If the next node of a current node already exists in the set, it means a loop is present.
3. Break the loop by setting `current.next = null`.

---

## ⏱️ Time and Space Complexity

| Complexity | Value       | Description                        |
|------------|-------------|------------------------------------|
| Time       | O(N)        | Traverse each node once            |
| Space      | O(N)        | Set stores references to each node |

---

## 🎯 Constraints

- 1 ≤ size of linked list ≤ 10⁵

---

## 💻 Code

```java
/*
class Node
{
    int data;
    Node next;
}
*/

class Solution {
    public static void removeLoop(Node head) {
        Set<Node> set = new HashSet<>();
        while(head != null){
            set.add(head);
            if(head.next != null && set.contains(head.next)){
                head.next = null;
                return;
            }
            head = head.next;
        }
    }
}
```

---

> Made with ❤️ by Milan Haria
