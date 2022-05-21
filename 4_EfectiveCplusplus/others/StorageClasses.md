# What is the Storage Classes in C/C++?

## Quick Answer
- Why this?
    - The storage class of a C++ variable determines its "lifetime", how long it remains in the computer's memory.
    - Determine [Memory Layout](../others/MemoryLayout.md).
- C: 4 storage classes.

Specifier|Storage|Initial Value|Visibility|Life|
-|-|-|-|-|
auto| stack | Garbage | local | End of block|
extern|Data Segment|0|Global multiple files|Start and End of program|
static|Data Segment|0|local|Start and End of program|
register|CPU register|Garbage|local|End of block|

- C: add an new storage classes.

Specifier|Storage|Initial Value|Visibility|Life|
-|-|-|-|-|
mutable| - | Garbage | Local | Class|
thread_local (c++11)| - | - | Local | thread begins and end|

- Additional: Dynamice variables

Specifier|Storage|Initial Value|Visibility|Life|
-|-|-|-|-|
new| Heap | - | Local | delete or program end|


## Detailed information
### Storage duration
- **automatic** storage duration
    - Memory layout: **Stack**
    - All local objects have this storage duration, except those declared *static, extern, or thread_local*.
- **static** storage duration
    - Memory layout: **Data Segment (BSS)**.
    - Start and End of program.
    - Only one instance of the object exist.
    - Types:
        - Declared with *static, extern*.
        - All object declared at namespace scope (including global namespace) have this storage duration.
- **thread** storage duration.
    - Thread begins and end.
    - Each thread has its own instance of the object.
    - Only object with thread_local have this storage duration.
- **dynamic** storage duration
    - Memory layout: **Heap (Free Storage)**.

## Linkage
A name that denotes object, reference, function, type, template, namespace, or value, may have linkage. If a name has linkage, it refers to the same entity as the same name introduced by a declaration in another scope.

- **No linkage**
    - variables that aren't explicitly declared *extern*. (regardless of the *static* modifier.)
- **internal linkage**
    - The name can be referred in the current translation unit.
    - declared *static*
- **external linkage**
    - not listed above.

## Ref
1. [Storage Class](http://faculty.cs.niu.edu/~mcmahon/CS241/Notes/storage_class.html)
2. [cppreference](https://en.cppreference.com/w/cpp/language/storage_duration)