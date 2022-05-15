## Binary Search Tree (BST)
## 1. Motivation: 
- Question:
    - For Searching, both Linked list and array require O(n). We want something faster.
- Idea:
    - Binary search only require O(log(n)), given a sorted array.
- Solution: 
    - Applying the concept of **binary search** while building **dictionary**.

### 1.1 Properties
- Each element has unique key.
- All keys in left sub-tree are smaller than the key of its root. 
- All keys in right sub-tree are greater than the key of its root. 
- Each sub-tree is also binary search tree.

## 2. Pros. & Cons.
- Pros: 
    - For Searching, relative good with complexity t(log(n)).
- Cons:
    - There is a O(1) search method, [HashTable](../ch8_Hash/8_2_Hashtable.md).
    - O(n) for worst case.
        - solved by [B Tree](../ch11_MultipathSearchTree/11_2_B_Tree.md), [Red Black Tree](../ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md), and [AVL Tree](../ch10_HigPerformancyBinarySearchTree/10_2_AVL_Tree.md).
    

## 3. When to use:
- Currently I've not found the most suitable applications.

## 4. Implementation
- based on Tree (Linked list).

## 5. Alternative
- When Searching dominates, 
    - If data is unordered, we shuold choose [HashTable](../ch8_Hash/8_2_Hashtable.md).
    - If data is should be ordered (sorted) or less memory, we shuold choose [Red Black Tree](../ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md).

Structure |**Time**| | | | | | | |**Space**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
 ||Average| | | |Worst| | | |Worst
 ||Access|Search|Insertion|Deletion|Access|Search|Insertion|Deletion|-
 [HashTable](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|N/A|**t(1)**|**t(1)**|**t(1)**|N/A|O(n)|O(n)|O(n)|O(n)
[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|O(n)|O(n)|O(n)|O(n)|O(n)
[Cartesian Tree](../1_DataStructureOthers/CartesianTree.md)|N/A|*o(log(n))*|*o(log(n))*|*o(log(n))*|N/A|O(n)|O(n)|O(n)|O(n)
[B Tree](../1_DataStructure/ch11_MultipathSearchTree/11_2_B_Tree.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[Red Black Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[Splay Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_4_SplayTree.md)|N/A|*o(log(n))*|*o(log(n))*|*o(log(n))*|N/A|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[AVL Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_2_AVL_Tree.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[KD Tree](../1_DataStructure/Others/KD_Tree.md)|*o(log(n))*|*o(log(n))*|*o(log(n))*|*o(log(n))*|O(n)|O(n)|O(n)|O(n)|O(n)


## 6. C++ Container
- Sequence Containers
    - [array](../2_Containers/array/array.md)
    - [vector](../2_Containers/vector/vector.md)
    - [deque](../2_Containers/deque/deque.md)

