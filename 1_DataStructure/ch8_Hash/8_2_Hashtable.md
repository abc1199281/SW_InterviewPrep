## Hash table
## 1. Motivation: 
- comming soon
## 2. Pros. & Cons.

- Pros: 
    - comming soon
- Cons:
    - comming soon
    
## 3. When to use:
- comming soon

## 4. Implementation
- comming soon

## 5. Alternative
- Good discussion: [Is there any advantage of using map over unordered_map in case of trivial keys?](https://stackoverflow.com/questions/2196995/is-there-any-advantage-of-using-map-over-unordered-map-in-case-of-trivial-keys)


Structure |**Time**| | | | | | | |**Space**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
 ||Average| | | |Worst| | | |Worst
 ||Access|Search|Insertion|Deletion|Access|Search|Insertion|Deletion|-
[HashTable](../ch8_Hash/8_2_Hashtable.md)|N/A|**t(1)**|**t(1)**|**t(1)**|N/A|O(n)|O(n)|O(n)|O(n)
[Binary Search Tree](../ch5_Tree/5_7_BST.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|O(n)|O(n)|O(n)|O(n)|O(n)
[Cartesian Tree](../CartesianTree.md)|N/A|*t(log(n))*|*t(log(n))*|*t(log(n))*|N/A|O(n)|O(n)|O(n)|O(n)
[B Tree](../ch11_MultipathSearchTree/11_2_B_Tree.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[Red Black Tree](../ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[Splay Tree](../ch10_HigPerformancyBinarySearchTree/10_4_SplayTree.md)|N/A|*t(log(n))*|*t(log(n))*|*t(log(n))*|N/A|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[AVL Tree](../ch10_HigPerformancyBinarySearchTree/10_2_AVL_Tree.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|*O(log(n))*|O(n)
[KD Tree](../Others/KD_Tree.md)|*t(log(n))*|*t(log(n))*|*t(log(n))*|*t(log(n))*|O(n)|O(n)|O(n)|O(n)|O(n)

## 6. C++ Container
- Unordered Associative Containers
    - [unordered_map](../2_Containers/unordered_map/unordered_map.md)
    - [unordered_multimap](../2_Containers/unordered_map/unordered_multimap.md)
    - [unordered_set](../2_Containers/unordered_set/unordered_set.md)
    - [unordered_multiset](../2_Containers/unordered_set/unordered_multiset.md)
