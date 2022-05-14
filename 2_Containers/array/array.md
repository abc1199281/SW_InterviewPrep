# Array
## Motivation
- Why this? What's the difference of between c-style array?
- This class merely adds a layer of member and global functions to it, so that arrays can be used as standard containers.


## Properties
- Fixed-size
    - no contraction or expansion
- Only its elements. 
    - no size info
    - We can call size() function.
- Effecient in terms of storage size.
- class instead of pointer, not support pointer operation.
    - Exception: .data() operation


## Internal Implementations
## Basic operations
### 1. Initialization
~~~c++
#include <array>

std::array<int, 5> a;
a.fill(10);
~~~
### 2. Access
~~~c++
// might be segmentation error from OS.
cout<<a[0]

// out of range error
cout<<a.at(0) 
~~~
### 3. Search (Iteration)
~~~c++
for (const auto& it : c0)
{
    std::cout << " " << it;
}
~~~
### 4. Insertion
- N/A, array is fixed-size.
### 5. Deletion
- N/A, array is fixed-size.
### 6. Algorithms (e.g., sort)
~~~c++
std::array<double, 10> b = {26, 9.2, 633, 8.31, 9.11};
std::sort(b.begin(), b.end());
~~~

## Alternatives and Comparison
- Comparison with vector

||vector|array|
|-|-|-|
|Memoray location|Heap|Stack|
|Runtime|Dynamic|Fixed-size|
    
    
- Comparison with c-style array

||c-style|c++11|
|-|-|-|
|Format|pointer|class|
|Performance|= |= (almost same)|
|OOR|undefined error|run-time error|

- Comparison with others

| Header | DataStructure | Implementation |Note| c++11|
|-|-|-|-|- |
|\<array\> | [array](../2_Containers/array/array.md) |[Array](../1_DataStructure/ch2_Array/Array.md)|Fixed-size|v| 
|\<deque\>|[deque](../2_Containers/deque/deque.md) |[Array](../1_DataStructure/ch2_Array/Array.md)|-|-| 
|\<vector\>|[vector](../2_Containers/vector/vector.md) |[Array](../1_DataStructure/ch2_Array/Array.md)|-|-|  
