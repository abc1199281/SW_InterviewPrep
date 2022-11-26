# E6 Composing Metafunctions

## Summary
0. Motivation:  
    ~~~c++
    // input
    using my_list = type_list<int, bool, float>;

    // existing functions
    empty_v<my_list>                // false
    front_t<my_list>                // int
    pop_front_t<my_list>            // type_list<bool, float>
    contains_type_v<bool, my_list>  // true

    // new functions
    back_t<my_list>               
    push_back_t<my_list>
    pop_back_t<my_list>
    at_t<my_list, idx>      
    ~~~

## Meta programming 
~~~c++
#include <iostream>
#include <type_traits>
#include <tuple>
#include <vector>
#include <string>
#include <list>

template<typename T>
struct has_type{
    using type = T;
};

///*************************************************************************
/// IF
template<bool condition, typename THEN, typename ELSE>
struct if_;

template<typename THEN, typename ELSE>
struct if_<true, THEN, ELSE>: has_type<THEN>{};

template<typename THEN, typename ELSE>
struct if_<false, THEN, ELSE>: has_type<ELSE>{};


///*************************************************************************
template<typename ...>
struct type_list{};


///*************************************************************************
/// Empty
template<typename LIST>
struct empty: std::false_type{};

template<>
struct empty<type_list<>>: std::true_type{};

static_assert(empty<type_list<>>::value);
static_assert(empty<type_list<float>>::value==false);

template<typename LIST>
static constexpr bool empty_v = empty<LIST>::value;

///*************************************************************************
/// Front
template<typename LIST>
struct front{};

template<typename T0, typename ... T1toN>
struct front<type_list<T0, T1toN...>>: has_type<T0>{};

template<typename LIST>
using front_t = typename front<LIST>::type;

static_assert(std::is_same_v<front<type_list<int, bool>>::type, int>);


///*************************************************************************
/// pop_front
template<typename LIST>
struct pop_front;

template<typename T0, typename ... T1toN>
struct pop_front<type_list<T0, T1toN...>>: has_type<type_list<T1toN...>>{};

static_assert(std::is_same_v<pop_front<type_list<int, bool, float>>::type, type_list<bool, float>>);

template<typename LIST>
using pop_front_t = typename pop_front<LIST>::type;

///*************************************************************************
/// BACK
template<typename LIST>
struct back: has_type<typename back<pop_front_t<LIST>>::type>{};

template<typename T0>
struct back<type_list<T0>>: has_type<T0>{};

template<typename LIST>
using back_t = typename back<LIST>::type;

static_assert(std::is_same_v<typename back<type_list<int, bool ,float>>::type, float>);

///*************************************************************************
/// PUSH_BACK

template<typename LIST, typename T>
struct push_back;

template<typename ... T0toN, typename T>
struct push_back<type_list<T0toN...>, T>: has_type<type_list<T0toN..., T>>{};

template<typename LIST, typename T>
using push_back_t = typename push_back<LIST, T>:: type;

static_assert(std::is_same_v<push_back_t<type_list<>, int>, type_list<int>>);
static_assert(std::is_same_v<push_back_t<type_list<int, bool>, float>, type_list<int, bool, float>>);

///*************************************************************************
/// POP_BACK
template<typename LIST, typename RET_LIST = type_list<>>
struct pop_back;

template<typename T0, typename RET_LIST>
struct pop_back<type_list<T0>, RET_LIST>: has_type<RET_LIST>{};

template<typename T0, typename T1, typename...T2toN, typename RET_LIST>
struct pop_back<type_list<T0, T1, T2toN...>, RET_LIST>:
    pop_back<type_list<T1, T2toN...>, push_back_t<RET_LIST,T0>>{};
    
template<typename LIST>
using pop_back_t = typename pop_back<LIST>::type;

static_assert(std::is_same_v<pop_back_t<type_list<int>>, type_list<>>);
static_assert(std::is_same_v<pop_back_t<type_list<int, bool, float>>, type_list<int, bool>>);
static_assert(std::is_same_v<pop_back_t<type_list<int, bool>>, type_list<int>>);

///*************************************************************************
/// AT

template<typename LIST, size_t index>
struct at: has_type<typename at<pop_front_t<LIST>, index-1>::type>{};

template<typename LIST>
struct at<LIST, 0>: has_type<front_t<LIST>>{};

template<typename LIST, size_t index>
using at_t = typename at<LIST, index>::type;

static_assert(std::is_same_v<at_t<type_list<int, bool, float>, 1>, bool>);
static_assert(std::is_same_v<at_t<type_list<int, bool, float>, 2>, float>);

///*************************************************************************
/// contains_type
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

template<typename SEARCH, typename LIST>
static constexpr bool contains_type_v = contains_type<SEARCH, LIST>::value;

int main()
{
    type_list<int, bool, double> types;
    std::cout << contains_type_v<bool, decltype(types)><<'\n';
    std::cout << contains_type_v<float, decltype(types)><<'\n';
    type_list<> types2;
    std::cout << contains_type_v<float, decltype(types2)><<'\n';
}
~~~

### Ref:
[1] [Composing Metafunctions - Template Metaprogrammning in C++ - E6](https://www.youtube.com/watch?v=k9Y8m_Pvx54&list=PLWxziGKTUvQFIsbbFcTZz7jOT4TMGnZBh&index=6)

### Date
2022/11/26