# std::list<T, Allocator>::erase

## Declaration
~~~c++
// 1. removes the element at pos
iterator erase(iterator pos);
iterator erase(const_iterator pos);

// 2. removes the elements in the range [first, last), which must be a valid range in *this.
iterator erase(const_iterator first, const_iterator last);

// 3. removes the element (if one exists) with the key equivalent to key.
size_type erase(const Key&key);
~~~
## Return value
1. iterator following the last removed element.
2. iterator following the last removed element.
3. Number of elements removed (0 or 1).

## Complexity
1. t(1), O(c.size())
2. t(std::distance(first, last)), O(c.size())
3. t(c.count(key)), O(c.size())

## Examples
~~~c++
#include <unordered_map>
#include <iostream>
int main(){
    std::unordered_map<int, std::string> c= {
        {1,"one"}, {2,"two"}, {3,"three"},
        {4,"four"}, {5,"five"}, {6,"six"}
    };

    // erase all odd numbers from c
    for(auto it = c.begin();it != c.end();){
        if(it->first%2!=0){
            it = c.erase(it);
        }else{
            it++;
        }        
    }

    for(auto &p:c){
        std::cout<<p.second<<" ";
    }
}
~~~
Possible output
~~~c++
two four six
~~~

