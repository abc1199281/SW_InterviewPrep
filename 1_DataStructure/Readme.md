# Introduction

In this section, we want to answer **Why and When** to use specific type of data structure.

For each data structure, we would answer the questions with following structures.
## Structures
1. Motivation 
    - Why to use?
2. Pros. and Cons. 
3. When to use? 
    - Classical Algorithms / leet code problems that utilize the data structure.
4. Implementations
    - array v.s. linked list
5. Possible alternatives
6. C++ Containers

## Operations
With known property of an algorithm, we should choose corresponding data structure, which can minimize the temporal complexity or space complexity. 

Structure |**Time**| | | | | | | |**Space**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
 ||Average| | | |Worst| | | |Worst
 ||Access|Search|Insertion|Deletion|Access|Search|Insertion|Deletion|-
[Array](../1_DataStructure/ch2_Array/Array.md)|**o(1)**|o(n)|o(n)|o(n)|**O(1)**|O(n)|O(n)|O(n)|O(n)
[Stack](../1_DataStructure/ch3_StackAndQueue/3_2_Stack.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Queue](../1_DataStructure/ch3_StackAndQueue/3_3_Queue.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Singly-Linked List](../1_DataStructure/ch4_LinkedList/4_1_SinglyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Doubly-Linked List](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md)|o(n)|o(n)|**o(1)**|**o(1)**|O(n)|O(n)|**O(1)**|**O(1)**|O(n)
[Skip List](../1_DataStructure/Others/SkipList.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|O(n)|O(n)|O(n)|O(n)|*O(log(n))*
[HashTable](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|N/A|**o(1)**|**o(1)**|**o(1)**|N/A|O(n)|O(n)|O(n)|O(n)
[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|O(n)|O(n)|O(n)|O(n)|O(n)
[Cartesian Tree](../1_DataStructureOthers/CartesianTree.md)|N/A|*o(log(n))*|*o(log(n))*|*o(log(n))*|N/A|O(n)|O(n)|O(n)|O(n)
[B Tree](../1_DataStructure/ch11_MultipathSearchTree/11_2_B_Tree.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[Red Black Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[Splay Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_4_SplayTree.md)|N/A|*o(log(n))*|*o(log(n))*|*o(log(n))*|N/A|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[AVL Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_2_AVL_Tree.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[KD Tree](../1_DataStructure/Others/KD_Tree.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|O(n)|O(n)|O(n)|O(n)|O(n)



## Refference
[1] Fundamentals of Data Structures in C++ (2e), Ellis Horowitz, Sartaj Sahni, Dinesh P. Mehta.
