<h1 align="center">🔗 Merge K Sorted Linked Lists 🔗</h1>

---

## 📝 Problem Statement

Given an array `arr[]` of `n` sorted linked lists, merge them into a single sorted linked list and return the head of the merged list.

---

## ✅ Examples

### ✅ Example 1

**Input:**  
```
arr[] = [
  1 -> 2 -> 3,
  4 -> 5,
  5 -> 6,
  7 -> 8
]
```

**Output:**  
```
1 -> 2 -> 3 -> 4 -> 5 -> 5 -> 6 -> 7 -> 8
```

**Explanation:**  
The arr[] has 4 sorted linked list of size 3, 2, 2, 2.
- 1st list: 1 -> 2-> 3
- 2nd list: 4 -> 5
- 3rd list: 5 -> 6
- 4th list: 7 -> 8

The merged list will be:

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700265/Web/Other/blobid0_1737094930.png"> </img>

---

### ✅ Example 2

**Input:**  
```
arr[] = [
  1 -> 3,
  8,
  4 -> 5 -> 6
]
```

**Output:**  
```
1 -> 3 -> 4 -> 5 -> 6 -> 8
```

**Explanation:**  
The arr[] has 3 sorted linked list of size 2, 3, 1.
- 1st list: 1 -> 3
- 2nd list: 8
- 3rd list: 4 -> 5 -> 6

The merged list will be:

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700265/Web/Other/blobid1_1722513386.png"> </img>

---

## 🧠 Approach

- Use a **Min Heap** (`PriorityQueue`) to always get the smallest node among all current nodes.
- Initially, insert the head of each linked list into the priority queue.
- Repeatedly poll the smallest node and attach it to the result list.
- If the polled node has a next node, insert the next node into the heap.
- Continue until the heap is empty.

---

## ⏱️ Time and Space Complexity

| Complexity | Value              | Description                                      |
|------------|--------------------|--------------------------------------------------|
| Time       | O(N log K)         | `N` total nodes, `K` lists, heap operations     |
| Space      | O(K)               | Heap stores at most `K` nodes at any time       |

---

## 🎯 Constraints

- `1 ≤ total no. of nodes ≤ 10⁵`
- `1 ≤ node->data ≤ 10³`

---

## 💻 Java Code

```java
/*class Node
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
    Node mergeKLists(List<Node> arr) {
        PriorityQueue<Node> queue = new PriorityQueue<>((a, b) -> a.data - b.data);
        for(Node i: arr){
            queue.offer(i);
        }
        Node head = queue.poll();
        if(head.next != null){
            queue.offer(head.next);
        }
        Node prev = head;
        while(!queue.isEmpty()){
            Node a = queue.poll();
            prev.next = a;
            prev = prev.next;
            if(a.next != null){
                queue.offer(a.next);
            }
        }
        return head;
    }
}
```

---

> Made with ❤️ by Milan Haria
