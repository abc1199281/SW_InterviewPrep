## Stack
## Motivation
- Insertion & Deletion dominates
- FILO

## Pros. & Cons.
- Pros: 
    - O(1) for Insertion & Deletion.
- Cons:
    - O(n) for Access & Search.

## When to use:
- Algorithms
    - Iterative DFS traversal
        - Deeper layer first in, process them first (FILO)
        - Visited is required.
    

## C++ Container & Implementation
- By Linked list
    - Pros: No need of enlarging / shrink space.
    - Cons: More space for address
- By array 
    - Pros: save space
    - Cons: Deal with enlarging / shrink space.

## C++ Container & usage
~~~c++
#inclue <vector>

// initialization
vector<int> vec={1,2,3}

// size
vec.size();

// iterations

~~~

## Other candidates 
- Insertion & Deletion dominates

Structure |**Time**| | | | | | | |**Space**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
 ||Average| | | |Worst| | | |Worst
 ||Access|Search|Insertion|Deletion|Access|Search|Insertion|Deletion|-
[Stack](\ch3_StackAndQueue\3_2_Stack.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Queue](\ch3_StackAndQueue\3_3_Queue.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Singly-Linked List](\ch4_LinkedList\4_1_SinglyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Doubly-Linked List](\ch4_LinkedList\4_10_DoublyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)