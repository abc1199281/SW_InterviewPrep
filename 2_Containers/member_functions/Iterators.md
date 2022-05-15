# Iterators
## Introduction
1. No iterators for Adapters
2. *.begin()*, *.cbegin()*, *.end()*, *.cend()*
    - supported by all other containers

3. *.rbegin()*, *.rcbegin()*, *.rend()*, *.rcend()*
    - only supported by sequential / associative containers.
        - except forward_list which cannot reverse.
    
## Sequence containers

Containers|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
-|-|-|-|-|-|-|-|-|
array|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
vector|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
deque|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
forward_list|begin|cbegin|end|cend|-|-|-|-|
list|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|

## Associative containers

Containers|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
-|-|-|-|-|-|-|-|-|
set|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
multiset|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
map|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
multimap|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|

## Unordered Associative containers

Containers|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
-|-|-|-|-|-|-|-|-|
unordered_set|begin|cbegin|end|cend|-|-|-|-|
unordered_multiset|begin|cbegin|end|cend|-|-|-|-|
unordered_map|begin|cbegin|end|cend|-|-|-|-|
unordered_multimap|begin|cbegin|end|cend|-|-|-|-|

## Containers Adaptors

Containers|begin|cbegin|end|cend|rbegin|rcbegin|rend|rcend|
-|-|-|-|-|-|-|-|-|
stack|-|-|-|-|-|-|-|-|
queue|-|-|-|-|-|-|-|-|
priority_queue|-|-|-|-|-|-|-|-|
