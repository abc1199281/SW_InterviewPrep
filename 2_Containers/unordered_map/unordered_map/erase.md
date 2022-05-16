# std::unordered_map<Key,T,Hash, KeyEqual, Allocator>::erase

## Declaration
~~~c++
// 1. removes the element at pos
iterator erase(iterator pos);
iterator erase(const_iterator pos);

// 2. removes the elements in the range [first, last), which must be a valid range in *this.
iterator erase(iterator first, iterator last);
iterator erase(const_iterator first, const_iterator last);
~~~

## Return value
iterator following the last removed element.

## Complexity
1. O(1) = t(1)
2. T=O(std::distance(first, last))

## Examples
~~~c++
#include <list>
#include <iostream>
#include <iterator>
void print_container(const std::list<int>&c){
    for(int i:c){
        std::cout<< i <<" ";
    }
    std::cout <<"\n";
}
int main(){
    std::list<int> c{0,1,2,3,4,5,6,7,8,9};
    print_container(c);

    c.erase(c.begin());
    print_container(c);

    std::list<int>::iterator range_begin = c.begin();
    std::list<int>::iterator range_end = c.begin();
    std::advance(range_begin, 2);
    std::advance(range_end, 5);

    c.erase(range_begin, range_end);
    print_container(c);

    // Erase all even numbers
    for(std::list<int>::iterator it = c.begin(); it!=c.end();){
        if(*it%2==0){ // get value
            it = c.erase(it);
        }else{
            it++;
        }
    }
    print_container(c);
}
~~~
Possible output
~~~c++
0 1 2 3 4 5 6 7 8 9
1 2 3 4 5 6 7 8 9
1 2 6 7 8 9
1 7 9 
~~~

