## Singly Linked list
## 1. Motivation: 
- Problem:
    - Insertion & Deletion
- Idea:
    - Use pointers and values for operations, O(1) for insertion, deletion.
- Result:
    - One of the two basic strategy for all others data structures. 
        - The other one is [array](../../2_Containers/array/array.md).
- Limit:
    - only one direction

## 2. Pros. & Cons.
- Pros: 
    - O(1) for Insertion, Deletion.
- Cons:
    - O(n) for Access.
    - Fast random access is not supported. 

## 3. When to use:
- Applications when Insertion & Deletion dominate.
- Algorithms:    
    - fast-slow pointers: 
        - Find the middle node.
        - Cycle detection
        - Given linked list with cycle, find start position.
        - Find last k elements.
    


## 4. Implementation
- Just linked list.

## 5. Alternatives
- When insertion & deletion dominates, alternatives are listed as follow.
- Compared to [Doubly-Linked List](4_10_DoublyLinkedList.md) this data structure provides **more space efficient storage** when **bidirectional iteration** is not needed.


Structure |**Time**| | | | | | | |**Space**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
 ||Average| | | |Worst| | | |Worst
 ||Access|Search|Insertion|Deletion|Access|Search|Insertion|Deletion|-
[Stack](../ch3_StackAndQueue/3_2_Stack.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Queue](../ch3_StackAndQueue/3_3_Queue.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Singly-Linked List](4_1_SinglyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Doubly-Linked List](4_10_DoublyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)


## 6. C++ Container
- Sequence Containers
    - [forward_list](../2_Containers/forward_list/forward_list.md)
