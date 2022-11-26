# E3, How to print elements in tuples?

## Summary
0. Motivation:  using variadic template

## Meta programming version
~~~c++
// Type your code here, or load an example.
#include <iostream>
#include <type_traits>
#include <tuple>

void printn(){
    std::cout << '\n';
}

template<typename LAST>
void printn(LAST t){
    std::cout << t << '\n';
}

template<typename T0, typename... T1toN> // ... in front of name: Variable number of elements (here typenames)
void printn(T0 t0, T1toN ... rest){ // between nuame: define second name as list of param given by the first.
    std::cout<<t0 << ", ";
    //if constexpr(sizeof...(rest)>0)
    //    printn(rest...); //... after name: expand name to a list of all elements it represents.
    printn(rest...); //... after name: expand name to a list of all elements it represents.
}

template<typename TUPLE, std::size_t ... indices>
void print_tuple_impl(TUPLE t, std::index_sequence<indices...>){
    printn(std::get<indices>(t)...); // printn(std::get<0>(t), std::get<1>(t), std:;get<2>(t)...);
}

template<typename TUPLE>
void print_tuple(TUPLE t){
    print_tuple_impl(t, std::make_index_sequence<std::tuple_size<TUPLE>::value>{});
}

int main()
{
    printn(9, "hello", 1.5, true);
    printn();
    printn(123,222);

    auto tuple = std::make_tuple(9, "hello world", 1.5, true);
    print_tuple(tuple);
}
~~~

### Perfect forwarding:
~~~c++
#include <iostream>
#include <type_traits>
#include <tuple>

void printn(){
    std::cout << '\n';
}

template<typename LAST>
void printn(LAST&& t){
    std::cout << std::forward<LAST>(t) << '\n';
}

template<typename T0, typename... T1toN> // ... in front of name: Variable number of elements (here typenames)
void printn(T0 t0, T1toN ... rest){ // between nuame: define second name as list of param given by the first.
    std::cout<< std::forward<T0>(t0) << ", ";
    //if constexpr(sizeof...(rest)>0)
    //    printn(rest...); //... after name: expand name to a list of all elements it represents.
    printn(std::forward<T1toN>(rest)...); //... after name: expand name to a list of all elements it represents.
}

template<typename TUPLE, std::size_t ... indices>
void print_tuple_impl(TUPLE &&t, std::index_sequence<indices...>){
    printn(std::get<indices>(std::forward<TUPLE>(t))...); // printn(std::get<0>(t), std::get<1>(t), std:;get<2>(t)...);
}

template<typename TUPLE>
void print_tuple(TUPLE&& t){
    print_tuple_impl(std::forward<TUPLE>(t), std::make_index_sequence<std::tuple_size<std::remove_reference_t<TUPLE>>::value>{});
}

int main()
{
    printn(9, "hello", 1.5, true);
    printn();
    printn(123,222);

    auto tuple = std::make_tuple(9, "hello world", 1.5, true);
    print_tuple(tuple);
}
~~~

### Ref:
[1] [Writing MetaFunctions - Template Metaprogramming in C++ - E3](https://www.youtube.com/watch?v=GusZ4P_iTks&list=PLWxziGKTUvQFIsbbFcTZz7jOT4TMGnZBh&index=3)

### Date
2022/11/25