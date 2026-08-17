---
title: "Linked Lists in Python"
topic: Linked Lists
summary: "Represenation of Linked List in Python"
---


Linked Lists is representated as a collection of Nodes. Each node is represented as a unique object storing the data of the elemnent and the pointer or reference to the next node. 

```python
class Node:
  def __init__(self, data):
    self.data= data
    self.next= None
```

Let's define a LinkedList Class which has the basic functions such as: 

1. Inserting an element at the head of a singly linked list.

```python
class LinkedList:
    def __init__(self):
       self.head=None

    def insert_at_beginning(self, data):
       new_node=Node(data)
       new_node.next= self.head
       self.head= new_node 

    def append(self, data):
       new_node = Node(data)
       if self.head is None:
          self.head=new_node
          return
       curr=self.head
       while curr:
         curr = curr.next
       curr.next = new_node

    def delete(self, key):
        curr= self.head
        prev = None
        while curr and curr.data!=key:
            prev= curr
            curr= curr.next
        if curr is None:
            return #Not found
        if prev is None:
           self.head= curr.next
        else:
           prev.next = curr.next

    def to_list(self):
        curr= self.head
        toList=[]
        while curr:
          toList.append(curr.data)
          curr = curr.next
        return toList 

```
