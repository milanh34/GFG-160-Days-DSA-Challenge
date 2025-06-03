<h1 align="center">🔁 Linked List Group Reverse 🔁</h1>

---

## 📝 Problem Statement

Given the **head of a linked list**, reverse every group of **k nodes** in the list. If the number of nodes is not a multiple of k, the remaining nodes at the end are still reversed as a group.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
head = 1 -> 2 -> 2 -> 4 -> 5 -> 6 -> 7 -> 8, k = 4
```

**Output:**  
```
4 -> 2 -> 2 -> 1 -> 8 -> 7 -> 6 -> 5
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700013/Web/Other/blobid0_1723298986.png"> </img>

The first 4 elements 1, 2, 2, 4 are reversed first and then the next 4 elements 5, 6, 7, 8. Hence, the resultant linked list is
4 -> 2 -> 2 -> 1 -> 8 -> 7 -> 6 -> 5.

---

### ✅ Example 2:

**Input:**  
```
head = 1 -> 2 -> 3 -> 4 -> 5, k = 3
```

**Output:**  
```
3 -> 2 -> 1 -> 5 -> 4
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700013/Web/Other/blobid1_1723298995.png"> </img>

The first 3 elements 1, 2, 3 are reversed first and then left out elements 4, 5 are reversed. Hence, the resultant linked list is 3 -> 2 -> 1 -> 5 -> 4.

---

## 🧠 Approach

1. Traverse the list in chunks of `k` nodes.
2. Reverse each chunk in place.
3. Keep track of the beginning of the final answer list and the end of the previous reversed group to link it correctly.
4. Continue the process until all nodes are reversed in their respective groups.

---

## ⏱️ Time and Space Complexity

| Complexity | Value  | Description               |
|------------|--------|---------------------------|
| Time       | O(N)   | Every node visited once   |
| Space      | O(1)   | In-place reversal         |

---

## 🎯 Constraints

- 1 ≤ size of linked list ≤ 10⁵  
- 1 ≤ data of nodes ≤ 10⁶  
- 1 ≤ k ≤ size of linked list  

---

## 💻 Code

```java
/*node class of the linked list
class Node
{
    int data;
    Node next;
    Node(int key)
    {
        data = key;
        next = null;
    }
}

*/

class Solution {
    public static Node reverseKGroup(Node head, int k) {
        if(k == 1){
            return head;
        }
        Node current = head, beg = null, end = null;
        while(current != null){
            int i = 0;
            Node prev = null, curr = current;
            while(current != null && i < k){
                Node next = current.next;
                current.next = prev;
                prev = current;
                current = next;
                i++;
            }
            if(beg == null){
                beg = prev;
            }
            if(end != null){
                end.next = prev;
            }
            end = curr;
        }
        return beg;
    }
}
```

---

## 📝 Explanation of Code

- **Initial Check:** If `k == 1`, no need to reverse, return original head.
- **Outer Loop:** Processes list in chunks of size `k`.
- **Inner Loop:** Reverses current group of `k` nodes.
- **Linking:** 
  - `beg` holds the head of the new list after first reversal.
  - `end` tracks the last node of the previously reversed group to connect it with the new one.
- **Return:** Returns `beg` which is the new head of the fully reversed list.

---

> Made with ❤️ by Milan Haria
