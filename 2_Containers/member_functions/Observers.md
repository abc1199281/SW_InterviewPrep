# Observers
## Introduction
1. These operations return a function object, such as
    - compare key/values
    - hash_function, key equality
2. These operations only work for associative / unordered associative containers
2. *.key_comp()*, *value_comp()*
    - only work for associative containers
        - set, map, multiset, multimap
3. *.hash_function()*, *.key_eq()*
    - only work for unordered associative containers.
        - unordered_set, unordered_map, unordered_multiset, unordered_multimap