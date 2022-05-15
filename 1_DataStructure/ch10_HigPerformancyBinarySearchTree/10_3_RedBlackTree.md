## Red Black Tree
## 1. Motivation: 
- Problem:
    - Application: Search
    - [Binary Search Tree](../ch5_Tree/5_7_BST.md)       
        - [-] can easily degenrate to the worst case, O(n). 
        - [-] non-balanced. 
    - AVL tree:
        - [+] solve the problem by **rotation**.
        - [-] requires complex insertion and remorval operations due to strick balance strategy. 
- Ideas:
    - we just build a roughly balanced tree.
- Results:
    - [=] Access, Search, Insertion, Deletion 
        - keep O(log(n)).
    - [+] Take less memory (1 bit).
    - [+] Insertion, Deletion are faster.
        - Take less processing for balancing.
        - maximum of 2 rotations are required.
    - [-] Search is comparatively slower.
    - [+] Easier to implement.


## 2. Pros. & Cons.
- Pros: 
    - Comparing with non-balanced [Binary Search Tree](../ch5_Tree/5_7_BST.md)         
        - Improve from O(n) to O(log(n)) for all basic operations.
    - Comparing with [HashTable](../ch8_Hash/8_2_Hashtable.md).
        - Support traversal in order.
        - Better worst case for insertion/deletion.
        - If hash function takes too long (e.g., long string), RB tree also has advantage.
        - Hashtable is O(n), because it requires backing dynamic array. 
    - Comparing with [AVL Tree](../ch10_HigPerformancyBinarySearchTree/10_2_AVL_Tree.md)
        - [+] requires only one bit (red-black), whereas AVL requires another storage, one integer per node.
- Cons:
    - Comparing with BST  
        - Nope.
    - Comparing with [HashTable](../ch8_Hash/8_2_Hashtable.md).
        - Much large average time complexity for Searching, insertion, deletion
        - t(log(n))->t(1).
    - Comparing with [AVL Tree](../ch10_HigPerformancyBinarySearchTree/10_2_AVL_Tree.md)
        - [-] less efficient searching.
    
## 3. When to use:
- Used in many *search* applications where data is constantly entering/leaving.
- Red Black Trees are used in most of the language libraries like map, multimap, multiset in C++ etc.

## 4. Implementation
- only linked-list based.

## 5. Alternative
- Commonly compared.

-|Hash Table|Red-black Tree|
-|-|-|
Containers|unordered_map unordered_set|set map|
Traversal in order|x|**Support**|
Insertion (avg.)|**t(1)**|t(log(n))|
Search (avg.)|**t(1)**|t(log(n))|
Insertion (worst)|O(n)|**O(log(n))**|
Search (worst)|O(n)|**O(log(n))**|


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
- Associative Containers
    - [map](../2_Containers/map/map.md)
    - [multimap](../2_Containers/map/multimap.md)
    - [set](../2_Containers/set/set.md)
    - [multiset](../2_Containers/set/multiset.md)

## 7. Reference
- [What is the underlying data structure of a STL set in C++?](https://stackoverflow.com/questions/2558153/what-is-the-underlying-data-structure-of-a-stl-set-in-c)
- [What data structure is inside std::map in C++?](https://stackoverflow.com/questions/18414579/what-data-structure-is-inside-stdmap-in-c/51945119#51945119)
- [Is there any advantage of using map over unordered_map in case of trivial keys?](https://stackoverflow.com/questions/2196995/is-there-any-advantage-of-using-map-over-unordered-map-in-case-of-trivial-keys)