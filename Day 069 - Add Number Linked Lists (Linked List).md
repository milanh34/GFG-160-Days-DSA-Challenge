<h1 align="center">➕ Add Number Linked Lists ➕</h1>

---

## 📝 Problem Statement

Given the **head of two singly linked lists** `num1` and `num2` representing two non-negative integers, return the **head of a new linked list** representing their sum.

- The digits are stored in forward order (i.e., most significant digit first).
- The resulting linked list should **not have leading zeros**.

---

## ✅ Examples

### ✅ Example 1:

**Input:**  
```
num1 = 4 -> 5  
num2 = 3 -> 4 -> 5
```

**Output:**  
```
3 -> 9 -> 0
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700043/Web/Other/blobid1_1721847725.png"> </img>

The numbers are 45 and 345.  
Their sum = 390, so the resulting list is 3 -> 9 -> 0.

---

### ✅ Example 2:

**Input:**  
```
num1 = 0 -> 0 -> 6 -> 3  
num2 = 0 -> 7
```

**Output:**  
```
7 -> 0
```

**Explanation:**  

<img src="https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700043/Web/Other/blobid2_1721847773.png"> </img>

The numbers are 63 and 7.  
Their sum = 70, so the resulting list is 7 -> 0.

---

## 🧠 Approach

1. **Reverse** both input linked lists to facilitate addition from least significant digit.
2. Traverse both lists:
   - Add corresponding digits and carry.
   - Store result as a new node in a new list.
3. **Reverse** the resulting list to restore forward order.
4. **Remove leading zeros** from the result, if any.

---

## ⏱️ Time and Space Complexity

| Complexity | Value    | Description               |
|------------|----------|---------------------------|
| Time       | O(N + M) | Where N and M are sizes of the input lists |
| Space      | O(1)     | In-place list manipulations |

---

## 🎯 Constraints

- 1 ≤ size of both linked lists ≤ 10⁶  
- 0 ≤ elements of both linked lists ≤ 9  

---

## 💻 Code

```java
/* node for linked list

class Node {
    int data;
    Node next;

    Node(int d) {
        data = d;
        next = null;
    }
}

*/

class Solution {
    static Node reverse(Node node){
        Node prev = null, curr = node;
        while(curr != null){
            Node next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
    static Node addTwoLists(Node num1, Node num2) {
        num1 = reverse(num1);
        num2 = reverse(num2);
        int carry = 0;
        Node temp = new Node(0);
        Node end = temp;
        while(num1 != null || num2 != null || carry != 0){
            int sum = carry;
            if(num1 != null){
                sum += num1.data;
                num1 = num1.next;
            }
            if(num2 != null){
                sum += num2.data;
                num2 = num2.next;
            }
            carry = sum / 10;
            end.next = new Node(sum % 10);
            end = end.next;
        }
        Node ans = reverse(temp.next);
        while(ans != null && ans.data == 0 && ans.next != null){
            ans = ans.next;
        }
        return ans; 
    }
}
```

---

## 📝 Explanation of Code

- **reverse()**: Helper function to reverse a linked list.
- **Initial Reversal**: Input numbers are reversed to make addition easier (least significant digit first).
- **Addition Loop**:
  - Digit-by-digit addition is performed with carry.
  - New nodes are added to a temporary result list.
- **Final Reverse**: The resulting list is reversed back to forward order.
- **Leading Zero Removal**: Any unnecessary leading zeros are skipped before returning the result.

---

> Made with ❤️ by Milan Haria
