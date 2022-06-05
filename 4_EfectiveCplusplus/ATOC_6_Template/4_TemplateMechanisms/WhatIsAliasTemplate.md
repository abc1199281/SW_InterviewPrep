# What is the Alias Template?

### Reference: 6.4 Template Mechanisms

## Summary
0. Definition:
    - A kind of template Mechanisms 
        1. Variable Templates
        2. Aliases
        3. A compile-time selection mechanism: **if constexpr**
        4. A compile-time mechanism to inquire property: **require expressions**.
    - Type alias is a name that refers to a previously defined type (similiar to typedef).
    - Alias template is a name that refers to a family of types.
1. Syntax
    ~~~c++
    using identifier = type-id; //1

    template<template-parameter-list>
    using identifier = type-id; // 2
    ~~~
1. Applications
    - portable type (e.g., **size_t**).
    - STL convention (e.g., **value_type**).
    - new template (e.g., String_map<int> m = Map<string,int>)

## Detailed Information
1. Portable code
    - actual type named **size_t** is implementation-dependent.
    - Another implementation of *size_t* might be unsigned long.    
    ~~~c++
    using size_t = unsigned int;
    ~~~

2. STL convention
    - Parameterized type provides an alias for types related to their template arguments.
    ~~~c++
    template<typename T>
    class Vector{
    public:
        using value_type = T;
        //...
    }
    ~~~
    - When type information is required for some algorithm.
    ~~~c++
    // type of C's element
    template<typename C>
    using Value_type = typename C::value_type; 
    
    template<typename Container>
    void algo(Container& c){
        // declare a vector (vec) with the same type
        // as the element in the container C.
        Vector<Value_type<Container>> vec;
    }
    ~~~

3. New template
    - Reuse other template
    ~~~c++
    template<typename Key, typename Value>
    class Map{
        //...
    }

    template<typename Value>
    using String_MAP = Map<string, Value>;

    // usage
    String_map<int> m; // m is Map<string, int>
    ~~~

### Ref:
[1] A Tour of C++ (2e), Bjarne Stroustrup

### Date
2022/06/06