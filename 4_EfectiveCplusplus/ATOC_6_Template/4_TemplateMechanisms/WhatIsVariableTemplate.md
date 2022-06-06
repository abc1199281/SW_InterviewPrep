# What is the Variable Template?

### Reference: 6.4 Template Mechanisms

## Summary
0. Definition:
    - A variable template defines a family of variables or static data members.
    - Since **C++14**, predecessor of the idea of **concept**.

1. Syntax
    ~~~c++
    template < parameter-list > 
    variable-declaration	(variable type, name = value ;)	
    ~~~
2. Example
    ~~~c++
    // variable template
    template<class T>
    constexpr T pi = T(3.1415926535897932385L);  
    // Declaration:
    //      Type = T
    //      name = pi
    //      value = T(3.1415926535897932385L);  
 
    // function template
    template<class T>
    T circular_area(T r) 
    {
        // pi<T> is a variable template instantiation
        // pi<int> = int(3.1415926535897932385L);
        // pi<double> = double(3.1415926535897932385L);
        return pi<T> * r * r; 
    }
    ~~~

3.  This is a kind of template Mechanisms 
    1. Variable Templates 
    2. Aliases
    3. A compile-time selection mechanism: **if constexpr**
    4. A compile-time mechanism to inquire property: **require expressions**.

## Detailed information
- Predecessor of the idea of **concept** (7.2).
~~~c++
// variable template
template<typename T, typename T2>
constexpr bool Assignable = is_assignable<T&, T2>::value;
// is_assignable<T&, T2>::value-->This is a **type trait**

template<typename T>
void testing()
{
    static_assert(Assignable<T&, double>, "can't assign a double.");
    static_assert(Assignable<T&, string>, "can't assign a string.");
}
~~~

### Ref:
[1] A Tour of C++ (2e), Bjarne Stroustrup

### Date
2022/06/06