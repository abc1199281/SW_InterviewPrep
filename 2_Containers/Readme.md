# From Data Structure to C++ STL Containers
In previous section, we've known **why and when** to use basic data structure.

However, when it comes to implementation, there is still a question, **How?**

Basically, we use c++ containers as data structure to implement algorithms. So, we should really understand the foundmental implemetations of C++ containers.

## Structure
1. Motivations    
2. Properties 
    - Itemized for memorization
3. Internal Implementations
    - Relationship to data structure
4. Basic Operations
    1. Access
    2. Search (Iterations)
    3. Insertion
    4. Deletion
5. Alternatives and Comparison
6. Optional (e.g., Other advanced usage / tips)

## Table
| Header | DataStructure | Implementation |Types| c++11|
|-|-|-|-|- |
|\<array\> | [array](../2_Containers/array/array.md) |[Array](../1_DataStructure/ch2_Array/Array.md)|Seq.|v|
|\<vector\>|[vector](../2_Containers/vector/vector.md) |[Array](../1_DataStructure/ch2_Array/Array.md)|Seq.|-|
|\<deque\>|[deque](../2_Containers/deque/deque.md) |[Array](../1_DataStructure/ch2_Array/Array.md)|Seq.|-|
|\<queue\>|[queue](../2_Containers/queue/queue.md) |[(default=deque) Array](../1_DataStructure/ch2_Array/Array.md), [Doubly-linked lists](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md)|Adaptor|-|
|\<queue\>|[priority_queue](../2_Containers/queue/priority_queue.md) |[(default=deque) Array](../1_DataStructure/ch2_Array/Array.md), [(list) Doubly-linked lists](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md)|Adaptor|-|
|\<stack\>|[stack](../2_Containers/stack/stack.md) |[(default=deque) Array](../1_DataStructure/ch2_Array/Array.md), [(list) Doubly-linked lists](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md), [(vector) Array](../1_DataStructure/ch2_Array/Array.md)|Adaptor|-|
| \<forward_list\> |[forward_list](../2_Containers/forward_list/forward_list.md) |[Singly-linked lists](../1_DataStructure/ch4_LinkedList/4_1_SinglyLinkedList.md)|Seq.|v|
|\<list\>|[list](../2_Containers/list/list.md) |[Doubly-linked lists](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md)|Seq.|-|
|\<map\>|[map](../2_Containers/map/map.md) |[Red Black Tree](../1_DataStructure/ch10_HigPerformancyBinarySearchTree/10_3_RedBlackTree.md)|Associ.|-|
|\<map\>|[multimap](../2_Containers/map/multi_map.md) |[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|Associ.|-|
|\<set\>|[set](../2_Containers/set/set.md) |[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|Associ.|-|
|\<set\>|[multiset](../2_Containers/set/multiset.md) |[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|Associ.|-|
|\<unordered_map\>|[unordered_map](../2_Containers/unordered_map/unordered_map.md) |[Hash](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|Unordered|V|
|\<unordered_map\>|[unordered_multimap](../2_Containers/unordered_map/unordered_multimap.md) |[Hash](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|Unordered|V|
|\<unordered_set\>|[unordered_set](../2_Containers/unordered_set/unordered_set.md) |[Hash](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|Unordered|V|
|\<unordered_set\>|[unordered_multiset](../2_Containers/unordered_set/unordered_multiset.md) |[Hash](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|Unordered|V|


### Note: three types of container
1. Sequence containers (Seq.)
    - can be accessed sequentially.
2. Associative containers (Associ.)
    - sorted data structures that can be quickly searched.
    - O(**log** **n**).
3. Unordered associative containers (unorder)
    - Unsorted (hashed) data structures that can be quickly searched 
    - O(1) amortized, O(n) worst-case
4. Container adaptors (adapt.)
    - adaptors that provide different interface for sequential containers.
## Refference
[1] [C++ reference](https://www.cplusplus.com/reference/)
[2] [cppreference](https://en.cppreference.com/w/cpp/container)