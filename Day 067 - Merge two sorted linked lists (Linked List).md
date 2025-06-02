<h1 align="center">🔗 Merge Two Sorted Linked Lists 🔗</h1>

---

## 📝 Problem Statement

Given the **heads of two sorted linked lists**, merge them into a single sorted linked list and return the head of the merged list.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
head1 = 5 -> 10 -> 15 -> 40,
head2 = 2 -> 3 -> 20
```

**Output:**  
```
2 -> 3 -> 5 -> 10 -> 15 -> 20 -> 40
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700176/Web/Other/blobid1_1722768650.png"> </img>

---

### ✅ Example 2:

**Input:**  
```
head1 = 1 -> 1,
head2 = 2 -> 4
```

**Output:**  
```
1 -> 1 -> 2 -> 4
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700176/Web/Other/blobid3_1722768742.png"> </img>

---

## 🧠 Approach

1. Start by comparing the first nodes of both lists.
2. Use a `prev` pointer to build the new list by attaching the smaller of the current nodes.
3. Continue moving the pointer and updating the `prev` to the latest added node.
4. If any list ends first, attach the remaining part of the other list directly.

---

## ⏱️ Time and Space Complexity

| Complexity | Value  | Description                       |
|------------|--------|-----------------------------------|
| Time       | O(N+M) | Where N and M are list lengths    |
| Space      | O(1)   | Constant space, in-place merge    |

---

## 🎯 Constraints

- 1 ≤ number of nodes ≤ 10³  
- 0 ≤ node.data ≤ 10⁵  

---

## 💻 Code

```java
/*
  Node is defined as
    class Node
    {
        int data;
        Node next;
        Node(int d) {data = d; next = null; }
    }
*/

class Solution {
    Node sortedMerge(Node head1, Node head2) {
        Node prev;
        if(head1.data < head2.data){
            prev = head1;
            head1 = head1.next;
        } else{
            prev = head2;
            head2 = head2.next;
        }
        Node ans = prev;
        while(head1 != null && head2 != null){
            if(head1.data < head2.data){
                prev.next = head1;
                prev = head1;
                head1 = head1.next;
            } else{
                prev.next = head2;
                prev = head2;
                head2 = head2.next;
            }
        }
        while(head1 != null){
            prev.next = head1;
            prev = head1;
            head1 = head1.next;
        }
        while(head2 != null){
            prev.next = head2;
            prev = head2;
            head2 = head2.next;
        }
        return ans;
    }
}
```

---

## 📘 Explanation of Code

- The function first picks the smaller head and sets it as the start of the merged list (`ans`).
- It then traverses both lists, always appending the smaller node to the result list.
- After one list ends, the remainder of the other list is directly appended.

---

> Made with ❤️ by Milan Haria
