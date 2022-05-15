## Doubly Linked list
## 1. Motivation: 
- Problem:
    - Insertion & Deletion
    - Two directions
- Idea:
    - doubly linked
- Result:
    - two direction with the cost of space.

## 2. Pros. & Cons.
- Pros: 
    - O(1) for Insertion, Deletion.
- Cons:
    - O(n) for Access.
    - Fast random access is not supported. 

## 3. When to use:
- Applications when Insertion & Deletion dominate.
- Algorithms:
    - Root structure for *Tree*, *Graph*.

## 4. Implementation
- Just linked list.

## 5. Alternatives
- When insertion & deletion dominates, alternatives are listed as follow.
- Compared to [Singly-Linked List](4_1_SinglyLinkedList.md), this data structure provides **bidirectional iteration** capability while being **less space efficient**.

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
    - [forward_list](../../2_Containers/forward_list/forward_list.md)