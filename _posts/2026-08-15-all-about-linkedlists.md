---
title: "All about Linked Lists"
topic: Linked Lists
summary: "Introduction, Advantages and Disadvantages of Linked Lists"
---


**Linked Lists**

Linked list is a data structure which unlike arrays does not contiguous memory, rather gets data via random access in the heap memory.

Linked Lists has 2 important information:

1. Data - Data of the node.
2. Next - Pointer to the next node.

In doubly linked list, there is a prev pointer which points to the previous node. 

Types of Linked Lists: 
  * Singly Linked List - It is one way with data and next pointer.
  * Doubly Linked List - You can traverse both ways - forward and backward.
  * Circulary Linked List - The tail points to the head. 


Complexity cheat sheet

| Operation | Array | Singly Linked List |
| :--------- | :----------: | ----------: |
| Access by index | O(1) |  O(n) |
| Search| 	O(n)	| O(n) | 
| Insert at head |	O(n) (shift)|	O(1)
| Insert at tail (no tail ptr)|	O(1) | amortized	O(n)
| Insert at tail (with tail ptr)| 	O(1)| amortized	O(1)
| Delete at head	| O(n) (shift)| 	O(1)
| Delete arbitrary node (given pointer)| 	O(n)| O(1) (singly: need prev; doubly: O(1) directly)

Advantages of Linked List:

1. Insertions and Deletion at the head are quicker with O(1) time complexity.
2. Grows or shrinks without resizing or reallocation overhead.
3. No wasted space by allocating exactly what is needed(node to node).
4. Efficient for implementing other structures such as stacks, queues, adjacency lists for graphs, LRU caches (doubly linked list + hashmap is the classic O(1) LRU pattern)

Disadvantages of Linked List: 

1. Access by index is O(n) unlike Array which is O(1).
2. Search in the linked list for a value is O(n).
3. Extra memory overhead since each node stores pointer(s) in addition to data (significant for small data types; a Node holding a single int in Python is far heavier than an int in an array-backed structure)
4. Poor cache locality where nodes are scattered across heap memory, so CPU cache misses hurt real-world performance even though Big-O looks favorable; arrays often beat linked lists in practice for medium-sized data due to this.
5. More complex pointer management such as off-by-one bugs, dangling pointers, and null-pointer errors are common failure modes.
6. Reverse traversal requires a doubly linked list (extra memory for prev pointers)

Practical Use Cases
1. LRU Cache — doubly linked list + hashmap gives O(1) get/put/evict; this is the textbook interview implementation (Redis, browser caches, OS page-replacement mimic this pattern)
2. Undo/Redo in editors — doubly linked list where each node is a state; back/forward navigation is O(1) pointer movement (browser history is a classic example)
3. Music/playlist "next/prev" navigation — circular doubly linked list
4. Memory allocators / free lists — OS and language runtimes track free memory blocks as a linked list to enable O(1) allocation/deallocation
5. Adjacency lists for graphs — each vertex holds a linked list of neighbors; standard for sparse graphs (more memory-efficient than adjacency matrices)
6. Implementing stacks/queues — collections.deque in Python is doubly-linked-list-backed and is the recommended way to get O(1) append/pop from both ends (better than list for queue-like use, where list.pop(0) is O(n))
7. Blockchain — conceptually a singly linked list where each block holds a hash pointer to the previous block
