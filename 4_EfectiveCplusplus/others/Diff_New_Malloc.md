# What is the difference between Malloc & New

## Summary
1. **new/delete**: do
    - new: 
        1. allocates memory
        2. call constructor
    - delete:
        1. calls destructor
        2. deallocates memory
2. **malloc/free**: do
    - malloc: allocate memory
    - free: deallocate memory

## Detailed information

Feature|new/delete|malloc/free|
-|-|-|
Memory Allocated|'FreeStore'|'Heap'|
Returns|Fully typed pointer| void*|
On failure|Throws (never returns NULL)|Returns NULL|
Require Size|Calculated by complier|Must be specified in bytes|
Handling arrays|Has an explicit version|Requires manual calculations|
Reallocating|Not handled intuitively|Simple(no copy constructor)|
Call of reverse|Implementation defined|No|
Low memory cases|Can add a new memory allocator|Not handled by user code|
Overridable|Yes|No|

## Ref:
[1] [What is the difference between new/delete and malloc/free?](https://stackoverflow.com/questions/240212/what-is-the-difference-between-new-delete-and-malloc-free)