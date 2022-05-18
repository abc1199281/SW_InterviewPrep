# std::list<T, Allocator>::emplace_back

## Declaration
~~~c++
// Appends a new element to the end of the container.
template< class... Args>
void emplace_back(Args&&... args);
~~~
## Introduction
Appends a new element to the end of the container.
No move.

## Return value
1. (none) (until c++17)
2. A reference to the inserted element (since C++17)

## Complexity
1. Constant

## Examples
~~~c++
#include <list>
#include <string>
#include <cassert>
#include <iostream>

struct President
{
    std::string name;
    std::string country;
    int year;
 
    President(std::string p_name, std::string p_country, int p_year)
        : name(std::move(p_name)), country(std::move(p_country)), year(p_year)
    {
        std::cout << "I am being constructed.\n";
    }
    President(President&& other)
        : name(std::move(other.name)), country(std::move(other.country)), year(other.year)
    {
        std::cout << "I am being moved.\n";
    }
    President& operator=(const President& other) = default;
};

int main(){
    std::list<President> elections;
    std::cout << "emplace_back:\n";
    auto& ref = elections.emplace_back("Nelson Mandela", "South Africa", 1994);
    assert(ref.year == 1994 && "uses a reference to the created object (C++17)");
 
    std::list<President> reElections;
    std::cout << "\npush_back:\n";
    reElections.push_back(President("Franklin Delano Roosevelt", "the USA", 1936));
 
    std::cout << "\nContents:\n";
    for (President const& president: elections) {
        std::cout << president.name << " was elected president of "
                  << president.country << " in " << president.year << ".\n";
    }
    for (President const& president: reElections) {
        std::cout << president.name << " was re-elected president of "
                  << president.country << " in " << president.year << ".\n";
    }
}
~~~
Possible output
~~~c++
emplace_back:
I am being constructed.
 
push_back:
I am being constructed.
I am being moved.
~~~

