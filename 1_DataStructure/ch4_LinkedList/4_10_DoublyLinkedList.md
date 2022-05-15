## Doubly Linked list
## 1. Motivation: 
- Use pointers and values for operations, O(1) for insertion, deletion.
- One of the basic implementation for all others data structures. 
    - The other one is [array](../../2_Containers/array/array.md).

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
- Compared to [Singly-Linked List](../1_DataStructure/ch4_LinkedList/4_1_SinglyLinkedList.md), this data structure provides **bidirectional iteration** capability while being **less space efficient**.

Structure |**Time**| | | | | | | |**Space**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
 ||Average| | | |Worst| | | |Worst
 ||Access|Search|Insertion|Deletion|Access|Search|Insertion|Deletion|-
[Stack](../1_DataStructure/ch3_StackAndQueue/3_2_Stack.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Queue](../1_DataStructure/ch3_StackAndQueue/3_3_Queue.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Singly-Linked List](../1_DataStructure/ch4_LinkedList/4_1_SinglyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Doubly-Linked List](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)

## 6. C++ Container
- Sequence Containers
    - [forward_list](../../2_Containers/forward_list/forward_list.md)