## Hash table (Static Hashing)
## 1. Motivation: 
- Problem: 
    - Search
    - Assumption: no need of traversal data in order.
    - Goal: optimize search speed.
- Idea:
    - Given currect *index*, access for array is O(1).
    - We can remap *key* to *index* with a pre-defined function, *hash function*.
- Result:
    - With aid of **Hash function** & **Collision Handling**, amortized time for search is constant.
- Expended topic:
    - 8.3 Dynamic hashing
        - Dealing with expanding space.
    - 8.4 BLOOM Filter
        - Pros: space complexity.
        - Cons: 
            - risk of false positive.
            - cannot delete inserted data.

## 2. Pros. & Cons.
- Pros: 
    - comparing with [BLOOM filter](8_4_BLOOM_Filter.md)
        - [+] can delete inserted data.
        - [+] no risk of false positive
- Cons:
    - comparing with [BLOOM filter](8_4_BLOOM_Filter.md)
        - larger space complexity.
    
## 3. When to use:
- Const time searching is required.

## 4. Implementation
1. Notations    
    - *ht*: hash table
    - *b*: buckets.
2. Hash functions
    - Heuristic methods
        - division (mod)
        - multiplication
        
3. Collision handling:
    1. Open addressing (probing)
        - 4 types of probing
            1. linear probing
            2. quadratic probing
            3. rehashing
            4. random probing
        - array, continuous space, complex operations
        - no need of another space.
    2. Chaining
        - linked list
            - require address space.
    
4. array or linked list:
    - Hash table is essetially an application of array.
    - Dynamic Hash requires some pointers.
5. Classic problems
    - See [705. Design HashSet](https://leetcode.com/problems/design-hashset/)

## 5. Alternative



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

## 7. Reference
- [Is there any advantage of using map over unordered_map in case of trivial keys?](https://stackoverflow.com/questions/2196995/is-there-any-advantage-of-using-map-over-unordered-map-in-case-of-trivial-keys)