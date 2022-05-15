## AVL Tree
## 1. Motivation: 
- Problem:
    - Application: Search
    - [Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)
        - [-] can easily degenrate to the worst case, O(n). 
        - [-] non-balanced.
- Ideas:
    - Find a scheme to balance the BST (red-black color).
    - For each insertion, rotating the root to balance the tree.
- Results:
    - Access, Search, Insertion, Deletion 
        - Improve from O(n) to O(log(n)).

## 2. Pros. & Cons.
- Pros: 
    - Comparing with non-balanced [Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)       
        - Improve from O(n) to O(log(n)) for all basic operations.
    - Comparing with [HashTable](../1_DataStructure/ch8_Hash/8_2_Hashtable.md).
        - Support traversal in order.
        - Better worst case for insertion/deletion.
        - If hash function takes too long (e.g., long string), RB tree also has advantage.
        - Hashtable is O(n), because it requires backing dynamic array. 
    - Comparing with [Red Black Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md)
        - [+] Search is comparatively faster.
        
- Cons:
    - Comparing with [Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)
        - Nope.
    - Comparing with [HashTable](../1_DataStructure/ch8_Hash/8_2_Hashtable.md).
        - Much large average time complexity for Searching, insertion, deletion
        - t(log(n))->t(1).
    - Comparing with [Red Black Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md)
        - [-] AVL requires another storage, one integer per node.
        - [-] Take more memory.
        - [-] Insertion, Deletion are faster.
            - Take more processing for balancing.            
        - [-] Harder to implement.

## 3. When to use:
- AVL Trees are used database for faster retrievals.

## 4. Implementation
- only linked-list based.

## 5. Alternative
- comming soon

- All data structure.

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
- comming soon
