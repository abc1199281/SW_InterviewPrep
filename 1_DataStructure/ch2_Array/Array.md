## Array
## 1. Motivation: 
- One of the basic implementation for all others data structures. 
- The other basic data staructure is linked list.

## 2. Pros. & Cons.
- Pros: 
    - O(1), Direct access based on index.
- Cons:
    - O(n), when expanding/contraction space 
    - Performs the worst when Insertion, Deletion.
## 3. When to use:
- Direct access dominates
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
