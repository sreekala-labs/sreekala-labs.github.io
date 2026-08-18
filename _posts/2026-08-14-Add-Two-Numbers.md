---
title: "Add Two Numbers"
topic: Linked Lists
summary: "One query to fetch the list, N more because you looped over it."
---

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

 
```
Example 1:


Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]
Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

**Constraints:**

The number of nodes in each linked list is in the range [1, 100].
0 <= Node.val <= 9
It is guaranteed that the list represents a number that does not have leading zeros.


**Solution:**

Don't fall into the trap of converting Linked Lists to integers, add them and convert them back to a new Linked List. That was my initial thought. 
Best solution would be to do basic elementary school mathematics, where if you sum two numbers and if there is a carry, use it in the next set of numbers. This concept applies here for 
linked list as well.

```python
class Node:
   def __init__(self, data):
      self.data = data
      self.next = None

def addTwoNumbers(l1:Node, l2:Node)-> Node:
   # Create a dummy node to store it as Linked List and not touching the l1 and l2 lists.
   dummy=Node(0)
   current= dummy
   carry= 0 # This is to store the carry number.

   while l1 is not None or l2 is not None or carry!=0:
      val1= l1.data if l1 is not None else 0
      val2= l2.data if l2 is not None else 0

      sum= val1 + val2 + carry
      carry = sum // 10
      out_digit = sum % 10

      current.next = Node(out_digit)
      current = current.next

      if l1 is not None:
        l1 = l1.next
      if l2 is not None:
        l2 = l2.next

   return dummy.next 
```
