# E4 Starting a Metaprogramming Library

## Summary
0. Motivation:  
    ~~~c++
    // input
    using my_list = type_list<int, bool, float>;

    // target functions
    empty_v<my_list>                // false
    front_t<my_list>                // int
    pop_front_t<my_list>            // type_list<bool, float>
    contains_type_v<bool, my_list>  // true
    ~~~
1. Core technique:
    - template specialization
    - alias template


## Meta programming 
~~~c++
// Type your code here, or load an example.
#include <iostream>
#include <type_traits>
#include <tuple>
#include <vector>
#include <string>
#include <list>

template<bool condition, typename THEN, typename ELSE>
struct if_;

template<typename THEN, typename ELSE>
struct if_<true, THEN, ELSE>{
    using type = THEN;
};

template<typename THEN, typename ELSE>
struct if_<false, THEN, ELSE>{
    using type = ELSE;
};

template<typename ...>
struct type_list{};

template<typename LIST>
struct empty: std::false_type{};

template<>
struct empty<type_list<>>: std::true_type{};

static_assert(empty<type_list<>>::value);
static_assert(empty<type_list<float>>::value==false);


template<typename LIST>
struct front{};

template<typename T0, typename ... T1toN>
struct front<type_list<T0, T1toN...>>{
    using type=T0;
};

static_assert(std::is_same_v<front<type_list<int, bool>>::type, int>);

template<typename LIST>
struct pop_front;

template<typename T0, typename ... T1toN>
struct pop_front<type_list<T0, T1toN...>>{
    using type = type_list<T1toN...>;
};

static_assert(std::is_same_v<pop_front<type_list<int, bool, float>>::type, type_list<bool, float>>);

template<typename LIST>
using front_t = typename front<LIST>::type;

template<typename LIST>
using pop_front_t = typename pop_front<LIST>::type;

template<typename LIST>
static constexpr bool empty_v = empty<LIST>::value;

template<typename SEARCH, typename LIST>
struct contains_type:
if_<   // IF
        std::is_same_v<SEARCH, front_t<LIST>>,
        // THEN
        std::true_type,
        // ELSE             
        contains_type<SEARCH, pop_front_t<LIST>>
    >::type
{};

template<typename SEARCH>
struct contains_type<SEARCH, type_list<>>:std::false_type{};

bool contains(const std::string& search, std::list<std::string> l){
    if(l.empty()){
        return false;
    }else{
        if(search == l.front()){
            return true;
        }else{
            l.pop_front();
            return contains(search, l);
        }
    }
}

int main()
{
    std::list<std::string> list_test{"int", "bool", "double"};
    std::cout << std::boolalpha;
    std::cout << contains("bool",list_test)<<'\n';
    std::cout << contains("float",list_test)<<'\n';

    type_list<int, bool, double> types;
    std::cout << contains_type<bool, decltype(types)>::value<<'\n';
    std::cout << contains_type<float, decltype(types)>::value<<'\n';
    type_list<> types2;
    std::cout << contains_type<float, decltype(types2)>::value<<'\n';
}
~~~

### Ref:
[1] [Starting a Metaprogramming Library - Template Metaprogrammning in C++ - E4](https://www.youtube.com/watch?v=-QuFIF8ucI4&list=PLWxziGKTUvQFIsbbFcTZz7jOT4TMGnZBh&index=4)

### Date
2022/11/26