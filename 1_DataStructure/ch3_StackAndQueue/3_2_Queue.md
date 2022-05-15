## Queue
## Motivation
- Insertion & Deletion dominates
- FIFO

## Pros. & Cons.
- Pros: 
    - O(1) for Insertion & Deletion.
- Cons:
    - O(n) for Access & Search.

## When to use:
- Algorithms
    - Iterative BFS traversal
        - Same layer first in, firt process same layer (FIFO)
        - Need to keep the number of next layer.
    

## C++ Container & Implementation
- By array (Default=deque)
    - Pros: save space
    - Cons: Deal with enlarging / shrink space.
- By Linked list
    - Pros: No need of enlarging / shrink space.
    - Cons: More space for address

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