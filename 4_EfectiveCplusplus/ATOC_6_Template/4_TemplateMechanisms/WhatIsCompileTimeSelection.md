# What is the compile-time selection mechanism: if constexpr?

### Reference: 6.4.3 Template Mechanisms

## Summary
0. Motivation:
    - Compile-time choose based on data type.
    ~~~c++
    If (data_type==?)
        slow_and_safe(T)
    else
        slow_and_safe(T)
    ~~~
    - Implementation (since C++17)
    ~~~c++
    template<typename T>
    void update(T& target){
        //...
        // Only one of these is instantiated.
        if constexpr(is_pod<T>::value)
            simple_and_fast(target);
        else
            slow_and_safe(target);
        //...
    }    
    ~~~    

### Ref:
[1] A Tour of C++ (2e), Bjarne Stroustrup

### Date
2022/06/06