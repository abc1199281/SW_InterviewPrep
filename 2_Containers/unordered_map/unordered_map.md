# unordered_map
## Definition

~~~c++
template<
    class Key,
    class T, 
    class Hash =std::hash<Key>,
    class KeyEqual = std::equal_to<Key>,
    class Allocator = std::allocator<std::pair<const Key,T>>
>
~~~