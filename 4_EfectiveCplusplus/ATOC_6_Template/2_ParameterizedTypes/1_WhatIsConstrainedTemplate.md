# What is the constrained template (C++20)?

### Reference: 6.2.1 constrained template argument

## Summary
1. Motivation:
    - Most often, a template will make sense only for template arguments that meet certain criteria. 
    - E.g., **Vector** require copyable elements.
2. Definition:
    - *Constrained argument* is arguments that specified by *concept*.
    - *constrained template*: one of the argument is constrained.
3. Sample 1:
    ~~~c++
    // Note: not template<typename T>
    template<Element T> // Element is a concept.
    class Vector{
    private:
        T* elem;
        int sz;
    }

    Vector<int> v1; // OK
    Vector<thread> v2; // error, thread is not copyable.
    ~~~
4. Sample 2:
    ~~~c++
    #include <type_traits> 

    // Define a concept.
    template <typename T>
    concept Integral = std::is_integral_v<T>; // Type Predicates

    // constrained template.
    template <typename T, Integral U>
    void func(const T &, U);
    ~~~

## Detailed Information
1. One of the parameterized types in template.
    - **Constrained Template Arguments**
    - Value Template Arguments
    - Template Argument Deduction

### Ref
[1] [Jonny's blog: 【C++ 20】Concept](https://jonny.vip/2021/07/11/%e3%80%90cplusplus-20%e3%80%91concept/)
### Date
2022/06/06