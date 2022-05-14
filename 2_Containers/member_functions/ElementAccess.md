# Element Access
## Introduction
1. direct access (*.at()*, *[]*)
    - Array like container
        - array, vector, deque
    - Map (dictionary)
        - unordered_map, map
2. *.data()*
    - require continuous memory
    - array, vector
3. *.front()*
    - direct access (array, vector, deque)
    - list
        - forward_list, list
    - queue
        - queue, priority_queue (top)
4. *.back()*
    - direct access (array, vector, deque)
    - list
        - list (doubly linked list)
    - adaptor
        - stack (top), queue 
## Sequence containers
Containers|at|opearator[]|data|front|back|
-|-|-|-|-|-|
array|at|operator[]|data|front|back|
vector|at|operator[]|data|front|back|
deque|at|operator[]|-|front|back|
forward_list|-|-|-|front|-|
list|-|-|-|front|back|

## Associative containers
Containers|at|opearator[]|data|front|back|
-|-|-|-|-|-|
set|-|-|-|-|-|
multiset|-|-|-|-|-|
map|at|operator[]|-|-|-|
multimap|-|-|-|-|-|

## Unordered Associative containers
Containers|at|opearator[]|data|front|back|
-|-|-|-|-|-|
unordered_set|-|-|-|-|-|
unordered_multiset|-|-|-|-|-|
unordered_map|at|operator[]|-|-|-|
unordered_multimap|-|-|-|-|-|


## Containers Adaptors
Containers|at|opearator[]|data|front|back|
-|-|-|-|-|-|
stack|-|-|-|-|top|
queue|-|-|-|front|back|
priority_queue|-|-|-|top|-|
