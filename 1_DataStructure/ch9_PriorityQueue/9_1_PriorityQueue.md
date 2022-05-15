## Priority Queue
## 1. Motivation: 
- Question:
    - For Searching, both Linked list and array require O(n). We want something faster.
- Idea:
    - Binary search only require O(log(n)), given a sorted array.
- Solution: 
    - Applying the concept of **binary search** while building **dictionary**.

## 2. Pros. & Cons.
- Pros: 
    - For Searching, relative good with complexity t(log(n)).
- Cons:
    - There is a O(1) search method, [HashTable](../ch8_Hash/8_2_Hashtable.md).
    - O(n) for worst case.
        - solved by [Red Black Tree](../ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md), and [AVL Tree](../ch10_HigPerformancyBinarySearchTree/10_2_AVL_Tree.md).
    

## 3. When to use:
- Not recommended: 
    - If Binary tree is non-balanced (e.g, BST), this is not very usefull.
    - Unless the data is coming in in a relatively random order, the tree can easily degenerate into its worst-case form, which is a linked list.


## 4. Implementation
- based on Tree (Linked list).

## 5. Alternative
- When Searching, 
    - If data is unordered, we shuold choose [HashTable](../ch8_Hash/8_2_Hashtable.md).
    - If data is should be ordered (sorted) or less memory, we shuold choose [Red Black Tree](../ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md).
    - [B Tree](../ch11_MultipathSearchTree/11_2_B_Tree.md) used in many databases, where the limiting factor is not how many comparisons are done but how many nodes can be loaded from the hard-drive at once.

Structure |**Time**| | | | | | | |**Space**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
 ||Average| | | |Worst| | | |Worst
 ||Access|Search|Insertion|Deletion|Access|Search|Insertion|Deletion|-
[HashTable](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|N/A|**t(1)**|**t(1)**|**t(1)**|N/A|O(n)|O(n)|O(n)|O(n)
[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|O(n)|O(n)|O(n)|O(n)|O(n)
[Cartesian Tree](../1_DataStructureOthers/CartesianTree.md)|N/A|*t(log(n))*|*t(log(n))*|*t(log(n))*|N/A|O(n)|O(n)|O(n)|O(n)
[B Tree](../1_DataStructure/ch11_MultipathSearchTree/11_2_B_Tree.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[Red Black Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[Splay Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_4_SplayTree.md)|N/A|*t(log(n))*|*t(log(n))*|*t(log(n))*|N/A|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[AVL Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_2_AVL_Tree.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[KD Tree](../1_DataStructure/Others/KD_Tree.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|O(n)|O(n)|O(n)|O(n)|O(n)


## 6. C++ Container
- Adaptor Containers
    - [priority_queue](../../2_Containers/queue/priority_queue.md)