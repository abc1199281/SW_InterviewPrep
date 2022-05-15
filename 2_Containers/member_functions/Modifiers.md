# Modifiers
## Introduction
1. *.swap()*
    - work for all containers 

2. *.clear()*, *.insert()*, *.emplace()*, *.erase()*  
    - work for most containers, except
        - array, adapters (queue, stack, priority_queue)
3. *.emplace_hint()*
    - work for associative / unordered associative containers
3. *.push_front()*, *.emplace_front()*, *.pop_front()*  
    - Seq. containers: 
        - deque, forward_list, list
    - Adaptors:
        - queue(pop), priority_queue(pop)            
4. *.push_back()*, *.emplace_back()*, *.pop_back()*  
    - Seq. containers: 
        - vector, deque, list
    - Adaptors:
        - queue(push), priority_queue(push), stack(push)
        - stack(pop)

## Sequence containers
Containers|clear|insert|emplace|emplace_hint|erase|push_front|emplace_front|pop_front|push_back|emplace_back|pop_back|swap|merge|
-|-|-|-|-|-|-|-|-|-|-|-|-|-|
array|-|-|-|-|-|-|-|-|-|-|-|swap|-|
vector|clear|insert|emplace|-|erase|-|-|-|push_back|emplace_back|pop_back|swap|-|
deque|clear|insert|emplace|-|erase|push_front|emplace_front|pop_front|push_back|emplace_back|pop_back|swap|-|
forward_list|clear|insert_after|emplace_after|-|erase_after|push_front|emplace_front|pop_front|-|-|-|swap|merge|
list|clear|insert|emplace|-|erase|push_front|emplace_front|pop_front|push_back|emplace_back|pop_back|swap|merge|

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


## Containers Adaptors
Containers|clear|insert|emplace|emplace_hint|erase|push_front|emplace_front|pop_front|push_back|emplace_back|pop_back|swap|merge|
-|-|-|-|-|-|-|-|-|-|-|-|-|-|
stack|-|-|-|-|-|-|-|-|push|emplace|pop|swap|-|
queue|-|-|-|-|-|-|-|pop|push|emplace|-|swap|-|
priority_queue|-|-|-|-|-|-|-|pop|push|emplace|-|swap|-|
