# What is the Type Traits?

## Summary
0. Definition:    
    - What is metaprogramming
        - programming: inupt = data, exe, output = data
        - metaprogramming: exe: reflect itself, gen other codes.
    - type_traits:
        - <type_traits> c++11
        - e.g., is_pointer<T>::value
1. Syntax
    ~~~c++
    template<typename T>
    void print(T t)
    {
        if constexpr(std::is_pointer<T>::value){
            std::cout << *t;
        }else{
            std::cout<< t;
        }
    }
    ~~~


## Detailed Information
    
~~~c++
#include <iostream>
#include <type_traits>

/*
// original: cannot distinguish pointers
template<typename A, typename B, typename C>
void print3(A a,B b,C c){
    std::cout<<a << ", " << b << ", " << c << "\n";
}
*/

// Templates definition
template<typename T>
struct is_pointer{
    static constexpr bool value = false;
};

// specialization
template<typename T>
struct is_pointer<T*>{ // Note the <T*>
    static constexpr bool value = true;
};

template<typename T>
void print1(T t)
{
    if constexpr(is_pointer<T>::value){
        std::cout << *t;
    }else{
        std::cout<< t;
    }
}

template<typename A, typename B, typename C>
void print3(A a,B b,C c){
    print1(a);
    std::cout <<", ";
    print1(b);
    std::cout <<", ";
    print1(c);
    std::cout <<"\n";
}

int main()
{
    print3(1,2,3);
    std::string hello = "hello world";
    print3(hello, 2, hello);
    print3(&hello, 2, hello);
}
~~~

## More Detailed Information
### Meta functions and manipulate types
### Note: C++20
~~~c++
#include <iostream>
#include <type_traits>

template<typename T>
struct is_pointer{
    static constexpr bool value = false;
};
template<typename T>
struct is_pointer<T*>{
    static constexpr bool value = true;
};

template<typename T>
struct strip_pointer{
    using type = T;
};

template<typename T>
struct strip_pointer<T*>{
    using type = T;
};

template<typename T>
void print1(T t){
    using T_without_pointer = strip_pointer<T>::type; // C++ 20's method
    if constexpr(is_pointer<T>::value && std::is_floating_point<T_without_pointer>::value){
        std::cout << *t;
    }else{
        std::cout<< t;
    }
}

template<typename A, typename B, typename C>
void print3(A a,B b,C c){
    print1(a);
    std::cout <<", ";
    print1(b);
    std::cout <<", ";
    print1(c);
    std::cout <<"\n";
}

int main()
{
    print3(1,2,3);
    std::string hello = "hello world";
    print3(hello, 2, hello);
    print3(&hello, 2, hello);
    float a = 10;
    double b = 2;
    print3(&hello, &a, &b);
}
~~~


### Ref:
[1] [Intro to Template Metaprogramming - Template Metaprogramming in C++ - E1](https://www.youtube.com/watch?v=VBI6TSo8Zog&list=PLWxziGKTUvQFIsbbFcTZz7jOT4TMGnZBh)

### Date
2022/11/25