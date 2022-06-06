# What is the Type Predicates?

### Reference: 13.9.2 Type Predicates

## Summary
0. Definition:
    - <type_traits> is a part of metaprogramming library.
    - Provides compile-time template-based interfaces to query the properties of types.
    check types    
1. Usage
    ~~~c++
    bool b1 = std::is_arithmetic<int>();    // true
    bool b1 = std::is_arithmetic<string>(); // false

    template<typename Scalar>
    class complex{
        Scalar re, im;
    public:
        // static_assert declaration, performs compile-time checking.
        static_assert(is_arithmetic<Scalar>(),"Sorry, only support complex of arithmetic types.");
    }
    ~~~

## Detailed information
1. Categories (just to name a few.)
    1. Primary type categories    
    ~~~c++
    is_void
    is_array
    is_floating_point
    is_function
    is_lvalue_reference    
    ~~~
    2. Composite type categories    
    ~~~c++
    is_arithmetic
    is_scalar
    is_object
    is_reference    
    ~~~
    3. type properties
    ~~~c++
    is_const
    is_volatile
    is_empty
    ~~~
    4. supported operations
    ~~~c++
    is_constructible
    is_asignable
    is_swappable
    ~~~
### Ref:
[1] A Tour of C++ (2e), Bjarne Stroustrup

### Date
2022/06/06