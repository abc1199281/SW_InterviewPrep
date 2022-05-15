## Array
## 1. Motivation: 
- Problem:
    - Access
- Idea:
    - Continuous space, O(1) for direct access.
- Results:
    - One of the two basic strategy for all the others data structures. 
        - The other basic one is the [Linked List](../1_DataStructure/ch4_LinkedList/4_1_SinglyLinkedList.md).

## 2. Pros. & Cons.
- Pros: 
    - O(1), Direct access based on index.
- Cons:
    - O(n), when expanding/contraction space 
    - Performs the worst when Insertion, Deletion.
## 3. When to use:
- Applications when Direct accessing dominates
    - Binary Search
    - Dynamic Programming

## 4. Implementation
- Just array.

## 5. Alternative
- When direct access dominates, array is the best choice.

Structure |**Time**| | | | | | | |**Space**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
 ||Average| | | |Worst| | | |Worst
 ||Access|Search|Insertion|Deletion|Access|Search|Insertion|Deletion|-
[Array](/Array.md)|**o(1)**|o(n)|o(n)|o(n)|**O(1)**|O(n)|O(n)|O(n)|O(n)


## 6. C++ Container
- Sequence Containers
    - [array](../2_Containers/array/array.md)
    - [vector](../2_Containers/vector/vector.md)
    - [deque](../2_Containers/deque/deque.md)
