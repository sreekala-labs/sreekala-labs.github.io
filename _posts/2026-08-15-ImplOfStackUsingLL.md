---
title: "Impelmentation of stack using Linked Lists."
topic: Linked Lists
summary: "LIFO implementation using Singly Linked Lists."
---


**Implementing a stack using Singly Linked List**

In designing an implmentation of stack using Linked List, we need to decide whether to model the top of the stack at the head or at the tail of the list. 

We can efficiently insert and delete elements in constant time only at the head. Since all stack operations(push, pop, top) affect the top, we orient the top of the stack at the head of our list. 

To represent individual nodes of the list, we develop a lightweight _Node class. 

If you obeserve the below code class has "_" before the name of the class. This means that it is an internal protected class and cannot be used outside of the class.

```python
class _Node:
    def __init__(self, element, next):
        self._element= element
        self._next= next

class LinkedStack:
    """LIFO Stack Implementation using a singly linked list for storage"""

    # nested _Node class 
    class _Node:
        def __init__(self, element, next):
        self._element= element
        self._next= next

    def __init__(self):
      #Create an empty stack
      self._head= None #Reference to the head node.
      self._size =0    #Number of stack elements.

    #Returns the number of elements in the stack.
    def __len__(self):
        return self._size

    # Check if the stack is Empty.
    def is_empty(self):
        return self._size ==0

    # Push to the top of the list.
    def push(self, e):
        self._head = self._Node(e, self._head)
        self._size+=1

    # Get the top of the list but don't delete.
    def top(self):
        if self.is_empty():
          return Empty("Stack is empty")
        return self._head.element

    #Get the top of the list and delete. 
    def pop(self):
        if self.is_empty():
          return Empty('Stack is empty')
        answer = self._head._element
        self._head= self._head._next
        self._size -=1
        return answer 
    
```
    
