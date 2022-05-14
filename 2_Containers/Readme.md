# From Data Structure to C++ STL Containers
In previous section, we've known **why and when** to use basic data structure.

However, when it comes to implementation, there is still a question, **How?**

Basically, we use c++ containers as data structure to implement algorithm. So, we should really understand the foundmental implemetations of C++ containers.

# Table
| Header | DataStructure | Implementation |Note| c++11|
|-|-|-|-|- |
|\<array\> | array |[Array](../1_DataStructure/ch2_Array/Array.md)|Fixed-size|v|
|\<deque\>|[deque](../2_Containers/deque/deque.md) |[Array](../1_DataStructure/ch2_Array/Array.md)|-|-|
| \<forward_list\> |[forward_list](../2_Containers/forward_list/forward_list.md) |[Singly-linked lists](../1_DataStructure/ch4_LinkedList/4_1_SinglyLinkedList.md)|-|v|
|\<list\>|[list](../2_Containers/list/list.md) |[Doubly-linked lists](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md)|-|-|
|\<map\>|[map](../2_Containers/map/map.md) |[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|-|-|
|\<map\>|[multi-map](../2_Containers/map/multi_map.md) |[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|-|-|
|\<queue\>|[queue](../2_Containers/queue/queue.md) |[(default=deque) Array](../1_DataStructure/ch2_Array/Array.md), [Doubly-linked lists](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md)|-|-|
|\<queue\>|[priority_queue](../2_Containers/queue/priority_queue.md) |[(default=deque) Array](../1_DataStructure/ch2_Array/Array.md), [(list) Doubly-linked lists](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md)|-|-|
|\<set\>|[set](../2_Containers/set/set.md) |[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|-|-|
|\<set\>|[multiset](../2_Containers/set/multiset.md) |[Binary Search Tree](../1_DataStructure/ch5_Tree/5_7_BST.md)|-|-|
|\<stack\>|[stack](../2_Containers/stack/stack.md) |[(default=deque) Array](../1_DataStructure/ch2_Array/Array.md), [(list) Doubly-linked lists](../1_DataStructure/ch4_LinkedList/4_10_DoublyLinkedList.md), [(vector) Array](../1_DataStructure/ch2_Array/Array.md)|-|-|
|\<unordered_map\>|[unordered_map](../2_Containers/unordered_map/unordered_map.md) |[Hash](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|-|V|
|\<unordered_map\>|[unordered_multimap](../2_Containers/unordered_map/unordered_multimap.md) |[Hash](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|-|V|
|\<unordered_set\>|[unordered_set](../2_Containers/unordered_set/unordered_set.md) |[Hash](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|-|V|
|\<unordered_set\>|[unordered_multiset](../2_Containers/unordered_set/unordered_multiset.md) |[Hash](../1_DataStructure/ch8_Hash/8_2_Hashtable.md)|-|V|
|\<vector\>|[vector](../2_Containers/vector/vector.md) |[Array](../1_DataStructure/ch2_Array/Array.md)|-|V|
## Refference
[1] [C++ reference](https://www.cplusplus.com/reference/)
