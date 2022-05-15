# Lookup
## Introduction
1. These operations only work for associative / unordered associative containers
2. *.count()*, *.find()*, *.equal_range()*
    - works for all of them.

    
## Associative containers 
Containers|clear|insert|emplace|emplace_hint|erase|push_front|emplace_front|pop_front|push_back|emplace_back|pop_back|swap|merge|
-|-|-|-|-|-|-|-|-|-|-|-|-|-|
set|clear|insert|emplace|emplace_hint|erase|-|-|-|-|-|-|swap|merge|
multiset|clear|insert|emplace|emplace_hint|erase|-|-|-|-|-|-|swap|merge|
map|clear|insert|emplace|emplace_hint|erase|-|-|-|-|-|-|swap|merge|
multimap|clear|insert|emplace|emplace_hint|erase|-|-|-|-|-|-|swap|merge|
### Note: Merge opeartion is supported for set/map only after c++17.

## Unordered Associative containers
Containers|clear|insert|emplace|emplace_hint|erase|push_front|emplace_front|pop_front|push_back|emplace_back|pop_back|swap|merge|
-|-|-|-|-|-|-|-|-|-|-|-|-|-|
unordered_set|clear|insert|emplace|emplace_hint|erase|-|-|-|-|-|-|swap|merge|
unordered_multiset|clear|insert|emplace|emplace_hint|erase|-|-|-|-|-|-|swap|merge|
unordered_map|clear|insert|emplace|emplace_hint|erase|-|-|-|-|-|-|swap|merge|
unordered_multimap|clear|insert|emplace|emplace_hint|erase|-|-|-|-|-|-|swap|merge|
