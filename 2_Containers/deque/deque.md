# deque
## Introduction
- Deque allocates its internal storage in blocks of pre-defined size via vector.

## Alternatives
| header | Implementation |Note| c++11|
|-|-|-|- |
array |[Array](..\1_DataStructure\ch2_Array\Array.md)|Fixed-size|Y|
deque |[Array](..\1_DataStructure\ch2_Array\Array.md)|1|Y|

## Summary of [link2](https://www.codeproject.com/Articles/5425/An-In-Depth-Study-of-the-STL-Deque-Container)

Experiment|vector|deque|Reason|
-|-|-|-|
Dynamic Add items|V||Need to reallocate
Reverse first|=|=|Same
dealocation memory|O(Poly)|O(linear)V|vector is continuous memroy
insert|V,O(1)||

 - The datas in deque are stored by chuncks of fixed size vector, which are pointered by a *map*(which is also a chunk of vector, but its size may change)

### Notes
1. The data in **deque** are stored by chuncks of **fixed size vector**, which are pointered by a **map** (which is also a chunk of vector with varied size). ([link1](https://stackoverflow.com/questions/6292332/what-really-is-a-deque-in-stl), [link2](https://www.codeproject.com/Articles/5425/An-In-Depth-Study-of-the-STL-Deque-Container))

## Refference
[1] Fundamentals of Data Structures in C++ (2e), Ellis Horowitz, Sartaj Sahni, Dinesh P. Mehta.
