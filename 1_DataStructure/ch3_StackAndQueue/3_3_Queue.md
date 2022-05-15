## Queue
## 1. Motivation
- Insertion & Deletion dominates
- First in first out (FIFO).

## 2. Pros. & Cons.
- Pros: 
    - O(1) for Insertion & Deletion.
- Cons:
    - O(n) for Access & Search.

## 3. When to use:
- Applications when Insertion & Deletion dominate.
- Algorithms
    - Iterative BFS traversal
        - Same layer first in, firt process same layer (FIFO)
        - Need to keep the number of next layer.
    
## 4. Implementation
- By array
    - Pros: save space (address)
    - Cons: Large effort when expanding/contracting space.
- By Linked list
    - Pros: little effort when expanding/contracting space 
    - Cons: More space for address
- By deque (Default in c++)
    - Hybrid of both
        - **map** (a variabled vector) which store address, behaved as linked list.
        - **chunck of fixed sized vector**, behaved as array.
    - For detail, please see ([deque](../2_Containers/deque/deque.md))
   
## 5. Alternative
- When insertion & deletion dominates, alternatives are listed as follow.

Structure |**Time**| | | | | | | |**Space**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
 ||Average| | | |Worst| | | |Worst
 ||Access|Search|Insertion|Deletion|Access|Search|Insertion|Deletion|-
[Stack](../1_DataStructure/ch3_StackAndQueue/3_2_Stack.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Queue](../1_DataStructure/ch3_StackAndQueue/3_3_Queue.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Singly-Linked List](../1_DataStructure/ch4_LinkedList/4_1_SinglyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Doubly-Linked List](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)

## 6. C++ Container
- Adapter Containers
    - [stack](../2_Containers/stack/stack.md)