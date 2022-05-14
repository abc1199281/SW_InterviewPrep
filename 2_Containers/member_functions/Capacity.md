# Capacity
## Introduction
1. *.empty()*
    - All containers have this function.
2. *.size()*
    - The only exception is **forward_list**, which require O(n).
    - All other containers have *.size()* function
    
3. *.max_size()*
    - Returns the maximum number of elements the container is able to hold due to system/lib.
    - Theoretical limit
        - e.g., std::vector = 9,223,372,036,854,775,807
    - Most containers except adapters.        
        - *stack, queue, priority_queue*
    
4. *.resize()*
    - All Sequence containers except *array*.
    - vector-based (vector, deque)
    - list-based (list, forward_list)

5. *.capacity()*
    - All unordered associate containers (unordered_*)
        - *.bucket_count()*
    - and *vector*

6. *.reserve()*
    - All unordered associate containers (unordered_*)
    - and *vector*

7. *.shrink_to_fit()*
    - only vector, deque

## Sequence containers
Containers|empty|size|max_size|resize|capacity|reserve|shrink_to_fit|
-|-|-|-|-|-|-|-|
array|empty|size|max_size|-|-|-|-|
vector|empty|size|max_size|resize|capacity|reserve|shrink_to_fit|
deque|empty|size|max_size|resize|-|-|shrink_to_fit|
forward_list|empty|-|max_size|resize|-|-|-|
list|empty|size|max_size|resize|-|-|-|

## Associative containers
Containers|empty|size|max_size|resize|capacity|reserve|shrink_to_fit|
-|-|-|-|-|-|-|-|
set|empty|size|max_size|-|-|-|-|
multiset|empty|size|max_size|-|-|-|-|
map|empty|size|max_size|-|-|-|-|
multimap|empty|size|max_size|-|-|-|-|

## Unordered Associative containers
Containers|empty|size|max_size|resize|capacity|reserve|shrink_to_fit|
-|-|-|-|-|-|-|-|
unordered_set|empty|size|max_size|-|bucket_count|reserve|-|
unordered_multiset|empty|size|max_size|-|bucket_count|reserve|-|
unordered_map|empty|size|max_size|-|bucket_count|reserve|-|
unordered_multimap|empty|size|max_size|-|bucket_count|reserve|-|

## Containers Adaptors
Containers|empty|size|max_size|resize|capacity|reserve|shrink_to_fit|
-|-|-|-|-|-|-|-|
stack|empty|size|-|-|-|-|-|
queue|empty|size|-|-|-|-|-|
priority_queue|empty|size|-|-|-|-|-|
