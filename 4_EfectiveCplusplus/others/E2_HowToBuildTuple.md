# How to build contain types in tuples?

## Summary
0. Motivation: 
    ~~~c++
    std::tuple<int, bool> t1;
    std::tuple<int, bool, float> t;
    // Key: std::get(): return the reference of type of element
    std::get<2>(t)-->float
    std::get<float>(t) = 1.5F;
    std::get<double>(t);-->error

    // Key: contains_type
    std::tuple<int, bool, float> t;
    contains_type<double, decltype(t)>::value== false;
    contains_type<float, decltype(t)>::value== true;
    ~~~

## Vector version
### No use of std::find, loop    
~~~c++
#include <iostream>
#include <tuple>
#include <vector>
#include <string>

bool contains(const std::string& search, const std::vector<std::string>& v, size_t start_from= 0){

    if(v[start_from]== search){
        return true;
    }else{
        if(start_from == v.size()-1){// we are at the last element.
            return false;
        }else{
            return contains(search, v, start_from+1);
        }
    }
}

int main()
{

    std::vector<std::string> vec{"int", "bool", "float"};
    std::cout<< std::boolalpha << contains("bool", vec) << '\n';
    std::cout<< std::boolalpha << contains("double", vec) << '\n';
}
~~~

## Meta programming version
~~~c++
#include <iostream>
#include <tuple>
#include <vector>
#include <string>

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

template<typename SEARCH, typename TUPLE, size_t start_from = 0>
struct contains_type:
    if_< // IF
        std::is_same<std::tuple_element_t<start_from, TUPLE>, SEARCH>:: value,
        // THEN
        std::true_type,
        // ELSE
        typename if_<
            (start_from == std::tuple_size<TUPLE>::value -1 ),
            // THEN
            std::false_type,
            // ELSE
            contains_type<SEARCH, TUPLE, start_from+1>
        >::type
    >::type
{}; 

template<typename SEARCH>
struct contains_type<SEARCH, std::tuple<>, 0>:std::false_type{};

bool contains(const std::string& search, const std::vector<std::string>& v, size_t start_from= 0){
    if(v[start_from]== search){
        return true;
    }else{
        if(start_from == v.size()-1){// we are at the last element.
            return false;
        }else{
            return contains(search, v, start_from+1);
        }
    }
}

int main()
{

    std::tuple<int, bool, float> tuple;
    std::cout<< std::boolalpha << contains_type<double, decltype(tuple)>::value << '\n';
    std::cout<< std::boolalpha << contains_type<float, decltype(tuple)>::value << '\n';
    //std::cout<< std::boolalpha << std::is_same<int, if_<(10<5), int, float>::type>::value << '\n';
    std::cout<< contains_type<bool, std::tuple<>>::value <<'\n';
}
~~~

### Ref:
[1] [Writing MetaFunctions - Template Metaprogramming in C++ - E2](https://www.youtube.com/watch?v=_yqIdYBdyPo&list=PLWxziGKTUvQFIsbbFcTZz7jOT4TMGnZBh&index=2)

### Date
2022/11/25