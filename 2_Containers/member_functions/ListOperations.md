# List Operations
## Introduction
1. only supported by List, forward_list

## List
1. splice
    - Transfers elements from one list to another.
    - called "splice_after" in forward_list
    - Complexity: O(1), constant
2. remove / remove_if
    - Removes all elements satisfying specific criteria.
    - Copmlexity: O(n), linear
~~~c++
std::list<int> l ={1,2,3,4,5,6,7,8,9,10};

auto count2 = l.remove_if([](int n){return n>10;});
std::cout<<count2<<"elements greater than 10";
~~~

3. reverse
    - Complexity: O(n), linear
4. unique
    - Removes all consecutive duplicate elements from the container. 
    - Complexity: O(n), linear comparison
5. sort
    - \<algorithm\> std::sort require random access, so cannot be used with list.
    - Complexity: Approximately o(nlogn)
~~~ c++
std::list<int> list = {8,7,6,5,4,3,2,1};
list.sort(); // ascending
list.sort(std::greater<int>()); //descending
~~~